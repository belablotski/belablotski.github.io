+++
date = '2025-08-03T19:01:03-08:00'
draft = false
title = 'Semantic Kernel and AutoGen: Microsoft stack for Multi-Agent AI'
tags = ['engineering', 'ai']
+++

## Microsoft Semantic Kernel

[Semantic Kernel](https://learn.microsoft.com/en-us/semantic-kernel/get-started/quick-start-guide) is a lightweight, open-source development kit that lets you easily build AI agents and integrate the latest AI models into your C#, Python, or Java codebase. It serves as an efficient middleware that enables rapid delivery of enterprise-grade solutions.

1. Code https://github.com/microsoft/semantic-kernel
2. Python examples https://github.com/microsoft/semantic-kernel/tree/main/python/samples
1. [semantic_kernel Package](https://learn.microsoft.com/en-us/python/api/semantic-kernel/semantic_kernel?view=semantic-kernel-python)

### [Kernel](https://learn.microsoft.com/en-us/semantic-kernel/concepts/kernel?pivots=programming-language-python)

The kernel is the central component of Semantic Kernel. At its simplest, the kernel is a Dependency Injection container that manages all of the services and plugins necessary to run your AI application. 

* **Services**: both AI services (e.g., chat completion) and other services (e.g., logging and HTTP clients) that are necessary to run application.
* **Plugins**: these are the components that are used by your AI services and prompt templates to perform work (retrieve data from DB, call APIs, etc.).

#### [Creating a MCP Server from your Kernel](https://learn.microsoft.com/en-us/semantic-kernel/concepts/kernel?pivots=programming-language-python#creating-a-mcp-server-from-your-kernel)

Create an MCP server from the function you have registered in your Semantic Kernel instance.

```
...
server = kernel.as_mcp_server(server_name="...")
```

Make of online with stdio:

```
import anyio
from mcp.server.stdio import stdio_server

async def handle_stdin(stdin: Any | None = None, stdout: Any | None = None) -> None:
    async with stdio_server() as (read_stream, write_stream):
        await server.run(read_stream, write_stream, server.create_initialization_options())

anyio.run(handle_stdin)
```

or SSE

```
import uvicorn
from mcp.server.sse import SseServerTransport
from starlette.applications import Starlette
from starlette.routing import Mount, Route

sse = SseServerTransport("/messages/")

async def handle_sse(request):
    async with sse.connect_sse(request.scope, request.receive, request._send) as (read_stream, write_stream):
        await server.run(read_stream, write_stream, server.create_initialization_options())

starlette_app = Starlette(
    debug=True,
    routes=[
        Route("/sse", endpoint=handle_sse),
        Mount("/messages/", app=sse.handle_post_message),
    ],
)

uvicorn.run(starlette_app, host="0.0.0.0", port=8000)
```

#### [Kernel components](https://learn.microsoft.com/en-us/semantic-kernel/concepts/semantic-kernel-components?pivots=programming-language-python#ai-service-connectors)

* AI Service Connectors
* Vector Store (Memory) Connectors
* Functions and Plugins (created from from native code, OpenAPI specs, ITextSearch implementations for RAG scenarios, and also from prompt templates)
* Prompt Templates
   * Starting point of a Chat Completion flow
   * Plugin function
* Filters
   * Before and after function invocation.
   * Before and after prompt rendering.

### [Function Calling](https://learn.microsoft.com/en-us/semantic-kernel/concepts/ai-services/chat-completion/function-calling/?pivots=programming-language-python)

[Reserved Names](https://learn.microsoft.com/en-us/semantic-kernel/concepts/ai-services/chat-completion/function-calling/?pivots=programming-language-python#reserved-names)
* kernel: Injected with the kernel object.
* service: Populated with the AI service selected based on the provided arguments.
* execution_settings: Contains settings pertinent to the function's execution.
* arguments: Receives the entire set of kernel arguments passed during invocation.
* return value: Type of the return value is not being serialized.

#### [Planning](https://learn.microsoft.com/en-us/semantic-kernel/concepts/planning?pivots=programming-language-python)

Semantic Kernel automates this loop:

1. Create JSON schemas for each of your functions
2. Provide the LLM with the previous chat history and function schemas
3. Parse the LLM's response to determine if it wants to reply with a message or call a function
4. If the LLM wants to call a function, you would need to parse the function name and parameters from the LLM's response
5. Invoke the function with the right parameters
6. Return the results of the function so that the LLM can determine what it should do next
7. Repeat steps 2-6 until the LLM decides it has completed the task or needs help from the user

#### VSCode / Copilot Studio integration

* The **Semantic Kernel Tools extension** is a Visual Studio Code extension designed to assist developers working with Microsoft's Semantic Kernel SDK.
* Semantic Kernel can be used to build custom agents that can be integrated with **Microsoft Copilot Studio**. This allows you to leverage Semantic Kernel's orchestration capabilities and connect your custom agents to Copilot Studio's features, including knowledge bases and conversational flows.

### [Semantic Kernel Agent Framework](https://learn.microsoft.com/en-us/semantic-kernel/frameworks/agent/?pivots=programming-language-python)

An AI agent is a software entity designed to perform tasks autonomously or semi-autonomously by receiving input, processing information, and taking actions to achieve specific goals.

* Modular Components
* Collaboration
* Human-Agent Collaboration
* Process Orchestration

When to use an AI agent?

* Autonomy and Decision-Making
* Multi-Agent Collaboration
* Interactive and Goal-Oriented

Goals of SK Agent Framework:

* The Semantic Kernel agent framework serves as the core foundation for implementing agent functionalities.
* Multiple agents of different types can collaborate within a single conversation, each contributing their unique capabilities, while integrating human input.
* An agent can engage in and manage multiple concurrent conversations simultaneously.

## Microsoft AutoGen

[AutoGen](https://www.microsoft.com/en-us/research/project/autogen/) is an open-source programming framework for building AI agents and facilitating cooperation among multiple agents to solve tasks.

1. Code https://github.com/microsoft/autogen
2. Docs https://www.microsoft.com/en-us/research/project/autogen/ and https://microsoft.github.io/autogen/stable/
3. User guide https://microsoft.github.io/autogen/stable/user-guide/agentchat-user-guide/index.html

AutoGen components:

* AutoGen Studio
* AgentChat
* AutoGen Core
* Extensions

## AutoGen and Semantic Kernel

The connection between the new Semantic Kernel (SK) Agent framework and AutoGen is designed to be direct and complementary.

Think of it as a two-layer stack:

1.  **The Individual Specialist Agent (Semantic Kernel):** The `Agent` framework is for building a single, self-contained, and highly capable agent.
2.  **The Multi-Agent Team (AutoGen):** AutoGen is the framework for making multiple agents (some of which can be Semantic Kernel agents) collaborate to solve a complex problem.

Here’s a more detailed breakdown of the relationship:

### Layer 1: Building the Specialist with Semantic Kernel

The `semantic_kernel.Agent` class is designed to create a single, powerful agent. Its core components are:

*   **Plugins:** A collection of "skills" you give the agent (e.g., a `WebSearchPlugin`, a `CodeInterpreterPlugin`, a `FileSystemPlugin`). These are the tools the agent can use.
*   **Planner:** An internal mechanism that allows the agent to look at a user's request, analyze the tools (plugins) it has, and create a step-by-step plan to achieve the goal.
*   **Kernel:** The engine that orchestrates the planner and the plugins.

You use the *Semantic Kernel framework to build a self-sufficient "specialist."* For example, you could build a `DatabaseAdminAgent` that has plugins for connecting to a database, querying tables, and generating reports. This agent, on its own, is very good at its specific job.

### Layer 2: Orchestrating the Team with AutoGen

AutoGen's primary role is to manage conversations between multiple agents. It excels at creating workflows where agents with different specializations can talk to each other to get a job done.

#### The Connection: How They Work Together

The key is that a **Semantic Kernel agent is designed to be seamlessly used as a `ConversableAgent` within the AutoGen framework.**

You don't choose one or the other; you use them together.

**Here is a practical example workflow:**

Imagine you want to build a system that can analyze sales data and create a presentation.

1.  **Build a Specialist SK Agent:**
    Using the `semantic_kernel.Agent` framework, you create a `DataAnalysisAgent`.
    *   You give it a `DatabasePlugin` to query your sales database.
    *   You give it a `PandasPlugin` to perform data analysis.
    *   This agent's instructions are: "You are an expert data analyst. When given a request, use your tools to query the database, analyze the data, and provide a summary."

2.  **Build another Specialist SK Agent:**
    You create a `PresentationAgent` using `semantic_kernel.Agent`.
    *   You give it a `PowerPointPlugin` (hypothetically) that can create slides and add text and charts.
    *   Its instructions are: "You are an expert at creating PowerPoint presentations. Use the data and summaries provided to you to create a slide deck."

3.  **Orchestrate them with AutoGen:**
    You set up an AutoGen `GroupChatManager` with a team of agents:
    *   A `UserProxyAgent` (representing you).
    *   Your `DataAnalysisAgent` (built with Semantic Kernel).
    *   Your `PresentationAgent` (built with Semantic Kernel).

**The conversation would flow like this:**

1.  **You (UserProxyAgent):** "Analyze last quarter's sales data and create a presentation summarizing the key trends."
2.  **AutoGen (GroupChatManager):** Sees the request and routes it to the `DataAnalysisAgent` first, since data analysis is needed before a presentation can be made.
3.  **DataAnalysisAgent (Semantic Kernel):** Receives the task. Its internal SK planner creates a plan:
    *   Step 1: Use `DatabasePlugin` to get sales data.
    *   Step 2: Use `PandasPlugin` to find key trends.
    *   It executes this plan and replies to the chat: "I have analyzed the data. The key trends are a 15% increase in sales in the North region and a 5% decrease in the South region."
4.  **AutoGen (GroupChatManager):** Sees the analysis is complete and routes the conversation and the summary to the `PresentationAgent`.
5.  **PresentationAgent (Semantic Kernel):** Receives the summary. Its internal SK planner creates a plan to use its `PowerPointPlugin` to create a title slide, a slide for the North region trend, and a slide for the South region trend. It executes the plan and replies: "I have created the presentation."

### Summary of the Division of Labor

| Aspect | Semantic Kernel `Agent` | AutoGen Framework |
| :--- | :--- | :--- |
| **Primary Role** | Defines the **capabilities and internal logic** of a single agent. | Manages the **collaborative conversation** between multiple agents. |
| **Scope** | **Intra-agent:** How an agent thinks and uses its tools (plugins) to form a plan. | **Inter-agent:** Who talks when, and how information is passed between agents. |
| **Synergy** | You build powerful, self-contained specialist agents using SK. | You use these SK agents as team members in a collaborative AutoGen workflow. |

In short, the link you provided shows you how to build the individual "workers." AutoGen is the framework you use to put those workers together on a team and manage their project.

## Analogs to AutoGen

AutoGen is a powerful framework, but several other excellent tools are available for building multi-agent systems, each with a different philosophy and focus. Here are some of the most popular analogs to AutoGen:

### 1. CrewAI

*   **Philosophy:** Role-playing, collaborative agents.
*   **Core Idea:** You define agents with specific `roles` (e.g., "Senior Researcher"), `goals` (e.g., "Find the latest AI trends"), and `backstories` (to give them context). You then define a `task` and assign it to a `crew` of these agents. CrewAI orchestrates how the agents work together, passing tasks from one to another until the goal is achieved.
*   **Key Difference from AutoGen:** CrewAI is often considered more straightforward for defining structured, assembly-line-style workflows. AutoGen is more focused on dynamic, conversational interactions between agents in a "chat" environment.
*   **Best for:** Tasks that can be broken down into a clear sequence of steps performed by different specialists.

### 2. LangGraph

*   **Philosophy:** State machines and graph-based agent workflows.
*   **Core Idea:** Built on top of LangChain, LangGraph allows you to define agent interactions as a `graph`. Each `node` in the graph is an agent or a tool, and the `edges` represent the flow of control. This gives you explicit, fine-grained control over the entire process.
*   **Key Difference from AutoGen:** LangGraph is more explicit and declarative. You define the exact paths the conversation can take, including cycles, branches, and human-in-the-loop checkpoints. AutoGen's conversations are more emergent and less explicitly defined.
*   **Best for:** Complex, stateful applications where you need precise control over the agent workflow and the ability to handle loops and human intervention.

### 3. Agent Development Kit (ADK) by Google

*   **Philosophy:** Hierarchical and composable multi-agent systems.
*   **Core Idea:** ADK is designed for building a hierarchy of specialized agents that can delegate tasks to one another. It emphasizes a structured, end-to-end development process.
*   **Key Difference from AutoGen:** ADK is built with a stronger focus on hierarchical delegation and composition from the ground up. It also has strong integrations with other Google AI tools and models.
*   **Best for:** Building complex systems where a "manager" agent might delegate sub-tasks to multiple "worker" agents.

### 4. OpenAI Swarm

*   **Philosophy:** Lightweight and simple agent handoffs.
*   **Core Idea:** An experimental framework from OpenAI that focuses on the simple concept of handing off a conversation from one agent to another. It's less feature-rich than the others but provides a clean and simple design.
*   **Key Difference from AutoGen:** Much more lightweight and less opinionated. It's more of a minimal starting point than a comprehensive framework.
*   **Best for:** Prototyping and experimenting with basic multi-agent concepts without the overhead of a larger framework.

### Summary Table

| Framework | Core Concept | Best For |
| :--- | :--- | :--- |
| **AutoGen** | Conversational agents in a group chat | Dynamic, emergent collaboration, especially for code generation. |
| **CrewAI** | Role-playing agents in a sequential crew | Structured, assembly-line workflows with clear roles. |
| **LangGraph** | State machines and graph-based workflows | Complex, stateful applications requiring explicit control and loops. |
| **ADK (Google)** | Hierarchical and composable agents | Systems with clear manager-worker delegation structures. |
| **OpenAI Swarm** | Lightweight agent handoffs | Simple prototyping and experimentation. |

While LangChain and Semantic Kernel can be used to build multi-agent systems, they are more accurately described as frameworks for building the individual agents themselves. CrewAI, LangGraph, and ADK are more direct analogs to AutoGen as they are primarily concerned with the **orchestration** of multiple agents.
