# Kubernetes Cheatsheet

*   **Core Concepts**: Clusters, Nodes (Master/Control Plane, Worker), Containers.
*   **Key Objects**:
    *   Pods: Smallest deployable unit, one or more containers, shared storage/network.
    *   Services: Abstract way to expose an application running on a set of Pods (e.g., ClusterIP, NodePort, LoadBalancer).
    *   Deployments: Declarative updates for Pods and ReplicaSets, manages stateless applications.
    *   ReplicaSets: Ensures a specified number of Pod replicas are running.
    *   Namespaces: Virtual clusters within a physical cluster.
    *   ConfigMaps & Secrets: Externalized configuration and sensitive data.
    *   Volumes: Persistent storage for Pods.
    *   Ingress: Manages external access to services, typically HTTP.
*   **`kubectl` Commands (Common)**:
    *   Cluster Info: `kubectl cluster-info`, `kubectl get nodes`.
    *   Managing Objects:
        *   `kubectl get <object-type> [object-name] [-n namespace] [-o wide/yaml/json]` (e.g., `kubectl get pods`)
        *   `kubectl describe <object-type> <object-name>`
        *   `kubectl apply -f <filename.yaml>`
        *   `kubectl delete -f <filename.yaml>` or `kubectl delete <object-type> <object-name>`
        *   `kubectl create <object-type> ...` (imperative, less common for deployments)
    *   Interacting with Pods:
        *   `kubectl logs <pod-name> [-c container-name]`
        *   `kubectl exec -it <pod-name> -- /bin/bash` (or other command)
        *   `kubectl port-forward <pod-name> <local-port>:<pod-port>`
    *   Scaling: `kubectl scale deployment <deployment-name> --replicas=<count>`
    *   Rollouts: `kubectl rollout status deployment/<name>`, `kubectl rollout history deployment/<name>`, `kubectl rollout undo deployment/<name>`.
*   **Manifest Files (YAML)**: Defining Kubernetes objects declaratively.
