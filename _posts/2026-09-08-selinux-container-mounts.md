---
layout: post
title: "Fixing SELinux Permission Denied Errors in Docker Container Volume Mounts"
author: softwareshinobi
categories: [ Docker, Linux ]
tags: [ SELinux, Docker, DevOps, Containers, Security ]
image: assets/images/template.jpeg
---

When binding host paths to containers using flags like `-v /host/path:/container/path`, Security-Enhanced Linux (SELinux) will block access by default to enforce access controls. 

To resolve permission issues, append the appropriate SELinux volume flag to your volume declarations in your `docker-compose.yml`:

* **`:z`** - Relabels the volume content so that it is **shared** across multiple containers.
* **`:Z`** - Relabels the volume content as **private** and unshared, restricting access strictly to a single container.

### Example Configuration

```yaml
version: '3.8'
services:
  app:
    image: my-app-image
    volumes:
      - ./data:/app/data:z
```