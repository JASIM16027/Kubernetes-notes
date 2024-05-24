# Kubernetes-notes


Here's how to convert the provided commands into Ubuntu-compatible commands:

1. **Update package lists and install dependencies:**

```sh
sudo apt-get update
sudo apt-get install -y curl apt-transport-https
```

2. **Install kubectl:**

```sh
# Download the latest release of kubectl
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"

# Make the kubectl binary executable
chmod +x kubectl

# Move the binary into your PATH
sudo mv kubectl /usr/local/bin/
```

3. **Install Minikube:**

```sh
# Download the latest release of Minikube
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64

# Make the Minikube binary executable
chmod +x minikube-linux-amd64

# Move the binary into your PATH
sudo mv minikube-linux-amd64 /usr/local/bin/minikube
```

4. **Install Hyperkit (Optional):**
Hyperkit is not available for Linux, it's primarily for macOS. For Linux, Minikube usually uses drivers like Docker, KVM, or VirtualBox. We'll use Docker here.

5. **Start Minikube using Docker:**

```sh
# Start Minikube with the Docker driver
minikube start --driver=docker
```

6. **Verify the installation:**

```sh
# Check kubectl version
kubectl version --client

# Check Minikube version
minikube version

# Check Minikube status
minikube status
```

7. **Create Minikube cluster with Docker driver:**

```sh
minikube start --driver=docker
kubectl get nodes
minikube status
kubectl version
```

8. **Delete cluster and restart in debug mode:**

```sh
minikube delete
minikube start --driver=docker --v=7 --alsologtostderr
minikube status
```

9. **kubectl commands:**

```sh
# List nodes
kubectl get nodes

# List pods
kubectl get pod

# List services
kubectl get services

# Create an nginx deployment
kubectl create deployment nginx-depl --image=nginx

# List deployments
kubectl get deployment

# List replicasets
kubectl get replicaset

# Edit the nginx deployment
kubectl edit deployment nginx-depl
```

10. **Debugging:**

```sh
# Get logs from a pod
kubectl logs {pod-name}

# Execute a command in a pod
kubectl exec -it {pod-name} -- bin/bash
```

11. **Create MongoDB deployment:**

```sh
# Create a MongoDB deployment
kubectl create deployment mongo-depl --image=mongo

# Get logs from the MongoDB pod
kubectl logs mongo-depl-{pod-name}

# Describe the MongoDB pod
kubectl describe pod mongo-depl-{pod-name}
```

12. **Delete deployments:**

```sh
kubectl delete deployment mongo-depl
kubectl delete deployment nginx-depl
```

13. **Create or edit a config file:**

```sh
# Edit or create the nginx-deployment.yaml file
vim nginx-deployment.yaml

# Apply the configuration
kubectl apply -f nginx-deployment.yaml

# List pods
kubectl get pod

# List deployments
kubectl get deployment
```

14. **Delete resources using a config file:**

```sh
kubectl delete -f nginx-deployment.yaml
```

15. **Metrics:**

For metrics, you need to have metrics-server installed in your cluster. Once it's set up, you can use the following command:

```sh
# View metrics for nodes and pods
kubectl top nodes
kubectl top pods
```
