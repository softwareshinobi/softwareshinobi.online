---
layout: post
title:  "ollama Docker compose"
author: sal
categories: [ Jekyll, tutorial ]
image: assets/images/12.jpg
featured: true
hidden: true
---

services:
  ollama:
    image: ollama/ollama:latest
    container_name: ollama
    restart: unless-stopped
    ports:
      - "11434:11434"
    volumes:
      - ollama:/root/.ollama

volumes:
  ollama:





docker exec -it ollama ollama pull llama3.2
