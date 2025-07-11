# Install Litmus using kubectl
Reference Documentation: 
    https://docs.litmuschaos.io/docs/getting-started/installation#prerequisites


# 1. Install LitmusChaos via Helm  

    helm repo add litmuschaos https://litmuschaos.github.io/litmus-helm/
    helm repo list
    kubectl create ns litmus
    helm upgrade --install chaos litmuschaos/litmus --namespace=litmus --set portal.frontend.service.type=NodePort -f litmus_values.yaml


# 2. Verify your installation  

    kubectl get pods -n litmus
    kubectl get svc -n litmus
    kubectl port-forward svc/litmusportal-frontend-service 9091:9091

    Login the Litmus GUI Portal 
    id: admin
    pass: litmus

# 3. Install the application  

    cd python_app
    kubectl apply -f .

# 4. Add the Minikube Environment in Litmus GUI  

Click on Environments
Add New Environment
Give a name and save it

    kubectl apply -f nonprod-litmus-chaos-enable.yml

# 5. Add the Chaos Experiments in Litmus GUI  

# 6. Verify the details on Cluster and in Litmus GUI  

# 7. Add Chaos Exporter for Metrics and monitor the same in Grafana

    git clone https://github.com/litmuschaos/litmus.git
    cd litmus/monitoring
    kubectl -n litmus apply -f utils/metrics-exporters/litmus-metrics/chaos-exporter/
    kubectl create ns monitoring
    helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
    helm repo update
    helm upgrade --install grafana prometheus-community/kube-prometheus-stack --namespace monitoring

# 8. Verify the details on Grafana

    Add the dashboard id
    1860

