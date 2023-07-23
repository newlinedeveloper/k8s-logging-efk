# k8s-fluentd
Kubernetes logging mechanism using EFK (Elastic search, Kibana and Fluentd)

#### Prerequisites

- Docker setup: https://docs.docker.com/engine/install/
- Kubectl installation: https://kubernetes.io/docs/tasks/tools/
- Minikube setup : https://minikube.sigs.k8s.io/docs/start/
- helm setup  - https://helm.sh/docs/intro/install/

```
docker version

kubectl version

minikube version

helm version

minikube start
```

### Implementation

```
kubectl create namespace dapr-monitoring

helm repo add elastic https://helm.elastic.co
helm repo update


helm install elasticsearch elastic/elasticsearch --version 7.17.3 -n dapr-monitoring --set replicas=1


helm install elasticsearch elastic/elasticsearch --version 7.17.3 -n dapr-monitoring --set persistence.enabled=false,replicas=1

helm list -n dapr-monitoring

kubectl get pods -n dapr-monitoring

kubectl get svc -n dapr-monitoring


helm install kibana elastic/kibana --version 7.17.3 -n dapr-monitoring


kubectl get pods -n dapr-monitoring


kubectl apply -f ./fluentd-config-map.yaml
kubectl apply -f ./fluentd-dapr-with-rbac.yaml


kubectl get pods -n kube-system -w


helm repo add dapr https://dapr.github.io/helm-charts/
helm repo update
helm install dapr dapr/dapr --namespace dapr-monitoring --set global.logAsJson=true


kubectl port-forward svc/kibana-kibana 5601 -n dapr-monitoring
```



### Delete all the resources


```
kubectl delete -f fluentd-config-map.yaml

kubectl delete -f fluentd-dapr-with-rbac.yaml

helm list -n dapr-monitoring

```
