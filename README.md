
# Kubernetes Notes:

## Step 1: Install Minikube

1. **Download the latest Minikube release:**
   ```sh
   curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
   ```

2. **Install Minikube and clean up:**
   ```sh
   sudo install minikube-linux-amd64 /usr/local/bin/minikube && rm minikube-linux-amd64
   ```

## Step 2: Start Your Cluster

1. **Start Minikube:**
   ```sh
   minikube start
   ```
   - If Minikube fails to start, refer to the [drivers page](https://minikube.sigs.k8s.io/docs/drivers/) for help setting up a compatible container or virtual-machine manager.

2. **Verify the installation:**
   ```sh
   # Check kubectl version
   kubectl version --client

   # Check Minikube version
   minikube version

   # Check Minikube status
   minikube status
   ```

## Step 3: Interact with Your Cluster

1. **Access with kubectl:**
   ```sh
   kubectl get po -A
   ```
   Alternatively, you can use the kubectl bundled with Minikube:
   ```sh
   minikube kubectl -- get po -A
   ```

2. **Add an alias for convenience:**
   Add the following to your shell config (`~/.bashrc`, `~/.zshrc`):
   ```sh
   alias kubectl="minikube kubectl --"
   ```

3. **Open the Kubernetes Dashboard:**
   ```sh
   minikube dashboard
   ```

## Step 4: Deploy Applications

1. **Create a sample deployment and expose it on port 8080:**
   ```sh
   kubectl create deployment hello-minikube --image=kicbase/echo-server:1.0
   kubectl expose deployment hello-minikube --type=NodePort --port=8080
   ```

2. **Check the service:**
   ```sh
   kubectl get services hello-minikube
   ```

3. **Access the service:**
   ```sh
   minikube service hello-minikube
   ```
   Alternatively, use kubectl to forward the port:
   ```sh
   kubectl port-forward service/hello-minikube 7080:8080
   ```
   Access your application at [http://localhost:7080/](http://localhost:7080/).

## Step 5: Manage Your Cluster

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

8. **Delete a specific cluster and check status:**
   ```sh
   minikube delete
   minikube status
   ```

## kubectl Commands

### Basic Commands

1. **List nodes:**
   ```sh
   kubectl get nodes
   ```

2. **List pods:**
   ```sh
   kubectl get pod
   ```

3. **List services:**
   ```sh
   kubectl get services
   ```

4. **Create an nginx deployment:**
   ```sh
   kubectl create deployment nginx-depl --image=nginx
   ```

5. **List deployments:**
   ```sh
   kubectl get deployment
   ```

6. **List replicasets:**
   ```sh
   kubectl get replicaset
   ```

7. **Edit the nginx deployment:**
   ```sh
   kubectl edit deployment nginx-depl
   ```

### MongoDB Deployment

1. **Create a MongoDB deployment:**
   ```sh
   kubectl create deployment mongo-depl --image=mongo
   ```

2. **Get logs from the MongoDB pod:**
   ```sh
   kubectl logs mongo-depl-{pod-name}
   ```

3. **Describe the MongoDB pod:**
   ```sh
   kubectl describe pod mongo-depl-{pod-name}
   ```

### Deleting Deployments

1. **Delete deployments:**
   ```sh
   kubectl delete deployment mongo-depl
   kubectl delete deployment nginx-depl
   ```

### Using Configuration Files

1. **Edit or create a configuration file:**
   ```sh
   vim nginx-deployment.yaml
   ```

2. **Apply the configuration:**
   ```sh
   kubectl apply -f nginx-deployment.yaml
   ```

3. **List pods and deployments:**
   ```sh
   kubectl get pod
   kubectl get deployment
   ```

4. **Delete resources using a configuration file:**
   ```sh
   kubectl delete -f nginx-deployment.yaml
   ```

### Metrics

1. **View metrics for nodes and pods (requires metrics-server):**
   ```sh
   kubectl top nodes
   kubectl top pods
   ```

### Debugging

1. **Get logs from a pod:**
   ```sh
   kubectl logs {pod-name}
   ```

2. **Execute a command in a pod:**
   ```sh
   kubectl exec -it {pod-name} -- bin/bash
   ```
Here's an organized guide to installing and managing Minikube on x86-64 Linux, including starting your cluster, deploying applications, and managing your Minikube clusters:





 
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
8. ** Minikube clusters:**

   ```sh
    minikube version
    minikube status
    minikube delete
   ```
  
