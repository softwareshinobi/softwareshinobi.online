---
layout: post
title: "Removing Git Plain-Text Credential Storage over HTTPS"
author: softwareshinobi
categories: [ Linux, Git ]
tags: [ Git, Security, CLI, DevOps, Linux ]
image: assets/images/template.jpeg
---

When Git credential storage is no longer required or if plain-text password files violate local security policies, you can disable the credential helper and remove stored authentication files.

<Steps>
  <Step title="Unset Credential Helper" subtitle="Global Config">
    Remove the global credential store configuration to prevent Git from writing or requesting stored credentials:

    ```bash
    git config --global --unset credential.helper
    ```

    To verify that the configuration step was successful, run `git config --global --get credential.helper`. The command should return an empty output.
  </Step>

  <Step title="Delete Stored Credentials" subtitle="File Removal">
    Delete the plain-text file where Git stored your unencrypted credentials:

    ```bash
    rm -f ~/.git-credentials
    ```

    To verify that the removal was successful, run `ls ~/.git-credentials`. The output should state `No such file or directory`.
  </Step>
</Steps>
