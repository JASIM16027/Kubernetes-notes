### Kubernetes Namespace Overview

A **Namespace** in Kubernetes is a mechanism for isolating groups of resources within a single cluster. Namespaces are intended for use in environments with many users spread across multiple teams, or projects. They provide a scope for names, enabling resource names to be unique within a namespace but not across namespaces.

### 4 Default Namespaces in Kubernetes

1. **default**: The default namespace for objects with no other namespace.
2. **kube-system**: The namespace for objects created by the Kubernetes system.
3. **kube-public**: This namespace is readable by all users (including those not authenticated). It is reserved for cluster usage.
4. **kube-node-lease**: This namespace holds lease objects associated with each node which improve the performance of the node heartbeats as the cluster scales.

### Create a Namespace

You can create a namespace using the following `kubectl` command:

```sh
kubectl create namespace <namespace-name>
```

Example:

```sh
kubectl create namespace my-namespace
```

Alternatively, you can define a namespace in a YAML file and apply it:

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: my-namespace
```

Apply the YAML file:

```sh
kubectl apply -f namespace.yaml
```

### Why Use Namespaces? 4 Use Cases

1. **Environment Isolation**: Different namespaces can be used for different environments such as development, staging, and production to ensure clear separation and avoid conflicts.
2. **Multi-Tenancy**: Multiple teams or projects can share the same Kubernetes cluster without interfering with each other, providing a logical separation.
3. **Resource Quotas**: Namespaces allow setting resource quotas (limits on CPU, memory, etc.) to prevent any single team or project from consuming excessive resources.
4. **Access Control**: Role-Based Access Control (RBAC) can be applied to namespaces to manage permissions and access for different users and teams.

### Characteristics of Namespaces

- **Scope**: Namespaces provide a scope for names; names of resources need to be unique within a namespace but not across namespaces.
- **Isolation**: Logical separation between resources, useful for organizing and managing resources.
- **Quota Management**: Resource quotas can be applied to limit resource usage within a namespace.
- **Access Control**: Kubernetes RBAC can be utilized to restrict or grant access to resources within a namespace.

### Create Components in Namespaces

When creating resources such as Pods, Services, Deployments, etc., you can specify the namespace in the YAML configuration:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
  namespace: my-namespace
spec:
  containers:
  - name: my-container
    image: my-image
```

Apply the configuration:

```sh
kubectl apply -f pod.yaml
```

Or specify the namespace using `kubectl` command line:

```sh
kubectl create deployment my-deployment --image=my-image --namespace=my-namespace
```

### Change Active Namespace

To change the active namespace for your `kubectl` context, use the following command:

```sh
kubectl config set-context --current --namespace=<namespace-name>
```

Example:

```sh
kubectl config set-context --current --namespace=my-namespace
```

This changes the default namespace for the current context, so you don't need to specify the namespace explicitly for every command.

### Summary

Kubernetes namespaces provide a way to partition resources within a cluster, offering benefits such as resource isolation, multi-tenancy, and better organization. They enable fine-grained access control and resource management, making them a crucial feature for managing complex and multi-tenant environments.
