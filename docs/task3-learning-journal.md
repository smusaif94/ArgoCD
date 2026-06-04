# Task 3 Learning Journal: ArgoCD Core Install + First Application

This document captures my hands-on progress for **ArgoCD core installation** and my first GitOps-managed application.

## What I built

- Installed ArgoCD in local Kubernetes using Helm
- Logged into ArgoCD CLI and rotated the admin password
- Connected my Git repo and deployed a Helm chart as an ArgoCD Application
- Enabled automated sync, prune, self-heal, and namespace auto-create
- Verified Git change detection by changing `replicaCount` from `2` to `4`

## Commands used (summary)

```bash
helm repo add argo https://argoproj.github.io/argo-helm
helm install argocd argo/argo-cd -n argocd --create-namespace \
  --set server.service.type=NodePort \
  --set server.insecure=true

kubectl get pods -n argocd
kubectl get secret argocd-initial-admin-secret -n argocd -o jsonpath="{.data.password}" | base64 -d

argocd login localhost:<nodeport> --insecure
argocd account update-password

argocd app sync demo-nginx
```

## Required manifests

- `manifests/task3/appproject-poc-demo.yaml`
- `manifests/task3/application-demo-nginx.yaml`

## Screenshot Checklist (replace with your own files)

- [ ] ArgoCD UI: Application **Synced + Healthy**
- [ ] ArgoCD resource tree
- [ ] ArgoCD app diff
- [ ] Terminal output: install/login/sync validation

Example markdown image links:

```markdown
![Synced and Healthy](images/argocd-synced-healthy.png)
![Resource tree](images/argocd-resource-tree.png)
![App diff](images/argocd-app-diff.png)
```

## Challenges I faced and how I solved them

1. **NodePort not reachable initially**
   - Rechecked service type and NodePort using `kubectl get svc -n argocd`.
2. **Initial login failed because of wrong port/password copy**
   - Decoded the secret again and used exact NodePort value.
3. **App was OutOfSync for a while**
   - Checked repo URL/path and then used `argocd app sync demo-nginx` for immediate reconciliation.

## LinkedIn post draft (human tone)

Today I completed a practical GitOps milestone with **ArgoCD** 🎯

✅ Installed ArgoCD on a local Kubernetes cluster using Helm  
✅ Created AppProject + Application manifests  
✅ Enabled auto-sync, prune, self-heal, and namespace auto-create  
✅ Pushed a Git change (`replicaCount: 4`) and watched ArgoCD reconcile automatically  

Big learning: GitOps really shifts deployment control to Git state + reconciliation loop, which makes operations cleaner and more auditable.

I also learned the practical difference between auto-sync and a manual `argocd app sync` trigger.

#ArgoCD #GitOps #Kubernetes #DevOps #CloudNative #LearningInPublic
