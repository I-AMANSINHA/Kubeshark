<H1> AWX (Ansible Automation Controller) environment from scratch on Minikube </H1>
AWX: A web-based enterprise interface and task scheduling engine that centralizes and securely delegates Ansible playbooks across teams, eliminating command-line isolation.

Step-1 : Install the AWX Operator (The Setup Framework)
- kubectl create namespace awx

Step-2 : create custom.yml file for configuration
Step-3 : kubectl apply -k . 
Step-4 : kubectl get pods -n awx 
Step-5 : awx-instance.yaml (actual app)
Step-6 : kubectl apply -f awx-instance.yaml 
Step-7 : kubectl get pods -n awx -w
Step-8 : Extract Your Decoded Admin Password 
- kubectl get secret my-awx-admin-password -n awx -o jsonpath="{.data.password}" | base64 --decode; echo
Step-9 : Launch and Log in to the Console
- minikube service my-awx-service -n awx

####### installation through helm ############

- curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
- chmod +x get_helm.sh
- ./get_helm.sh

- helm repo add awx-operator https://ansible-community.github.io/awx-operator-helm/
- helm repo update
- helm install ansible-awx-operator awx-operator/awx-operator -n awx --create-namespace
- kubectl get pods -n awx
- create your application definition file named awx-instance.yaml
- kubectl apply -f awx-instance.yaml
- kubectl get pods -n awx -w
- The PostgreSQL database instance is created automatically by default by the AWX Operator
- kubectl get secret my-awx-admin-password -n awx -o jsonpath="{.data.password}" | base64 --decode; echo
- minikube service my-awx-service -n awx
- by default - 31926 uses


- 
