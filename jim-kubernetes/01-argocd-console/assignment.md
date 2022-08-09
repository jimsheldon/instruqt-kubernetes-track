---
slug: argocd-console
id: 7t91utsiltpg
type: challenge
title: Access ArgoCD Console
teaser: Everything starts with ArgoCD
notes:
- type: text
  contents: |-
    This track will get you started with ArgoCD.

    ## Objectives

    In this track, this is what you'll learn:
    - How to login to ArgoCD using the CLI and console
    - How to deploy Gitea using ArgoCD
tabs:
- title: Shell
  type: terminal
  hostname: kubernetes-vm
- title: ArgoCD
  type: service
  hostname: kubernetes-vm
  path: /
  port: 30080
difficulty: basic
timelimit: 600
---
ArgoCD CLI
===========

ArgoCD creates a default password for the `admin` user that you can retrieve with this command:

```
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo
```

Login to ArgoCD with this command, enter the password when prompted:

```
argocd login localhost:30080 --username admin --insecure
```

ArgoCD Console
===============

The ArgoCD console is running in the tab named "ArgoCD".

Open the tab and login as the `admin` user.

🏁 Finish
=========

To complete this challenge, press **Check**.
