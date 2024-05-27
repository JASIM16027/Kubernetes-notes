### The Main Components of Kubernetes (K8s):

1. **Node & Pod:**
   - **Node:** A physical or virtual machine that serves as a worker in a Kubernetes cluster.
   - **Pod:** The smallest deployable unit in Kubernetes, representing one or more containers that are tightly coupled and share resources.
     - **Example:** Imagine you have a Node called "worker-node-1" in your cluster. You can deploy a Pod on "worker-node-1" that contains two containers: one for your web server and another for a logging sidecar.

   🔥 **Node & Pod:** 🔥
   ```
   Kubernetes Cluster
   └── Node (worker-node-1)
       └── Pod (nginx-server + log-sidecar)
   └── Node (worker-node-2)
   ```

   **Pod Example (pod.yaml):**
   ```yaml
   apiVersion: v1
   kind: Pod
   metadata:
     name: nginx-pod
   spec:
     containers:
     - name: nginx-container
       image: nginx:latest
       ports:
       - containerPort: 80
     - name: log-sidecar
       image: fluentd:latest   # Sidecar container for logging
   ```

2. **Service & Ingress:**
   - **Service:** An abstraction that defines a logical set of Pods and a policy by which to access them. Services enable network access to a set of Pods.
   - **Ingress:** Manages external access to services in a cluster, typically HTTP.
     - **Example:** Let's say you have a service called "frontend-service" that exposes your website to users. You can use an Ingress to route traffic from the internet to the "frontend-service".

   🔥 **Service & Ingress:** 🔥
   ```
   Kubernetes Cluster
   └── Service (frontend-service)
       └── Pod (nginx-server)
   └── Ingress
   ```

   **Service Example (service.yaml):**
   ```yaml
   apiVersion: v1
   kind: Service
   metadata:
     name: frontend-service
   spec:
     selector:
       app: nginx-app   # Points to the labels of Pods to include in the service
     ports:
     - protocol: TCP
       port: 80
       targetPort: 80   # Port on the Pod to forward traffic to
   ```

   **Ingress Example (ingress.yaml):**
   ```yaml
   apiVersion: networking.k8s.io/v1
   kind: Ingress
   metadata:
     name: frontend-ingress
   spec:
     rules:
     - host: example.com
       http:
         paths:
         - path: /
           pathType: Prefix
           backend:
             service:
               name: frontend-service
               port:
                 number: 80   # Port exposed by the service
   ```

3. **ConfigMap & Secret:**
   - **ConfigMap:** Kubernetes object to store non-sensitive configuration data in key-value pairs, which can be consumed by Pods.
   - **Secret:** Similar to ConfigMap but used to store sensitive data like passwords, API keys, and tokens.
     - **Example:** You might store your database connection string in a ConfigMap and your database password in a Secret. Then, your application Pods can access this information securely.

   🔥 **ConfigMap & Secret:** 🔥
   ```
   Kubernetes Cluster
   └── ConfigMap (database-config)
   └── Secret (database-credentials)
   └── Pod
       ├── Container
       │   ├── Environment Variable (from ConfigMap)
       │   ├── Mounted Volume (from Secret)
       │   └── Application
   ```

   **ConfigMap Example (configmap.yaml):**
   ```yaml
   apiVersion: v1
   kind: ConfigMap
   metadata:
     name: database-config
   data:
     database_url: "mysql://user@hostname:3306/database"   # Configuration data
   ```
   
**Secret Example (Secret.yaml):**
```yaml
   apiVersion: v1
   kind: Secret
   metadata:
     name: mysql-secret
   type: Opaque
   data:
      mysql-root-username: dXNlcm5hbWU=
      mysql-root-password: cGFzc3dvcmQ=
   ```


4. **Volumes:**
   - A Volume is a directory, possibly with data in it, accessible to a Container in a Pod.
     - **Example:** You can attach a Volume to a Pod to store persistent data, such as a database's data files or application logs.

   🔥 **Volumes:** 🔥
   ```
   Kubernetes Cluster
   └── Pod
       └── Container
           └── Mounted Volume (Persistent Storage)
   ```

   **Pod with Volume Example (pod_with_volume.yaml):**
   ```yaml
   apiVersion: v1
   kind: Pod
   metadata:
     name: data-storage-pod
   spec:
     containers:
     - name: storage-container
       image: busybox
       volumeMounts:
       - name: persistent-storage
         mountPath: /data
     volumes:
     - name: persistent-storage
       emptyDir: {}   # Empty directory volume
   ```

5. **Deployment & StatefulSet:**
   - **Deployment:** A higher-level abstraction that manages Pods and provides declarative updates to them. Typically used for stateless applications.
   - **StatefulSet:** Manages stateful applications and provides guarantees about the ordering and uniqueness of Pods.
     - **Example:** For a stateless application like a web server, you might use a Deployment. But for a stateful application like a database, you'd use a StatefulSet to ensure each Pod has a stable identity and storage.

   🔥 **Deployment & StatefulSet:** 🔥
   ```
   Kubernetes Cluster
   └── Deployment (nginx-deployment)
       └── ReplicaSet
           └── Pod
   └── StatefulSet (mysql-statefulset)
       └── Pod (mysql-0)
       └── Pod (mysql-1)
       └── ...
   ```

   **Deployment Example (deployment.yaml):**
   ```yaml
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: nginx-deployment
   spec:
     replicas: 3   # Number of desired Pods
     selector:
       matchLabels:
         app: nginx-app
     template:
       metadata:
         labels:
           app: nginx-app
       spec:
         containers:
         - name: nginx-container
           image: nginx:latest
           ports:
           - containerPort: 80
   ```

   **StatefulSet Example (statefulset.yaml):**
   ```yaml
   apiVersion: apps/v1
   kind: StatefulSet
   metadata:
     name: database
   spec:
     serviceName: mysql   # Headless service name for the StatefulSet
     replicas: 3
     selector:
       matchLabels:
         app: mysql
     template:
       metadata:
         labels:
           app: mysql
       spec:
         containers:
         - name: mysql
           image: mysql:5.7
           env:
           - name: MYSQL_ROOT_PASSWORD
             valueFrom:
               secretKeyRef:
                 name: database-credentials
                 key: password   # Accessing password from Secret
   ```


Remember, these components work together to create and manage applications in Kubernetes, providing scalability, reliability, and ease of management.

