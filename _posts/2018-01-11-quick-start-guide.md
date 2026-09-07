---
layout: post
title:  "ollama Docker compose"
author: sal
categories: [ Jekyll, tutorial ]
image: assets/images/12.jpg
featured: true
hidden: true
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



docker exec -it ollama ollama pull llama3.2




#####

```bash
docker exec -it ollama ollama pull qwen3:0.6b
```

Run it interactively:

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

And if you want to delete the heavier Llama model afterward:

```bash
docker exec -it ollama ollama rm llama3.2
```

