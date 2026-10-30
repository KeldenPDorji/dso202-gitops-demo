# dso202-gitops-demo

The GitOps configuration repository for **DSO202 Practical 4 (GitOps with Argo CD)**.

It holds only Kubernetes manifests, no application code. Argo CD v3.5.6, running inside a kind cluster, pulled this repository and kept the cluster equal to it.

## Contents

| File | Object |
| --- | --- |
| `manifests/deployment.yaml` | Deployment `webapp-deploy`: `nginxdemos/hello:plain-text`, 4 replicas |
| `manifests/service.yaml` | Service `webapp-svc`: ClusterIP, port 80 |

The Argo CD `Application` that points here (`path: manifests`, automated sync with `prune` and `selfHeal`) is kept outside this repository, in the practicals repository at `dso202-practical-04/argocd/argocd-app.yaml`.

## History as audit trail

Every change to the workload was made by a commit here, never by `kubectl`:

| Commit | Change | Argo CD result |
| --- | --- | --- |
| `7982284` | Initial deployment with 2 replicas | Namespace `demo-app` created, 2 Pods |
| `5a2467b` | Scale webapp to 4 replicas | Scaled 2 → 4 |
| `17ea9c5` | Remove webapp-svc | Service **pruned** from the cluster |
| `fb50266` | Revert "Remove webapp-svc" | Service re-created |

The full report and screenshots are in [KeldenPDorji-AS2026DSO202_Practicals / dso202-practical-04](https://github.com/KeldenPDorji/KeldenPDorji-AS2026DSO202_Practicals/tree/main/dso202-practical-04).
