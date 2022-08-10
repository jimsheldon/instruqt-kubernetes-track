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
- title: Drone
  type: service
  hostname: kubernetes-vm
  path: /
  port: 30980
  new_window: true
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

Create Gitea Resources
=======================

This will create your Gitea user and Oauth app.

```
kubectl create -f gitea-helper.yaml
```

Verify that the secret was created.

```
kubectl -n drone get secret
```

Open Gitea
===========

Open the 'Gitea' tab and login as `user-01` with password `user-01@123`.

Install Drone
==============

```
argocd app create drone --repo "https://charts.drone.io" --helm-chart drone --dest-namespace drone --dest-server "https://kubernetes.default.svc" --sync-policy auto --values-literal-file drone-values.yaml --revision 0.5.0
```

Install Drone Docker Runner
============================

```
argocd app create drone-runner-docker --repo "https://charts.drone.io" --helm-chart drone-runner-docker --dest-namespace drone --dest-server "https://kubernetes.default.svc" --sync-policy auto --values-literal-file drone-runner-docker-values.yaml --revision 0.1.0
```

Open Drone
===========

Click the 'Drone' tab above.


