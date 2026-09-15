---
layout: post
title:  "Remove Git Credential Storage"
author: softwareshinobi
categories: [ Jekyll, tutorial ]
image: assets/images/15.jpg
---
Option 2: Remove Git Credential Storage (For HTTPS)If you enabled credential.helper store, remove the setting and delete any stored plain-text passwords.1.Unset Credential Helper:Remove the global credential store configuration:Bashgit config --global --unset credential.helper
2.Delete Stored Credentials:Remove the plain-text file where Git saved your password:Bashrm -f ~/.git-credentials
3.Verify Removal:Run git config --global --get credential.helper to confirm it returns empty.to mere outlines, as evidenced in a beautiful 2014 version of the same Little Red Riding Hood story. 
