## Starter:
On start of machine(single node k8s cluster) run:

```
minikube start --driver=docker
minikube enable addons ingress
minikube enable addons metrics-server

kubectl apply -f namespaces/
kubectl apply -f backend/
kubectl apply -f frontend/
kubectl apply -f ingress/

```

### For frontend to access base url(backend url) = 127.0.0.1:8000
 
```
kubectl port-forward svc/backend-service 8000:8000 -n dev
```
