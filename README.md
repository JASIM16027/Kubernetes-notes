# Kubernetes Notes

Here's an organized guide to installing and managing Minikube on x86-64 Linux, including starting your cluster, deploying applications, and managing your Minikube clusters:

### Step 1: Install Minikube

1. **Download the latest Minikube release:**

   ```sh
   curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
   ```

2. **Install Minikube and clean up:**

   ```sh
   sudo install minikube-linux-amd64 /usr/local/bin/minikube && rm minikube-linux-amd64
   ```

### Step 2: Start Your Cluster

1. **Start Minikube:**

   From a terminal with administrator access (but not logged in as root), run:

   ```sh
   minikube start
   ```

2. **Troubleshooting:**

   If Minikube fails to start, refer to the [drivers page](https://minikube.sigs.k8s.io/docs/drivers/) for help setting up a compatible container or virtual-machine manager.

### Step 3: Interact with Your Cluster

1. **Access with kubectl:**

   If you already have `kubectl` installed:

   ```sh
   kubectl get po -A
   ```

   Alternatively, minikube can download the appropriate version of kubectl and you should be able to use it like this:

   ```sh
   minikube kubectl -- get po -A
   ```

2. **Add an alias for convenience:**

   You can also make your life easier by adding the following to your shell config: ( (e.g., `~/.bashrc`, `~/.zshrc`):

   ```sh
   alias kubectl="minikube kubectl --"
   ```

 Initially, some services such as the storage-provisioner, may not yet be in a Running state. This is a normal condition during cluster bring-up, and will resolve itself momentarily. For additional insight into your cluster state, minikube bundles the Kubernetes Dashboard, allowing you to get easily acclimated to your new environment:


4. **Open the Kubernetes Dashboard:**

   ```sh
   minikube dashboard
   ```

### Step 4: Deploy Applications

1. **Create a sample deployment and expose it on port 8080:**

   ```sh
   kubectl create deployment hello-minikube --image=kicbase/echo-server:1.0
   kubectl expose deployment hello-minikube --type=NodePort --port=8080
   ```

3. **Check the service:**

   It may take a moment for the deployment to show up:

   ```sh
   kubectl get services hello-minikube
   ```

4. **Access the service:**

 The easiest way to access this service is to let minikube launch a web browser for you:

   ```sh
   minikube service hello-minikube
   ```

  Alternatively, use kubectl to forward the port:

   ```sh
   kubectl port-forward service/hello-minikube 7080:8080
   ```

   Access your application at [http://localhost:7080/](http://localhost:7080/).

### Step 5: Manage Your Cluster

1. **Pause Kubernetes without impacting deployed applications:**

   ```sh
   minikube pause
   ```

2. **Unpause the instance:**

   ```sh
   minikube unpause
   ```

3. **Halt the cluster:**

   ```sh
   minikube stop
   ```

4. **Change the default memory limit (requires a restart):**

   ```sh
   minikube config set memory 9001
   ```

5. **Browse the catalog of easily installed Kubernetes services:**

   ```sh
   minikube addons list
   ```

6. **Create a second cluster with an older Kubernetes release:**

   ```sh
   minikube start -p aged --kubernetes-version=v1.16.1
   ```

7. **Delete all Minikube clusters:**

   ```sh
   minikube delete --all
   ```

8. **Verify the installation:**

```sh
# Check kubectl version
kubectl version --client

# Check Minikube version
minikube version

# Check Minikube status
minikube status
```


```sh
kubectl get nodes
kubectl version
```

9. **Delete cluster and status **

```sh
minikube delete
minikube status
```

10. **kubectl commands:**

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

11. **Debugging:**

```sh
# Get logs from a pod
kubectl logs {pod-name}

# Execute a command in a pod
kubectl exec -it {pod-name} -- bin/bash
```

12. **Create MongoDB deployment:**

```sh
# Create a MongoDB deployment
kubectl create deployment mongo-depl --image=mongo

# Get logs from the MongoDB pod
kubectl logs mongo-depl-{pod-name}

# Describe the MongoDB pod
kubectl describe pod mongo-depl-{pod-name}
```

13. **Delete deployments:**

```sh
kubectl delete deployment mongo-depl
kubectl delete deployment nginx-depl
```

14. **Create or edit a config file:**

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

14. **Metrics:**

For metrics, you need to have metrics-server installed in your cluster. Once it's set up, you can use the following command:

```sh
# View metrics for nodes and pods
kubectl top nodes
kubectl top pods
```

