---
slug: install-gitea
id: bxrkdtwemrc4
type: challenge
title: Install Gitea
teaser: Install Gitea
notes:
- type: text
  contents: Now that you have access to the ArgoCD cluster, deploy Gitea.
tabs:
- title: Shell
  type: terminal
  hostname: kubernetes-vm
- title: ArgoCD
  type: service
  hostname: kubernetes-vm
  path: /
  port: 30080
- title: Gitea
  type: service
  hostname: kubernetes-vm
  path: /
  port: 30950
difficulty: basic
timelimit: 600
---

Install Gitea
==============

Install Gitea

```
argocd app create gitea --repo "https://dl.gitea.io/charts/" --helm-chart gitea --dest-namespace default --dest-server https://kubernetes.default.svc  --sync-policy auto  --values-literal-file gitea-values.yaml --revision 5.0.9
```

Wait for this command to return 'Running' status:

```
kubectl -n default get pod gitea-0
```

Open Gitea
===========

Open the 'Gitea' tab and login.