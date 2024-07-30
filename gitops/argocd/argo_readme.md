# GitOps using ArgoCD

### install
```sh
brew install helm
brew install argocd
```

### repos
```sh
helm repo add argo https://argoproj.github.io/argo-helm
```

### build
```sh
terraform init
terraform apply
```

### configure [manual]
```sh
kubectl patch svc argocd-server -n gitops -p '{"spec": {"type": "LoadBalancer"}}'
kubectl get svc argocd-server -n gitops
kubectl -n gitops get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo


argocd login "4.152.158.35" --username admin --password "z7TJxhqWcEXFbheP0oK2puPXXxSYgyEV" --insecure
argocd login "4.152.158.35" --username admin --password "WlhsGOAY8TvxXk3s" --insecure

argocd cluster add orion-development

kubectl apply -f git-repo-con.yaml -n gitops
```

