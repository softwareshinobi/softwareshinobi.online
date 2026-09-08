---
layout: post
title: "Why You Shouldn't Add SELinux Volume Flags to Every Docker Compose File"
author: softwareshinobi
categories: [ Docker, DevOps ]
tags: [ Docker, SELinux, DevOps, Linux, Containers ]
image: assets/images/2026-09-08-docker-selinux-mount-flags.jpg
---

No. Do not slap `:z` or `:Z` on every volume flag like a careless amateur. Every line in a config file costs time to maintain, and adding parameters without understanding their function is a liability.

### The Strict Rule of Mount Flags

* **Non-SELinux Systems (Ubuntu, Debian, macOS, Windows):** The `:z` and `:Z` flags are completely ignored by the Docker daemon. They cause no harm, but they are dead weight.
* **SELinux Systems (AlmaLinux, RHEL, Fedora, Rocky):** The flags actively modify the file label on the host filesystem.

### Why Blanket Bolding the Flag Is Dangerous

The `:z` and `:Z` options do not just grant permissions; they run `chcon` behind the scenes to relabel the host path to `container_file_t`.

* **`:z` (Shared):** Relabels the host directory so multiple containers can access it.
* **`:Z` (Private/Unshared):** Relabels the host directory with a unique private label. **Warning:** If you use `:Z` on a system directory (like `/var/log` or `/etc`), SELinux will relabel that system folder for the container, which can instantly break host processes trying to access it.

### How to Handle Portability Cleanly

If you write `docker-compose.yml` files that must run across both Ubuntu (no SELinux) and AlmaLinux (SELinux enforced), choose one of these strategies:

#### Named Volumes Over Bind Mounts (Recommended)
If you use Docker managed volumes instead of host bind mounts (`./data:/app/data`), Docker manages the SELinux labeling automatically. You do not need to append anything.

```yaml
services:
  db:
    image: postgres
    volumes:
      - pgdata:/var/lib/postgresql/data # No :z needed

volumes:
  pgdata:

```

#### Bind Mounts for Local/Cross-Platform Dev

If you are developing locally on Ubuntu and pushing to a non-SELinux production server, omit the flags entirely.

#### Bind Mounts Targeting Enterprise Linux

If the target environment is explicitly AlmaLinux/RHEL and you must use host bind mounts, use `:z` for shared directories and `:Z` only for dedicated, isolated container storage directories.
