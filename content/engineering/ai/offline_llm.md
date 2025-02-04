+++
title = 'Offline LLM Inferencing'
date = '2025-02-02T18:26:12-08:00'
draft = true
+++

Offline LLM Inferencing:

1. Ollama
2. Llamafile
   * Executable Linkable Format (ELF)
3. Jan
4. LM Studio 
5. LLaMa.cpp
6. GPT4All

See also
1. The great article on the subject https://getstream.io/blog/best-local-llm-tools/
2. https://getstream.io/blog/local-deepseek-r1/


## Ollama

Ollama
1. Repo https://github.com/ollama/ollama
2. Docs https://github.com/ollama/ollama/blob/main/docs/README.md
3. Model library https://ollama.com/search
4. HuggingFace models https://huggingface.co/models?other=llama

Ollama model CRUD:

```bash
ollama list
ollama show <model>

ollama pull <model>
ollama create <model> -f ./Modelfile

ollama run <model>
ollama serve        # start the server, then ollama run <model>
ollama ps
ollama stop <model>

ollama rm <model>
ollama cp <model> <copy>

# Multiline """
# ...
# """

# Multimodal
ollama run llava "What's in this image? <path>"

# Prompt as an argument
ollama run llama3.2 "Summarize this file: $(cat <file>)"
```

Ollama service control:

```bash
sudo systemctl start ollama
sudo systemctl status ollama
sudo systemctl edit ollama

journalctl -e -u ollama

sudo systemctl stop ollama
sudo systemctl disable ollama
sudo rm /etc/systemd/system/ollama.service
```

### GGUF

GPT-Generated Unified Format ([GGUF](https://github.com/ollama/ollama?tab=readme-ov-file#import-from-gguf)) - file format that stores large language models (LLMs) for inference.

[Modelfile](https://github.com/ollama/ollama/blob/main/docs/modelfile.md) analog to a dockerfile.

```Modelfile
FROM ./vicuna-33b.Q4_0.gguf
PARAMETER temperature 1
SYSTEM """
You are Mario from Super Mario Bros. Answer as Mario, the assistant, only.
"""
```

```bash
ollama create example -f Modelfile
ollama run example
```

### DeepSeek-coder

https://ollama.com/library/deepseek-coder

```
ollama run deepseek-coder
```



