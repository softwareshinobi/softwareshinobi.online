```markdown
---
layout: post
title: "How to Create, Edit, and Execute a Shell Script in Linux"
author: softwareshinobi
categories: [ Linux, Bash ]
tags: [ Linux, Bash, Shell Scripting, CLI, DevOps ]
image: assets/images/template.jpg
---

Creating, configuring permissions, and executing a custom shell script can be accomplished entirely from the command line using standard POSIX utilities[cite: 1].

### 1. Create the Script File
Use `touch` to create an empty script file[cite: 1]:
```bash
touch system_info.sh

```

### 2. Make the Script Executable

Grant execution permissions using `chmod`:

```bash
chmod +x system_info.sh

```

### 3. Write Script Content

Use `cat` to write a script that outputs formatted date, time, and system hostname information:

```bash
cat << 'EOF' > system_info.sh
#!/bin/bash

# Visual Separator
echo "========================================"
echo "          SYSTEM INFORMATION            "
echo "========================================"

# Output System Details
echo " Hostname : $(hostname)"
echo " Date     : $(date '+%Y-%m-%d')"
echo " Time     : $(date '+%H:%M:%S %Z')"

echo "========================================"
EOF

```

### 4. Execute the Script

Run the script directly from the terminal:

```bash
./system_info.sh

```

#### Example Output

```text
========================================
          SYSTEM INFORMATION            
========================================
 Hostname : enterprise-node-01
 Date     : 2026-09-08
 Time     : 18:59:00 EDT
========================================
