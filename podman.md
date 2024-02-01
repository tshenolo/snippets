# Podman Cheat Sheet

## 1. Podman Installation:
### On Ubuntu:
```
sudo apt-get -y update
sudo apt-get -y install podman
```

### On CentOS/RHEL:
```
sudo yum -y install podman
```

## 2. Basic Commands:
### Run a container:
```
podman run -it ubuntu bash
```


### List running containers:
```
podman ps
```

### List all containers, including stopped ones:
```
podman ps -a
```

### Stop a container:
```
podman stop CONTAINER_ID
```

### Remove a container:
```
podman rm CONTAINER_ID
```

### Pull an image:
```
podman pull IMAGE_NAME
```

### List images:
```
podman images
```

### Remove an image:
```
podman rmi IMAGE_NAME
```

## 3. Rootless Containers:
Run a rootless container (simply run the command as a non-root user):
```
podman run -it ubuntu bash
```

## 4. Volumes and Bind Mounts:
### Create a volume:
```
podman volume create my_volume
```

### Run a container with a volume:
```
podman run -v my_volume:/data ubuntu
```

### Run a container with a bind mount:
```
podman run -v /path/on/host:/path/in/container ubuntu
```

## 5. Networking:

### Run a container with a specific network:
```
podman run --network=NETWORK_NAME ubuntu
```

## 6. Pods:
### Create a pod:
```
podman pod create --name my_pod
```

### Run a container in a pod:
```
podman run --pod my_pod ubuntu
```

### List pods:
```
podman pod list
```

### Remove a pod:
```
podman pod rm POD_NAME
```

## 7. Building Images:
### Build an image from a Dockerfile:
```
podman build -t my_image .
```



