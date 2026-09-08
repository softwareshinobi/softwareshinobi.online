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

```

### Init and Service Management: `systemctl` → `systemctl`

Process control is the most seamless transition across both ecosystems. Service management remains completely unchanged—both distributions implement `systemd` natively.

```bash
sudo systemctl status <service_name>
sudo systemctl enable --now <service_name>

```

*(Note: Unlike Ubuntu, which automatically launches services immediately upon package installation, Red Hat family distributions leave newly installed daemons inactive by default until explicitly enabled.)*

### Mandatory Access Control: AppArmor → SELinux

While Ubuntu utilizes AppArmor for security containment, AlmaLinux enforces SELinux strictly out of the box.

When running containerized workloads, localized permission denials on volume mounts or unexpected file lockouts are frequently caused by SELinux context rules holding the access boundary. Managing container storage volumes or system services requires accounting for SELinux security contexts rather than AppArmor profiles.

```

```