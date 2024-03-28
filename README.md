# p7-8

Group Member: Hong

Source for demo app: https://github.com/tastejs/todomvc  

# Diagram
![Cloud Architecture (1)](https://github.com/developingcow/p7-8/assets/155276353/158ecdca-879e-4883-bba2-e842ef0a4f21)


# Setup
Prereq: Helm, aws cli, kubectl
## EKS Cluster
1. `eksctl create cluster --name test --region us-east-1 --nodegroup-name testng --node-type t3.medium --nodes 2 --nodes-min 2 --nodes-max 2`
2. `kubectl apply -f deploy.yaml`
3. `kubectl expose deployment todo --type=LoadBalancer --name=todo --port 80 --target-port=80`
4. You should then be able to reach the app using the url for load balancer created on AWS, `kubectl describe svc` for url


## Observability
1. `kubectl create namespace monitoring`
2. `helm install monitoring prometheus-community/kube-prometheus-stack -n monitoring`
3. `kubectl config set-context --current --namespace=monitoring`
4. `kubectl port-forward service/monitoring-grafana 8080:80 -n monitoring`
5. You should be able to open up grafana with default credentials (admin, prom-operator)

# Tear down
`eksctl delete cluster --name <name>`
