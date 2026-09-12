---
layout: post
title: "Understanding Shell Flags: Why Use set -e and set -x in Bash Scripts"
author: softwareshinobi
categories: [ Linux, Bash ]
tags: [ Linux, Bash, Shell-Scripting, DevOps, RHEL ]
image: assets/images/template.jpeg
---

Using `set -e` and `set -x` at the beginning of shell scripts introduces strict execution safety and real-time debugging capabilities into automated Linux workflows.

### Why Use `set -e` and `set -x`

* **`set -e` (Exit Immediately on Error):** Forces the script to terminate instantly if any command exits with a non-zero (failure) status. This prevents cascading errors—such as running a destructive cleanup command when a prior directory-creation or download step fails.
* **`set -x` (Print Commands / Execution Tracing):** Prints each command and its evaluated arguments to `stderr` prior to execution. This offers full transparency into script runtime, showing exact variable expansions and control flow.

---

### How to Check Flag Status Within a Script

To check if these options are currently active inside a running script, inspect the `$-` special variable (which holds active shell flag options) or evaluate the option status using `[[ $- =~ ... ]]`.

#### Method 1: Inspect Active Shell Flags via `$-`

Print all active option flags directly to output:

```bash
#!/bin/bash
set -e
set -x

# Print active flags (e.g., outputs "himBHs" or flags containing 'e' and 'x')
echo "Active shell flags: $-"

```

#### Method 2: Programmatic Check Inside Script

Check flags conditionally and display clean output:

```bash
#!/bin/bash
set -e
set -x

# Check if 'e' option is enabled
if [[ $- == *e* ]]; then
    echo "set -e is ENABLED"
else
    echo "set -e is DISABLED"
fi

# Check if 'x' option is enabled
if [[ $- == *x* ]]; then
    echo "set -x is ENABLED"
else
    echo "set -x is DISABLED"
fi

```

#### Method 3: Use Shell Built-in `shopt` / `set -o`

Inspect flag states using `set -o`:

```bash
#!/bin/bash
set -e
set -x

# Display status of errexit (-e) and xtrace (-x)
set -o | grep -E 'errexit|xtrace'

```

##### Example Output

```text
errexit         on
xtrace          on

```
