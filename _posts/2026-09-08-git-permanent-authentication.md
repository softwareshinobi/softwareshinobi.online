layout: post
title: "How to Permanently Stop Git From Asking for Passwords"
author: softwareshinobi
categories: [ Git, Linux ]
tags: [ Git, SSH, Security, Red Hat, DevOps ]
image: assets/images/template.jpg

When Git repeatedly prompts for a password on remote operations, it is usually because the repository is configured to use HTTPS instead of SSH, or because no persistent credential store is configured.

To permanently resolve this without relying on temporary credential caching, transition to SSH authentication using key pairs or use Git's standard storage backend.

### Option 1: Switch Remote URL to SSH (Recommended)

Using SSH keys eliminates interactive password prompts entirely for repository operations.

1. Generate an SSH key pair on your machine if you do not already have one:

```bash
ssh-keygen -t ed25519 -C "admin@enterprise.local"

```

2. Display your public key and add it to your Git host (GitHub, GitLab, or self-hosted Git server):

```bash
cat ~/.ssh/id_ed25519.pub

```

3. Check your current remote URL:

```bash
git remote -v

```

4. Change the remote URL from HTTPS (`https://...`) to SSH (`git@...`):

```bash
git remote set-url origin git@github.com:username/repository.git

```

Verify authentication works without prompting:

```bash
ssh -T git@github.com

```

---

### Option 2: Configure Git Store Helper (For HTTPS)

If you must continue using HTTPS instead of SSH, configure Git to use the persistent `store` credential helper. This saves your credentials in unencrypted plain text in your home directory (`~/.git-credentials`).

1. Enable the persistent store helper globally:

```bash
git config --global credential.helper store

```

2. Run a Git operation to prompt for credentials one last time:

```bash
git pull

```

Verify that credentials were saved permanently:

```bash
cat ~/.git-credentials

```