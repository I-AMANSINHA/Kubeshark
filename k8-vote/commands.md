<h1> Prometheus & Grafana </h1>

Prometheus - for monitoring, metrics and logging

Grafana - visualisation

Helm = Prometheus + Grafana

Kind - kubernetes in docker

ArgoCD - get manifest file from github and deploy on node, GitOps

Kind forces everything into Docker containers. A cluster node is literally just a container running on your machine.

Minikube traditionally creates a whole Virtual Machine (VM) via VirtualBox, VMware, or Hyper-V, and runs Kubernetes inside that isolated operating system.

Kind is like a disposable cup. It is built to start instantly, run an automated test in a CI/CD pipeline, and be deleted immediately.

nodePort: 31001 ➔ External Port (The outside world uses this) (localhost)

port: 5001 ➔ Service Port (Internal cluster apps use this) (Kubernetes Service)

targetPort: 80 ➔ Container Port (The actual code application uses this) (Your App Code)

Prometheus - time/series database

Helm - k8s package manager

Get Grafana 'admin' user password by running

nodeExporter - tool to get the data from the nodes

Prometheus query :- 

{to check the cpu usage}

sum (rate (container_cpu_usage_seconds_total{namespace="default"}[1m])) / sum (machine_cpu_cores) * 100
{memory-check}


sum (container_memory_usage_bytes{namespace="default"}) by (pod)

{network-check}

sum(rate(container_network_receive_bytes_total{namespace="default"}[5m])) by (pod)

sum(rate(container_network_transmit_bytes_total{namespace="default"}[5m])) by (pod)


Grafana - http://0.0.0.0:31000/ , user - admin, pass - prom-operator

Prometheus - http://0.0.0.0:9099/

Vote-app - http://0.0.0.0:500/


Commands: -
1. kind create cluster
2. kind get clusters
kind export kubeconfig --name kind
kubectl config get-contexts
kubectl get nodes
kind delete cluster
kind create cluster --config config.yml
kubectl config use-context kind-dev-env (if you have multiple clusters)
kubectl apply -f .
kubectl get all
helm repo list
helm repo update
kubectl create namespace monitoring
kubectl --namespace monitoring get pods
kubectl port-forward svc/kind-prometheus-kube-prome-prometheus -n monitoring 9099:9090 --address=0.0.0.0 &
kubectl port-forward svc/kind-prometheus-grafana -n monitoring 31000:80 --address=0.0.0.0 &
kubectl port-forward svc/vote 500:5000 --address=0.0.0.0 &
kubectl logs deployment/name
kubectl delete -f old-filename.yaml 
(If you have old, incorrect duplicate files in that directory, make sure to delete them from your folder first)
docker stop $(docker ps -q --filter label=io.x-k8s.kind.cluster)
docker start $(docker ps -a -q --filter label=io.x-k8s.kind.cluster)
helm install kind-prometheus prometheus-community/kube-prometheus-stack --namespace monitoring --set prometheus.service.nodePort=30000 --set prometheus.service.type=NodePort --set grafana.service.nodePort=31000 --set grafana.service.type=NodePort --set alertmanager.service.nodePort=32000 --set alertmanager.service.type=NodePort --set prometheus-node-exporter.service.nodePort=32001 --set prometheus-node-exporter.service.type=NodePort
kubectl --namespace monitoring get secrets kind-prometheus-grafana -o jsonpath="{.data.admin-password}" | base64 -d ; echo
kubectl get secret --namespace monitoring -l app.kubernetes.io/component=admin-secret -o jsonpath="{.items[0].data.admin-password}" | base64 --decode ; echo
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo add stable https://charts.helm.sh/stable
helm upgrade <YOUR-RELEASE-NAME> grafana/grafana -f grafana-pass.yaml -n <YOUR-NAMESPACE>



