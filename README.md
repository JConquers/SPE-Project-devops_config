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
## Logging

Create namespace "logging": ```kubectl create ns logging```

```
kubectl apply -f observability/elasticsearch-deployment.yaml -n logging

kubectl apply -f observability/kibana-deployment.yaml -n logging

kubectl apply -f observability/filebeat-rbac.yaml -n logging
kubectl apply -f observability/filebeat-configmap.yaml -n logging
kubectl apply -f observability/filebeat-daemonset.yaml -n logging


# Port forwading necessary ClusterIP services
kubectl -n logging port-forward svc/elasticsearch 9200:9200
kubectl -n logging port-forward svc/kibana 5601:5601


```