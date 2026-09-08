---
layout: post
title: "The Red Hat Exchange Rate: Mapping Ubuntu Habits to AlmaLinux 9"
author: softwareshinobi
categories: [ Jekyll, tutorial ]
tags: [ almalinux, rhel, ubuntu, selinux, linux ]
image: assets/images/template.jpeg
---

If you have been living in Ubuntu land for a while, jumping back into the Red Hat Enterprise Linux (RHEL) ecosystem for enterprise work can feel like speaking a slightly different dialect. While system core concepts remain similar, your day-to-day commands, package delivery, and default security rules require a mental translation layer.

Here is a straightforward reference guide mapping your standard Ubuntu habits directly to Red Hat's ecosystem via AlmaLinux 9.

### Package Management: `apt` / `apt-get` → `dnf`

AlmaLinux 9 relies on `dnf` as its primary package manager, replacing the older `yum` tool. The operational syntax maps directly to what you are used to executing in Debian-based systems:

*   **Installing Packages:** `sudo dnf install <package>`
*   **System Updates:** `sudo dnf update`
*   **Removing Packages:** `sudo dnf remove <package>`

### Software Repositories: PPAs → Official RPM Repositories

Debian and Ubuntu setups often rely on Personal Package Archives (PPAs) added via `add-apt-repository`. AlmaLinux does not use PPAs. Instead, package management utilizes explicit configuration files stored under `/etc/yum.repos.d/`. 

To manage external software sources, point your package manager directly to upstream RPM repositories using the native configuration tool:

```bash
sudo dnf config-manager --add-repo <repository_url>