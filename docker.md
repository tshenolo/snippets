# Docker Cheat Sheet

## Basic Commands
- **Version information**: `docker --version`
- **Detailed information**: `docker info`
- **Help**: `docker <command> --help`

## Image Management
- **List images**: `docker images`
- **Pull an image**: `docker pull <image-name>`
- **Build an image**: `docker build -t <image-name>:<tag> <path-to-dockerfile>`
- **Remove an image**: `docker rmi <image-name>`
  
## Container Management
- **List running containers**: `docker ps`
- **List all containers**: `docker ps -a`
- **Run a container**: `docker run <image-name>`
- **Stop a container**: `docker stop <container-id>`
- **Remove a container**: `docker rm <container-id>`
- **Inspect a container**: `docker inspect <container-name/id>`
- **Fetch logs of a container**: `docker logs <container-name/id>`

## Docker Compose
- **Build services**: `docker-compose build`
- **Start services**: `docker-compose up`
- **Stop services**: `docker-compose down`
- **View running services**: `docker-compose ps`

## Networking
- **List networks**: `docker network ls`
- **Inspect a network**: `docker network inspect <network-name/id>`
- **Create a network**: `docker network create <network-name>`
- **Remove a network**: `docker network rm <network-name>`

## Volume Management
- **List volumes**: `docker volume ls`
- **Create a volume**: `docker volume create <volume-name>`
- **Remove a volume**: `docker volume rm <volume-name>`
  
## Miscellaneous
- **Docker system information**: `docker system info`
- **Prune unused images, containers, and volumes**: `docker system prune`

