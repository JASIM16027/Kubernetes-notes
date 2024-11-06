
# Kubernetes Notes

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
  ```sh

  nginx-deployment.yaml:
  
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: nginx-depl
    spec:
      replicas: 3
      selector:
        matchLabels:
          app: nginx
      template:
        metadata:
          labels:
            app: nginx
        spec:
          containers:
          - name: nginx
            image: nginx:latest
            ports:
            - containerPort: 80

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

Here’s a more streamlined and extended version of the Kubernetes commands and concepts for managing pods, deployments, and rollouts, with added structure for better clarity:

---

### 1. **Check Kubernetes Node Version and Operating System**
   - To get details about the version of Kubernetes and the flavor of the OS on the nodes:
     ```bash
     kubectl get nodes -o wide
     kubectl describe nodes
     ```

---

### 2. **Creating a Pod**

   **Create an NGINX Pod:**
   ```bash
   kubectl run nginx --image=nginx
   ```
   - *Note*: Starting from Kubernetes version 1.18, `kubectl run` (without additional arguments like `--generator`) creates a pod, not a deployment.

   **List Pods:**
   ```bash
   kubectl get pods
   ```

   **Get Detailed Pod Information:**
   ```bash
   kubectl describe pod nginx
   ```

   **View Pods with Additional Information:**
   ```bash
   kubectl get pods -o wide
   ```

---

### 3. **Creating a Deployment**
   - **Create an NGINX Deployment Imperatively:**
     ```bash
     kubectl create deployment nginx --image=nginx
     ```

   - **Create a Deployment via YAML:**
     ```bash
     kubectl apply -f deployment.yaml
     ```

   **Get Deployment Information:**
   ```bash
   kubectl get deployment
   kubectl describe deployment myapp-deployment
   ```

   **Delete Deployment:**
   ```bash
   kubectl delete -f deployment.yaml
   kubectl delete deployment myapp-deployment
   ```

---

### 4. **Replicaset Management**
   - **Create a Replicaset:**
     ```bash
     kubectl create -f replicaset.yaml
     ```

   - **View Replicaset:**
     ```bash
     kubectl get replicaset
     kubectl describe replicaset myapp-replicaset
     ```

   - **Scale Replicaset:**
     ```bash
     kubectl scale replicaset myapp-replicaset --replicas=5
     ```

   - **Filter Pods by Label:**
     ```bash
     kubectl get pods -l app=myapp,type=front-end
     ```

   - **Delete Replicaset:**
     ```bash
     kubectl delete -f replicaset.yaml
     ```

---

### 5. **Managing Rollouts in Deployments**

   **Check Rollout Status:**
   ```bash
   kubectl rollout status deployment/myapp-deployment
   ```

   **View Rollout History:**
   ```bash
   kubectl rollout history deployment/myapp-deployment
   ```

   **Rollback Deployment to a Previous Revision:**
   ```bash
   kubectl rollout undo deployment/myapp-deployment
   ```

   **Set Image in Deployment:**
   ```bash
   kubectl set image deployment/myapp-deployment nginx=nginx:1.9.1
   ```

---

### 6. **General Kubernetes Commands**

   **View Resource Explanations:**
   ```bash
   kubectl explain deployment
   kubectl explain replicaset
   ```

   **View All Resources:**
   ```bash
   kubectl get all
   ```

---

### 7. **Deployment Strategies**

   **Recreate Strategy:**
   - Deletes all existing Pods and creates new ones immediately.
   
   **RollingUpdate Strategy:**
   - Incrementally replaces the old pods with new ones while ensuring there’s no downtime.

---

### Useful Resources:
- [Kubernetes Concepts](https://kubernetes.io/docs/concepts/)
- [Pod Overview](https://kubernetes.io/docs/concepts/workloads/pods/pod-overview/)
- [Certified Kubernetes Administrator](https://www.cncf.io/certification/cka/)
- [Exam Curriculum](https://github.com/cncf/curriculum)
- [Candidate Handbook](https://www.cncf.io/certification/candidate-handbook)
- [CKA Exam Tips](http://training.linuxfoundation.org/go//Important-Tips-CKA-CKAD)

  
### KUBERNETES DEPLOYMENT

```yaml

** ::::::::::::::::::::::::::::: POSTGRES DEPLOYMENT SAMPLE ::::::::::::::::::::::::::::::::::::::::::::::::::::::: **

apiVersion: apps/v1
kind: Deployment
metadata:
  name: postgres-deploy
  labels:
    name: postgres-deploy
    app: demo-voting-app
spec:
  replicas: 1
  selector:
    matchLabels:
      name: postgres-pod
      app: demo-voting-app
    
  template:
    metadata:
      name: postgres-pod
      labels:
        name: postgres-pod
        app: demo-voting-app
    spec:
      containers:
        - name: postgres
          image: postgres
          ports:
            - containerPort: 5432
          env:
            - name: POSTGRES_USER
              value: "postgres"
            - name: POSTGRES_PASSWORD
              value: "postgres"
            - name: POSTGRES_HOST_AUTH_METHOD
              value: trust


```




```yaml

** :::::::::::::::::::::::::::::REDIS DEPLOYMENT SAMPLE ::::::::::::::::::::::::::::::::::::::::::::::::::::::: **

apiVersion: apps/v1
kind: Deployment
metadata:
  name: redis-deploy
  labels:
    name: redis-deploy
    app: demo-voting-app
spec:
  replicas: 1
  selector:
    matchLabels:
      name: redis-pod
      app: demo-voting-app
    
  template:
    metadata:
      name: redis-pod
      labels:
        name: redis-pod
        app: demo-voting-app
    spec:
      containers:
        - name: redis
          image: redis
          ports:
            - containerPort: 6379
         
```


```yaml

** :::::::::::::::::::::::::::::VOTING-APP DEPLOYMENT SAMPLE ::::::::::::::::::::::::::::::::::::::::::::::::::::::: **

apiVersion: apps/v1
kind: Deployment
metadata:
  name: voting-app-deploy
  labels:
    name: voting-app-deploy
    app: demo-voting-app
spec:
  replicas: 1
  selector:
    matchLabels:
      name: voting-app-pod
      app: demo-voting-app
    
  template:
    metadata:
      name: voting-app-pod
      labels:
        name: voting-app-pod
        app: demo-voting-app
    spec:
      containers:
        - name: voting-app
          image: kodekloud/examplevotingapp_vote:v1
          ports:
            - containerPort: 80
    

```

```yaml

** :::::::::::::::::::::::::::::RESULT-APP DEPLOYMENT SAMPLE ::::::::::::::::::::::::::::::::::::::::::::::::::::::: **

apiVersion: apps/v1
kind: Deployment
metadata:
  name: result-app-deploy
  labels:
    name: result-app-deploy
    app: demo-voting-app
spec:
  replicas: 1
  selector:
    matchLabels:
      name: result-app-pod
      app: demo-voting-app
    
  template:
    metadata:
      name: result-app-pod
      labels:
        name: result-app-pod
        app: demo-voting-app
    spec:
      containers:
        - name: result-app
          image:  // IMAGE WHICH IS DEPLOYED IN DOCKER HUB
          ports:
            - containerPort: 80
    
```

```yaml
** :::::::::::::::::::::::::::::WORKER-APP DEPLOYMENT SAMPLE ::::::::::::::::::::::::::::::::::::::::::::::::::::::: **

apiVersion: apps/v1
kind: Deployment
metadata:
  name: worker-app-deploy
  labels:
    name: worker-app-deploy
    app: demo-voting-app
spec:
  replicas: 1
  selector:
    matchLabels:
      name: worker-app-pod
      app: demo-voting-app
    
  template:
    metadata:
      name: worker-app-pod
      labels:
        name: worker-app-pod
        app: demo-voting-app
    spec:
      containers:
        - name: worker-app
          image: // IMAGE WHICH IS DEPLOYED IN DOCKER HUB
   ```


### KUBERNETES SERVICES

```yaml
** ::::::::::::::::::::::::::::: POSTGRES SERVICE SAMPLE ::::::::::::::::::::::::::::::::::::::::::::::::::::::: **

apiVersion: v1
kind: Service
metadata:
  name: db
  labels:
    name: postgres-service
    app: demo-voting-app
spec:
  ports:
    - port: 5432
      targetPort: 5432
  selector:
    name: postgres-pod
    app: demo-voting-app
```




```yaml
** :::::::::::::::::::::::::::::REDIS SERVICE SAMPLE ::::::::::::::::::::::::::::::::::::::::::::::::::::::: **

apiVersion: v1
kind: Service
metadata:
  name: redis
  labels:
    name: redis-service
    app: demo-voting-app
spec:
  ports:
    - port: 6379
      targetPort: 6379
  selector:
    name: redis-pod
    app: demo-voting-app
         
```


```yaml
** :::::::::::::::::::::::::::::VOTING-APP DEPLOYMENT SAMPLE ::::::::::::::::::::::::::::::::::::::::::::::::::::::: **

apiVersion: v1
kind: Service
metadata:
  name: voting-service
  labels:
    name: voting-service
    app: demo-voting-app
spec:
  type: LoadBalancer
  ports:
    - port: 80
      targetPort: 80
  selector:
    name: voting-app-pod
    app: demo-voting-app    

```

```yaml

** :::::::::::::::::::::::::::::RESULT-APP DEPLOYMENT SAMPLE ::::::::::::::::::::::::::::::::::::::::::::::::::::::: **

apiVersion: v1
kind: Service
metadata:
  name: result-service
  labels:
    name: result-service
    app: demo-voting-app
spec:
  type: LoadBalancer
  ports:
    - port: 80
      targetPort: 80
  selector:
    name: result-app-pod
    app: demo-voting-app
    
```

```yaml
** :::::::::::::::::::::::::::::WORKER-APP DEPLOYMENT SAMPLE ::::::::::::::::::::::::::::::::::::::::::::::::::::::: **

apiVersion: apps/v1
kind: Deployment
metadata:
  name: worker-app-deploy
  labels:
    name: worker-app-deploy
    app: demo-voting-app
spec:
  replicas: 1
  selector:
    matchLabels:
      name: worker-app-pod
      app: demo-voting-app
    
  template:
    metadata:
      name: worker-app-pod
      labels:
        name: worker-app-pod
        app: demo-voting-app
    spec:
      containers:
        - name: worker-app
          image: // IMAGE WHICH IS DEPLOYED IN DOCKER HUB
   ```


---


---

### **What is Kubernetes?**  
A platform for managing and running multiple containers over multiple different machines.

### **Why use Kubernetes?**  
 When you need to run many different containers with different images( unique images). 
 
---


## Chapter 1: Elastic Beanstalk Scaling Strategy

![image](https://github.com/user-attachments/assets/03428073-e63c-4a0a-b509-8956bd8a12b4)


### Overview

In this architecture, we’re looking at a scaling strategy using **AWS Elastic Beanstalk**, a platform-as-a-service (PaaS) that helps developers deploy and manage web applications without worrying too much about the underlying infrastructure. Elastic Beanstalk handles things like load balancing, scaling, and monitoring automatically.

### Diagram Walkthrough

#### Components

1. **Load Balancer**:
   - The load balancer is the entry point for all incoming requests. When users access the application, their requests first hit the load balancer, which then decides which instance to forward the request to.
   - The goal of the load balancer is to distribute traffic evenly across multiple instances, which prevents any single machine from getting overloaded.

2. **Nginx, Server, Client, and Worker Instances**:
   - Each instance or virtual machine in this architecture has:
     - **Nginx**: A web server that routes incoming traffic to the correct service or component within each instance.
     - **Server**: The backend application code, handling requests such as fetching data from the database, processing user inputs, etc.
     - **Client**: The frontend application, which may serve static assets or render pages for the user.
     - **Worker**: A component dedicated to background tasks, like sending emails, processing payments, or generating reports. This way, long-running tasks don’t slow down the main application.
   
3. **Multiple Machines with Limited Control**:
   - Elastic Beanstalk automatically adds or removes instances to meet demand. As traffic grows, more instances are launched, each with the same set of components (Nginx, server, client, worker).
   - However, because Elastic Beanstalk is a managed service, there’s limited control over how each instance is configured. You can’t easily specify that one instance should have more powerful resources for the worker, or another for the server, for example.

#### Pros and Cons

- **Pros**:
  - **Easy to Set Up**: Elastic Beanstalk simplifies deployment by handling server and environment management.
  - **Automatic Scaling**: Elastic Beanstalk monitors your app’s performance and scales up or down based on traffic, without requiring manual intervention.
  - **Managed Infrastructure**: AWS handles load balancing, monitoring, and scaling.

- **Cons**:
  - **Limited Flexibility**: You don’t have fine-grained control over specific resources within each instance. All instances are treated the same way.
  - **Cost**: Because Elastic Beanstalk scales entire instances rather than individual services, it can be costly, especially if you only need more resources for one specific component.

#### Use Case Example: E-commerce Platform

Imagine you’re running an e-commerce platform that experiences high traffic during peak times, like Black Friday. Elastic Beanstalk is suitable here because:

- It scales up during peak times, adding more instances to handle increased traffic.
- It distributes traffic across multiple instances to prevent any one server from overloading.
- AWS manages the infrastructure, so your team can focus on developing features instead of server management.

**However**, if your platform relies heavily on background tasks (e.g., real-time order processing), you might encounter limitations with this approach. Since each instance has the same configuration, you can't give extra resources specifically to the worker component.

---

## Chapter 2: Clustered Node Orchestration with Containers

![image](https://github.com/user-attachments/assets/839177c8-9bf7-4ef0-8ee8-98b5a7fd536d)


### Overview

In this architecture, we’re looking at a **containerized cluster** managed by an orchestration tool (like Kubernetes). Containers offer a lightweight, modular way to package and deploy application components, allowing for fine-grained control over scaling and resource allocation.

### Diagram Walkthrough

#### Components

1. **Load Balancer**:
   - Similar to the Elastic Beanstalk setup, the load balancer here routes incoming requests. However, in a containerized cluster, the load balancer distributes traffic across **nodes**, each of which contains one or more containers.
   - The load balancer can route requests based on the specific type of service (e.g., user profiles, messaging, feeds), directing them to nodes with available containers that handle the request type.

2. **Nodes**:
   - A **node** is a server (either virtual or physical) in the cluster. Each node hosts one or more containers, and it’s the basic building block of the containerized cluster.
   - Nodes can be configured differently based on the workload they handle. For example, one node might be optimized to run more CPU-intensive containers, while another node is configured for tasks that need more memory.

3. **Containers**:
   - Containers are isolated environments that package everything a microservice needs to run (code, dependencies, configuration).
   - Each container can run a different microservice or application instance. For instance, one container might handle user authentication, another might handle messaging, and another might be responsible for notifications.
   - Containers allow for independent scaling. If a particular microservice experiences high demand, more containers can be added to handle that specific service, without scaling the entire application.

4. **Master Node**:
   - The master node controls the entire cluster, ensuring that containers are scheduled, monitored, and scaled as needed.
   - The master node also allocates resources to nodes based on their load and availability. It maintains a high-level view of the cluster, ensuring that services are running smoothly and scaling as necessary.

#### Pros and Cons

- **Pros**:
  - **Granular Control**: You have detailed control over each component in the system. Each container can be configured individually, allowing you to optimize resources for specific services.
  - **Independent Scaling**: You can scale only the components that need it. If the messaging service experiences high demand, you can add containers for just that service.
  - **Fault Tolerance**: If a container or node fails, the orchestration tool (like Kubernetes) will restart or relocate the affected container, ensuring high availability.

- **Cons**:
  - **Complexity**: Managing a containerized environment requires expertise in orchestration and often involves more setup and maintenance.
  - **Single Point of Failure**: The master node is critical. If it fails and there’s no redundancy, the entire cluster could be disrupted, though Kubernetes and similar tools often have measures to handle this.

#### Use Case Example: Social Media Platform

Consider a social media platform that has multiple microservices for features like user profiles, posts, messaging, notifications, and search. With a containerized cluster:

- Each microservice runs in its own container, allowing you to manage and scale them independently. For example, if user posts are in high demand, you can scale the posts container without affecting other services.
- The master node controls where each service runs, optimizing resource usage across the cluster.
- If one node becomes overloaded, the master can redistribute containers to other nodes, maintaining performance and stability.

**However**, this setup can be complex to manage. It requires familiarity with container orchestration tools like Kubernetes and a deeper understanding of how to configure and optimize individual services within the cluster.

---

### Comparison Summary

| Feature                         | Elastic Beanstalk (Diagram 1)             | Containerized Cluster (Diagram 2)                 |
|---------------------------------|------------------------------------------|--------------------------------------------------|
| **Control**                     | Limited to AWS-managed scaling and setup | High control over individual service configuration |
| **Scaling**                     | Scales entire instances uniformly         | Scales individual services independently         |
| **Ease of Use**                 | Easy, minimal setup                      | Complex, requires expertise in orchestration      |
| **Resource Optimization**       | Limited optimization options             | Fine-grained resource allocation per service     |
| **Ideal for**                   | Simple or monolithic applications        | Complex, microservices-based applications        |

In summary, **Elastic Beanstalk** (Diagram 1) is suited for simpler applications that don’t require individual service scaling, while a **containerized cluster** (Diagram 2) is ideal for applications with microservices, where specific control and independent scaling of each service are essential.

