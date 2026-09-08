---
layout: post
title: "RHEL REVOLUTIONS: Modernizing Enterprise Infrastructure with Official Docker Binaries"
author: softwareshinobi
categories: [ Jekyll, tutorial ]
tags: [ docker, almalinux, devops, linux, containers ]
image: assets/images/template.jpeg
---

Deploying Docker on enterprise-grade Linux distributions like AlmaLinux 9 requires a slightly different approach than Ubuntu-based environments. Because AlmaLinux ships with Podman as its default container engine and defaults service daemons to an inactive state upon installation, setting up Docker Engine and Docker Compose v2 requires a clean environment prep and specific configuration steps.

Here is the complete step-by-step guide to clearing out conflicting software, configuring upstream repositories, installing Docker components, and configuring user permissions.

### 1. Clean Up Conflicting Packages

AlmaLinux pushes Podman by default. If Podman, Buildah, or older Docker packages are present, remove them to prevent runtime and resource conflicts:

```bash
sudo dnf remove -y podman buildah docker docker-client docker-client-latest docker-common docker-latest docker-latest-logrotate docker-logrotate docker-engine

```

### 2. Add the Official Docker Repository

Install the `dnf-plugins-core` package to manage your repositories, then point your package manager directly to the upstream Docker Community Edition repository:

```bash
sudo dnf install -y dnf-plugins-core
sudo dnf config-manager --add-repo [https://download.docker.com/linux/centos/docker-ce.repo](https://download.docker.com/linux/centos/docker-ce.repo)

```

### 3. Install Docker Engine and Docker Compose

Fetch the core Docker engine binaries alongside the modern Compose v2 plugin directly through `dnf`:

```bash
sudo dnf install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

```

### 4. Enable and Start the Docker Daemon

Unlike Debian/Ubuntu systems—which automatically launch services upon installation—Red Hat family distributions leave newly installed services disabled. Enable the service to start at boot and initialize it immediately:

```bash
sudo systemctl enable --now docker

```

### 5. Grant User Privileges (Optional)

To run container commands without prepending `sudo`, add your current user to the `docker` system group and apply the new group settings:

```bash
sudo usermod -aG docker $USER
newgrp docker

```

### 6. Verify Docker Compose Installation

Confirm that Docker Compose v2 is properly configured and operational:

```bash
docker compose version

```

```[cite: 2, 3]

```
