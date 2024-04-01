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

This file defines a Kubernetes Deployment for running Prometheus pods. It specifies:

* Image: The Docker image to use for the Prometheus container (e.g., prom/prometheus:latest).
* Replicas: The number of Prometheus pods to run (usually 1 for a single instance).
* Resource Requests and Limits: Memory and CPU resource requests and limits for the Prometheus container.
* Port: The port on which Prometheus exposes its web UI (usually 9090).
* ConfigMap: (Optional) A ConfigMap reference containing the Prometheus configuration options.
* Volume Mounts: Mounts the ConfigMap volume (if used) at the desired path within the container (e.g., /etc/prometheus).

2. Use `kubectl apply -f prometheus-service.yaml` to deploy Prometheus in your cluster.

This file defines a Kubernetes Service to expose the Prometheus pods running in the deployment. This allows other applications in the cluster to access the Prometheus API. It specifies:

* Selector: Labels to match the pods in the Prometheus deployment.
* Ports: The port on which the service exposes Prometheus (usually 9090).
* Type: The service type (e.g., ClusterIP for internal cluster access or NodePort for external access through a NodePort).

3. Use `kubectl apply -f prometheus-config-map.yaml` to deploy Prometheus in your cluster.

This file defines a Kubernetes ConfigMap containing the configuration options for Prometheus. It allows you to manage the configuration separately from the deployment definition. The ConfigMap defines key-value pairs for various configuration options:

* scrape_interval: Interval between scraping targets for metrics.
* global: Global settings for all scrape configs.
* scrape_configs: Individual configurations for scraping specific targets (e.g., services, endpoints).

### 3. Accessing Prometheus and Grafana:

If you deployed the services with NodePorts, access them using:
Prometheus: http://<your_node_ip>:<nodePort> (e.g., http://192.168.1.10:30900)
Grafana: http://<your_node_ip>:<nodePort> (e.g., http://192.168.1.10:31000)

### 4. Additional Notes:

This is a basic example. You might need to configure Prometheus scraping targets and Grafana datasources to monitor your applications.
Remember to update NodePorts if they conflict with existing services.
Consider using ConfigMaps to manage configurations for easier updates.

### Further Resources

Prometheus Documentation: https://prometheus.io/docs/introduction/overview/
Kubernetes Documentation: https://kubernetes.io/docs/home/
