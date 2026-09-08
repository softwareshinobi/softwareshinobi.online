---

## layout: post
title: "Installing Zip Utilities and Managing Archive Compression on Enterprise Linux"
author: softwareshinobi
categories: [ Linux, Administration ]
tags: [ RHEL, Bash, System-Administration, Compression, Enterprise-Linux ]
image: assets/images/template.jpeg
---

When managing compressed archives on enterprise RHEL-based systems, install the standard `zip` and `unzip` package utilities via `yum` or `dnf` to handle compression and extraction operations.

### Installation

Install both the compression and extraction utilities from default system repositories:

```bash
sudo yum install zip unzip -y

```

---

### File Compression (Creating Archives)

#### 1. Compress a Single File

Create a compressed archive containing a single file:

```bash
zip archive_name.zip file1.txt

```

#### 2. Compress Multiple Files

Combine multiple discrete files into a single ZIP archive:

```bash
zip archive_name.zip file1.txt file2.txt file3.txt

```

#### 3. Compress a Directory Recursively

Use the `-r` flag to traverse and include all contents, subdirectories, and hidden files within a directory:

```bash
zip -r archive_name.zip /path/to/directory/

```

---

### File Extraction (Uncompressing Archives)

#### 1. Extract Archives to the Current Directory

Uncompress the contents of a ZIP file directly into the current working directory:

```bash
unzip archive_name.zip

```

#### 2. Extract Archives to a Specific Destination

Extract files into a target target directory using the `-d` option:

```bash
unzip archive_name.zip -d /path/to/destination/

```

#### 3. Inspect Archive Contents Without Unzipping

List all files contained within an archive before extraction using the `-l` flag:

```bash
unzip -l archive_name.zip

```
