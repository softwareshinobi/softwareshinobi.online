---
layout: post
title: "Ollama Docker Compose"
author: softwareshinobi
categories: [ Jekyll, tutorial ]
tags: [ Docker, Ollama, AI, LLM, Containerization ]
image: assets/images/template.jpeg
---

```yaml
services:
  ollama:
    image: ollama/ollama:latest
    container_name: ollama
    restart: unless-stopped
    volumes:
      - ./ollama/ollama:/root/.ollama
    environment:
      - OLLAMA_KEEP_ALIVE=24h

  ollama-webui:
    image: ghcr.io/open-webui/open-webui:main
    container_name: ollama-webui
    restart: unless-stopped
    ports:
      - "8080:8080"
    volumes:
      - ./ollama/ollama-webui:/app/backend/data
    environment:
      - OLLAMA_BASE_URL=http://ollama:11434
      - WEBUI_AUTH=False
    depends_on:
      - ollama

```

### Pulling and Managing Models

Pull the Llama 3.2 model:

```bash
docker exec -it ollama ollama pull llama3.2

```

Pull the Qwen 3 model:

```bash
docker exec -it ollama ollama pull qwen3:0.6b

```

Run the model interactively:

```bash
docker exec -it ollama ollama run qwen3:0.6b

```

List installed models:

```bash
docker exec -it ollama ollama list

```

Exit the interactive chat:

```text
/bye

```

Delete heavier models to free up resources:

```bash
docker exec -it ollama ollama rm llama3.2

```
