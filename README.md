# Kubernetes-Prometheus
Integrate Prometheus on Kubernetes

## Explanation:

* This YAML defines two deployments: prometheus and grafana.
* Each deployment runs a single container with the corresponding image (prom/prometheus:latest and grafana/grafana:latest).
* Prometheus exposes port 9090 for scraping targets and metrics.
* An optional Prometheus service (prometheus-service) with a nodePort (30900 by default) allows external access.
* Grafana exposes port 3000 for the web interface.
* An optional Grafana service (grafana-service) with a nodePort (31000 by default) allows external access.
ConfigMaps (not defined here) are used to store Prometheus and Grafana configurations (refer to documentation for details).

### 2. Running the YAML file:

Save the YAML content as prometheus-grafana.yaml.

1. Use `kubectl apply -f prometheus-deployment.yaml` to deploy Prometheus in your cluster.
2. Use `kubectl apply -f prometheus-service.yaml` to deploy Prometheus in your cluster.
3. Use `kubectl apply -f prometheus-config-map.yaml` to deploy Prometheus in your cluster.

### 3. Accessing Prometheus and Grafana:

If you deployed the services with NodePorts, access them using:
Prometheus: http://<your_node_ip>:<nodePort> (e.g., http://192.168.1.10:30900)
Grafana: http://<your_node_ip>:<nodePort> (e.g., http://192.168.1.10:31000)

### 4. Additional Notes:

This is a basic example. You might need to configure Prometheus scraping targets and Grafana datasources to monitor your applications.
Remember to update NodePorts if they conflict with existing services.
Consider using ConfigMaps to manage configurations for easier updates.
