# POC. Create cluster and config ArgoCD

### For Demo use GitHub Codespaces project.
[https://github.com/features/codespaces]()

### Install k3d
```bash
curl -s https://raw.githubusercontent.com/k3d-io/k3d/main/install.sh | bash
```

### Create cluster for 1 master node and 3 agents
```bash
k3d cluster create demo --agents 3
```

### Install AgroCD
```bash
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

### Port forwarding
```bash
kubectl port-forward svc/argocd-server -n argocd 8080:443
```

### Get initial admin ArgoCD password
```
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo
```

Go to https://127.0.0.1:8080 with accept self-signed SSL certificate.

For GitHub Codespaces GUI users. Use automatically generated link in "ports" tab ([with using HTTP forwarding](https://docs.github.com/en/codespaces/developing-in-a-codespace/forwarding-ports-in-your-codespace#using-https-forwarding)),
ex.: https://animated-telegram-9wp74ww7637q5x-8080.app.github.dev/...

```text
Login: admin
Password: _from previous step_
```

#### Keep your eys! Enable dark them in Settings / Appearance
