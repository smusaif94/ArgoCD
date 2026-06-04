# ArgoCD

This repository documents a **Task 3 GitOps learning implementation**:

- ArgoCD core install on local cluster (Helm)
- First managed ArgoCD Application using a Helm chart
- Validation of Git → ArgoCD → Kubernetes sync loop

## Task 3 deliverables in this repo

- AppProject manifest: `/manifests/task3/appproject-poc-demo.yaml`
- Application manifest: `/manifests/task3/application-demo-nginx.yaml`
- Learning write-up + screenshot checklist: `/docs/task3-learning-journal.md`

## Quick explanation (in simple words)

- **Sync**: ArgoCD continuously compares Git desired state with live cluster state.
- **Prune**: If something is removed from Git, ArgoCD removes it from the cluster.
- **Self-heal**: If someone changes live resources manually, ArgoCD brings them back to the Git version.

## Pull-based vs push-based CI/CD

- **Push-based**: CI/CD pipeline pushes deployments directly into the cluster.
- **Pull-based (GitOps)**: Agent/controller (ArgoCD) pulls desired state from Git and reconciles cluster.

Why pull-based helps:

- Single source of truth in Git
- Better audit trail
- Safer rollback/recovery

## Core ArgoCD components used

- **argocd-server**: UI + API server
- **argocd-repo-server**: fetches manifests from Git and Helm/Kustomize sources
- **argocd-application-controller**: compares desired vs live state and performs reconciliation

## Notes

Replace placeholder repo URL and Helm chart path in the manifests before applying in your own cluster.
