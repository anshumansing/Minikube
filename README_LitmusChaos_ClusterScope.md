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

    kubectl apply -f petclinic.yaml

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
    kubectl create ns monitoring
    helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
    helm repo update
    helm upgrade --install prometheus-stack prometheus-community/kube-prometheus-stack --namespace monitoring
    kubectl apply -f podmonitor.yaml


# 8. Validate the metrics on Grafana
To Search all of the time series data points grouping by job  in query  

    count({__name__=~".+"}) by (job)

# 9. Verify the details on Grafana

    Add the dashboard json of sockshop.json from this repo.
    Also you can add this dashboard id 13358

