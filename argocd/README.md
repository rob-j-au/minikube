## ArgoCD


### Installation

```
kubectl create namespace argocd
```

```
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

```
kubectl patch svc argocd-server -n argocd \
  -p '{"spec": {"type": "NodePort"}}'
```

```
kubectl get svc argocd-server -n argocd
```


```
kubectl get secret argocd-initial-admin-secret -n argocd -o jsonpath="{.data.password}" | base64 -d
```


Web Interface

```
minikube service argocd-server -n argocd
```

Client

```
brew install argocd
argocd login localhost:50254
```


### Deploy

```
argocd app create guestbook \
  --repo https://github.com/argoproj/argocd-example-apps.git \
  --path guestbook \
  --dest-server https://kubernetes.default.svc \
  --dest-namespace default
```

Sync the App
```
argocd app sync guestbook
```

Check the App Status
```
argocd app get guestbook
```

Access the App

```
minikube kubectl port-forward svc/guestbook-ui 8080:80
```