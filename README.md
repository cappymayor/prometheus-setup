## PROMETHEUS SETUP GUIDE ON KUBERNETES
This guide walk through the installation of the prometheus instance on a Kubernetes cluster based on this repository. However, to be able to follow through, you need to have the below installed on your machine.
- A Kubernetes Cluster
  - You can install a Minikube or a Cloud based Kubernetes cluster.
- Helm
  - Considering Prometheus have official chart, we will leverage helm to install Prometheus on Kubernetes.

### STEP 1
- Clone the repository by running the below on your terminal.
```
git clone https://github.com/cappymayor/prometheus-setup.git
```
- Change directory to the newly cloned repository
```
cd prometheus-setup
```

### STEP 2
- Start your Kubernetes Cluster, if you are using Minikube, you can run the below to start your Minikube
```
minikube start
```
- You can run the below command to get all the running pods you have in the default namespace. This is just to verify if your cluster is reachable, its fine if you don't have any pod.
```
kubectl get pods 
```

### STEP 3
- Run the below command to install `Prometheus-server`, `prometheus-kube-state-metrics`, `prometheus-node-exporter`, `prometheus-pushgateway`.
```
helm install prometheus .
```
 - The `prometheus` in the above command is the name of the helm release, this can be anything you want.
 - The `.` at the end is telling helm where to find the `template` and the value override file `value.yaml`.
- You can confirm the installation by running
```
kubectl get pods
```
- You will see the pods are starting, ensure they are all running and in ready state before we can check the Prometheus UI.

### STEP 4
- If all is in running and ready state, run the below command to list all the service created as part of the Prometheus installation.
```
kubectl get svc
```
- Copy the service named `prometheus-server`, after its added like below, you can run the below command to do the forwarding
```
kubectl port-forward service/prometheus-server 8000:80
```
- After running it, you should see something like this `Forwarding from 127.0.0.1:8000` on your terminal, copy it and paste in your browser and you shuld have a Prometheus UI.

###
Prometheus Helm Chart Reference: https://github.com/prometheus-community/helm-charts/tree/main/charts/prometheus

