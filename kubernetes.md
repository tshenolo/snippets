# Kubernetes (k8s) Cheatsheet

This cheatsheet covers common `kubectl` commands and concepts for interacting with a Kubernetes cluster.

## Core Concepts

*   **Cluster**: A set of worker machines, called nodes, that run containerized applications. Managed by the control plane.
*   **Node**: A worker machine in Kubernetes, can be a VM or a physical machine.
*   **Control Plane**: Manages the worker nodes and the Pods in the cluster. Components include kube-apiserver, etcd, kube-scheduler, kube-controller-manager.
*   **Container**: Lightweight, standalone, executable package of software that includes everything needed to run it.
*   **Pod**: The smallest and simplest unit in the Kubernetes object model that you create or deploy. A Pod represents a running process on your cluster and can contain one or more containers (like Docker containers), storage resources, a unique network IP, and options that govern how the container(s) should run.
*   **Service**: An abstract way to expose an application running on a set of Pods as a network service.
*   **Deployment**: Provides declarative updates for Pods and ReplicaSets. You describe a desired state in a Deployment, and the Deployment Controller changes the actual state to the desired state at a controlled rate.
*   **ReplicaSet**: Ensures that a specified number of Pod replicas are running at any given time.
*   **Namespace**: Provides a scope for names. Used to divide cluster resources between multiple users/teams.
*   **ConfigMap**: Used to store non-confidential data in key-value pairs. Pods can consume ConfigMaps as environment variables, command-line arguments, or as configuration files in a volume.
*   **Secret**: Used to store sensitive information, such as passwords, OAuth tokens, and ssh keys.
*   **Volume**: A directory, possibly with some data in it, which is accessible to the Containers in a Pod.
*   **Ingress**: An API object that manages external access to the services in a cluster, typically HTTP. Ingress can provide load balancing, SSL termination, and name-based virtual hosting.
*   **Manifest Files (YAML/JSON)**: Declarative configuration files that define Kubernetes objects.

## `kubectl` Basic Commands

*   **Get kubectl version**:
    ```bash
    kubectl version
    kubectl version --short --client
    ```
*   **Get cluster information**:
    ```bash
    kubectl cluster-info
    ```
*   **Configure kubectl context** (if you have multiple clusters):
    ```bash
    kubectl config get-contexts # List available contexts
    kubectl config current-context # Display current context
    kubectl config use-context <context_name> # Switch to a different context
    ```
*   **Get help**:
    ```bash
    kubectl --help
    kubectl <command> --help # Help for a specific command, e.g., kubectl get --help
    kubectl explain pods # Documentation for a resource type
    kubectl explain pods.spec.containers
    ```

## Managing Kubernetes Objects

Most `kubectl` commands follow the pattern: `kubectl <action> <resource_type> [resource_name] [flags]`

*   **Common Actions**: `get`, `describe`, `create`, `apply`, `delete`, `edit`, `logs`, `exec`, `port-forward`, `scale`, `rollout`.
*   **Common Resource Types**: `pods` (po), `services` (svc), `deployments` (deploy), `replicasets` (rs), `nodes` (no), `namespaces` (ns), `configmaps` (cm), `secrets`, `ingresses` (ing), `persistentvolumes` (pv), `persistentvolumeclaims` (pvc), `jobs`, `cronjobs` (cj).

*   **Get (List/View) Resources**:
    *   List all pods in the current namespace:
        ```bash
        kubectl get pods
        ```
    *   List all pods in a specific namespace:
        ```bash
        kubectl get pods -n <namespace_name>
        ```
    *   List all pods in all namespaces:
        ```bash
        kubectl get pods --all-namespaces # or kubectl get pods -A
        ```
    *   Get a specific pod by name:
        ```bash
        kubectl get pod <pod_name>
        ```
    *   Get detailed information about a pod (YAML format):
        ```bash
        kubectl get pod <pod_name> -o yaml
        ```
    *   Get detailed information about a pod (JSON format):
        ```bash
        kubectl get pod <pod_name> -o json
        ```
    *   Get pods with more details (IP, node, etc.):
        ```bash
        kubectl get pods -o wide
        ```
    *   List all services:
        ```bash
        kubectl get services # or kubectl get svc
        ```
    *   List all deployments:
        ```bash
        kubectl get deployments
        ```
    *   Get resources with specific labels:
        ```bash
        kubectl get pods -l app=my-app
        kubectl get pods -l environment=production,tier=frontend
        ```
*   **Describe Resources** (get detailed information, including events):
    ```bash
    kubectl describe pod <pod_name>
    kubectl describe service <service_name>
    kubectl describe node <node_name>
    ```
*   **Create Resources** (from YAML/JSON manifest files):
    ```bash
    kubectl apply -f ./my-pod.yaml
    kubectl apply -f ./my-deployment.json
    kubectl apply -f ./directory_with_manifests/ # Apply all manifests in a directory
    ```
    *   `apply` is preferred over `create` as it handles updates if the resource already exists.
    *   Create a resource imperatively (less common for complex objects):
        ```bash
        kubectl create deployment my-nginx --image=nginx
        kubectl create namespace my-namespace
        ```
*   **Delete Resources**:
    *   Delete a pod defined in a YAML file:
        ```bash
        kubectl delete -f ./my-pod.yaml
        ```
    *   Delete a pod by name:
        ```bash
        kubectl delete pod <pod_name>
        ```
    *   Delete all pods with a specific label:
        ```bash
        kubectl delete pods -l app=my-app
        ```
    *   Delete a deployment and its associated pods/replicasets:
        ```bash
        kubectl delete deployment <deployment_name>
        ```
        ```bash
        kubectl delete service <service_name> namespace <namespace_name>
        ```
    *   Force delete a pod (use with caution, e.g., if stuck terminating):
        ```bash
        kubectl delete pod <pod_name> --grace-period=0 --force
        ```
*   **Edit Resources** (opens the resource manifest in your default editor):
    ```bash
    kubectl edit deployment <deployment_name>
    kubectl edit service <service_name>
    ```
*   **Label Resources**:
    ```bash
    kubectl label pods <pod_name> environment=production
    kubectl label pods <pod_name> version=v1 --overwrite # Overwrite existing label
    kubectl label pods <pod_name> mylabel- # Remove a label
    ```

## Interacting with Pods

*   **View logs of a pod**:
    ```bash
    kubectl logs <pod_name>
    ```
    *   If the pod has multiple containers:
        ```bash
        kubectl logs <pod_name> -c <container_name>
        ```
    *   Follow logs (stream):
        ```bash
        kubectl logs -f <pod_name>
        # kubectl logs -f <pod_name> -c <container_name>
        ```
    *   Get logs from a previous instance of a crashed container:
        ```bash
        kubectl logs <pod_name> --previous
        ```
*   **Execute a command in a container**:
    ```bash
    kubectl exec <pod_name> -- <command> [args...]
    # Example: List files in a container
    # kubectl exec <pod_name> -- ls /app
    ```
    *   Get an interactive shell into a container:
        ```bash
        kubectl exec -it <pod_name> -- /bin/sh # or /bin/bash
        # kubectl exec -it <pod_name> -c <container_name> -- /bin/sh
        ```
*   **Copy files to/from a container**:
    *   Copy from pod to local:
        ```bash
        kubectl cp <namespace>/<pod_name>:<path_in_pod> ./local_path
        # Example: kubectl cp my-namespace/my-pod:/app/logs/error.log ./error.log
        ```
    *   Copy from local to pod:
        ```bash
        kubectl cp ./local_file <namespace>/<pod_name>:<path_in_pod>
        # Example: kubectl cp ./config.txt my-namespace/my-pod:/app/config.txt
        ```
        *   If a container name is not specified, it defaults to the first container in the pod. Use `-c <container_name>` if needed.
*   **Port Forwarding** (access an application in a pod/service locally):
    ```bash
    kubectl port-forward pod/<pod_name> <local_port>:<pod_port>
    # Example: kubectl port-forward my-app-pod 8080:80
    # Access via localhost:8080
    ```
    ```bash
    kubectl port-forward service/<service_name> <local_port>:<service_target_port>
    # Example: kubectl port-forward svc/my-service 9000:http
    ```

## Managing Deployments

*   **Scale a deployment** (change number of replicas):
    ```bash
    kubectl scale deployment <deployment_name> --replicas=<count>
    # Example: kubectl scale deployment my-app-deployment --replicas=5
    ```
*   **View rollout status**:
    ```bash
    kubectl rollout status deployment/<deployment_name>
    ```
*   **View rollout history**:
    ```bash
    kubectl rollout history deployment/<deployment_name>
    ```
    *   View details of a specific revision:
        ```bash
        kubectl rollout history deployment/<deployment_name> --revision=<revision_number>
        ```
*   **Rollback to a previous revision**:
    ```bash
    kubectl rollout undo deployment/<deployment_name>
    # Rollback to a specific revision
    # kubectl rollout undo deployment/<deployment_name> --to-revision=<revision_number>
    ```
*   **Update image of a deployment**:
    ```bash
    kubectl set image deployment/<deployment_name> <container_name>=<new_image_tag>
    # Example: kubectl set image deployment/my-app-deploy my-app-container=my-app:v2.0
    ```
*   **Autoscale a deployment** (requires Metrics Server to be installed):
    ```bash
    kubectl autoscale deployment <deployment_name> --cpu-percent=50 --min=2 --max=10
    ```

## Example Minimal Pod Manifest (`pod-example.yaml`)

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-nginx-pod
  labels:
    app: nginx
    environment: development
spec:
  containers:
  - name: nginx-container
    image: nginx:latest
    ports:
    - containerPort: 80
```

## Example Minimal Deployment Manifest (`deployment-example.yaml`)

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3 # Desired number of Pods
  selector:
    matchLabels: # This Deployment manages Pods with these labels
      app: nginx
  template: # Pod template
    metadata:
      labels: # Labels applied to Pods created by this Deployment
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.21 # Use a specific version
        ports:
        - containerPort: 80
```

## Example Minimal Service Manifest (`service-example.yaml`)

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  selector:
    app: nginx # Selects Pods with this label
  ports:
    - protocol: TCP
      port: 80       # Port the Service is available on within the cluster
      targetPort: 80 # Port on the Pods the Service routes traffic to
  type: ClusterIP # Default type, only reachable within the cluster
  # Other types: NodePort, LoadBalancer, ExternalName
```

## Working with Nodes

*   **List nodes**:
    ```bash
    kubectl get nodes
    kubectl get nodes -o wide
    ```
*   **Cordon a node** (mark as unschedulable):
    ```bash
    kubectl cordon <node_name>
    ```
*   **Uncordon a node** (mark as schedulable):
    ```bash
    kubectl uncordon <node_name>
    ```
*   **Drain a node** (safely evict pods for maintenance):
    ```bash
    kubectl drain <node_name> --ignore-daemonsets --delete-emptydir-data
    ```
    *   `--ignore-daemonsets`: DaemonSet pods are not evicted.
    *   `--delete-emptydir-data`: If pods use emptyDir volumes, their data will be deleted.
    ```

This ensures the Kubernetes cheatsheet is now in the correct detailed format. I will continue reviewing the other selected files.
