+++
date = '2025-01-18T17:54:58-08:00'
draft = false
title = 'Level-of-Effort Estimations'
tags = ['management']
toc = true
+++

## Engineering Team Planning Process - LOE Estimations

This document outlines the process followed by the engineering team for planning and estimating work for the next quarter of the fiscal year.
<!--more-->

### Input

* Organizational OKRs: The planning process is initiated by a thorough understanding of the organization's overall objectives and key results (OKRs). 
* Product Requirement Documents (PRDs): Detailed PRDs are utilized to translate high-level organizational OKRs into specific, actionable goals for the engineering team. Each PRD outlines the requirements for a particular feature or improvement.

| Product Requirements Document | Team 1 LOE | Team 1 Commitment | Team 2 LOE | Team 2 Commitment | Other teams... |
|-------------------------------|------------|-------------------|------------|-------------------|----------------|
| PRD 1 ...                     |     ?      |        ?          |     ?      |        ?          |      ...       |
| PRD 2 ...                     |     ?      |        ?          |     ?      |        ?          |      ...       |
| PRD 3 ...                     |     ?      |        ?          |     ?      |        ?          |      ...       |

### Output 

Based on the detailed scoping and LOE estimations, the work is translated into a realistic number of sprints. Each sprint typically spans two weeks, with the team focusing on delivering a specific set of features or functionalities within each sprint.

| Product Requirements Document | Team 1 LOE | Team 1 Commitment | Team 2 LOE | Team 2 Commitment | Other teams... |
|-------------------------------|------------|-------------------|------------|-------------------|----------------|
| PRD 1 ...                     |     4      |       Yes         |     8      |       Yes         |      ...       |
| PRD 2 ...                     |     5      |       No          |     4      |       No          |      ...       |
| PRD 3 ...                     |     7      |       Yes         |     1      |       No          |      ...       |

### Process

* Objective Analysis: The first step involves a detailed analysis of the "objective" component of each OKR. This provides the overarching direction and guides subsequent planning activities. 
* Key Result Definition: Based on the analyzed objective, specific, measurable, achievable, relevant, and time-bound (SMART) Key Results are defined. These KRs serve as concrete milestones for measuring progress towards the overall objective.
* Assumption & Dependency Identification: Potential assumptions and dependencies are carefully identified and documented. These include factors such as:
    * Availability of resources (e.g., data, infrastructure budget)
    * Completion of work by other teams
    * Successful integration with third-party systems
* Work Scoping: The work required from the engineering team is meticulously scoped. This involves breaking down projects into smaller, more manageable tasks and identifying the necessary resources and timelines. 
* Internal Review: Two rounds of internal review are conducted:
    * Individual Review: The Engineering Manager conducts an initial review of KRs, assumptions, scope, and LOE estimations.
    * Team Lead Review: The Engineering Manager then collaborates with team leads to double-check the accuracy and completeness of KRs, assumptions, scope, and LOE estimations.

A worksheet for LOE estimations:

| PRD   | Org OKR | TPM is needed | QA is needed | LOE | Commitment | Scope           |
|-------|---------|---------------|--------------|-----|------------|-----------------|
| PRD 1 | OKR 1   | Yes           | Yes          | 4   | Commit     | *Key Results:*  |
|       |         |               |              |     |            | 1. Key Result 1 |
|       |         |               |              |     |            | 2. Key Result 2 |
|       |         |               |              |     |            | *Scope:*        |
|       |         |               |              |     |            | 1. Todo X       |
|       |         |               |              |     |            | 2. Todo Y       |
|       |         |               |              |     |            | *Assumptions:*  |
|       |         |               |              |     |            | 1. Prereq. 1    |
|       |         |               |              |     |            | 2. Prereq. 2    |
|       |         |               |              |     |            | *Dependencies:* |
|       |         |               |              |     |            | 1. Team 1       |
|       |         |               |              |     |            | 2. Team 2       |
| PRD 2 | OKR 1   | No            | No           | 5   | No         | *Key Results:*  |
|       |         |               |              |     |            | 1. Key Result 1 |
|       |         |               |              |     |            | 2. Key Result 2 |
|       |         |               |              |     |            | *Scope:*        |
|       |         |               |              |     |            | 1. Todo X       |
|       |         |               |              |     |            | 2. Todo Y       |
|       |         |               |              |     |            | *Assumptions:*  |
|       |         |               |              |     |            | 1. Prereq. 1    |
|       |         |               |              |     |            | 2. Prereq. 2    |
|       |         |               |              |     |            | *Dependencies:* |
|       |         |               |              |     |            | 1. Team 1       |
|       |         |               |              |     |            | 2. Team 2       |
| PRD 3 | OKR 2   | No            | Yes          | 7   | Commit     | *Key Results:*  |
|       |         |               |              |     |            | 1. Key Result 1 |
|       |         |               |              |     |            | 2. Key Result 2 |
|       |         |               |              |     |            | *Scope:*        |
|       |         |               |              |     |            | 1. Todo X       |
|       |         |               |              |     |            | 2. Todo Y       |
|       |         |               |              |     |            | *Assumptions:*  |
|       |         |               |              |     |            | 1. Prereq. 1    |
|       |         |               |              |     |            | 2. Prereq. 2    |
|       |         |               |              |     |            | *Dependencies:* |
|       |         |               |              |     |            | 1. Team 1       |
|       |         |               |              |     |            | 2. Team 2       |


## Commit/No-Commit Meeting

A critical "commit/no-commit" meeting is held with the Product Team Managers (TPMs) to:

* Review Team Capacity: Assess available team bandwidth, considering factors like planned vacations, potential roadblocks, and the complexity of proposed work.
* Prioritize OKRs: Prioritize OKRs based on team capacity, LOE estimates, and identified risks. 
* Align Expectations: Ensure alignment between the team's commitments and the overall business objectives.

### Conclusion

The estimation and planning process is an iterative one. Continuous communication, regular check-ins, and a proactive approach to addressing challenges are crucial for successful execution. By adhering to this structured process, the engineering team can effectively align with company goals, deliver high-quality work, and achieve desired outcomes.

See also:
- [Capacity Planning]({{< relref "/management/capacity-planning" >}})
- The orinial blog post [Week 3 of the year 2025]({{< relref "/posts/week-2025-03" >}})
