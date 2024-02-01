# OpenShift cheat Sheet

## General Commands
### Login
```
oc login --token=<token> --server=<server-url>
```


### Logout
```
oc logout
```


### Get OpenShift Version
```
oc version
```


### Get Help for a Command
```
oc <command> --help
```


## Working with Projects
### List Projects
```
oc projects
```


### Create a New Project
```
oc new-project <project-name>
```


### Switch to a Project
```
oc project <project-name>
```


### Delete a Project
```
oc delete project <project-name>
```


## Working with Applications
### Create a New Application
```
oc new-app <image>
```


### Expose Service to Create a Route
```
oc expose svc/<service-name>
```


### Get Logs for a Pod
```
oc logs <pod-name>
```


### Scale a Deployment
```
oc scale --replicas=<number-of-replicas> dc/<deploymentconfig-name>
```


### Edit a Resource (e.g., deployment, service)
```
oc edit <resource-type>/<resource-name>
```


### Delete a Resource
```
oc delete <resource-type>/<resource-name>
```


## Managing Resources
### List Resources (e.g., pods, services)
```
oc get <resource-type>
```


### Describe a Specific Resource
```
oc describe <resource-type>/<resource-name>
```


### Create a Resource from a YAML File
```
oc create -f <filename.yaml>
```


### Apply a Configuration from a YAML File
```
oc apply -f <filename.yaml>
```


## Working with Nodes and Cluster
### Get Cluster Status
```
oc cluster status
```


### List Nodes
```
oc get nodes
```


### Describe a Node
```
oc describe node <node-name>
```


## Troubleshooting and Debugging
### Debug a Pod
```
oc debug pod/<pod-name>
```


### Get Events in a Namespace
```
oc get events
```

