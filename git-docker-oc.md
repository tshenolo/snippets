# Git
## Clone the Repository
```bash
git clone https://github.com/<USERNAME>/<project>.git
cd <project>
```

## Create and Checkout New Branch
```bash
git checkout -b dev-feature
```

## Stage a specific file for the next commit
```bash
git add <filename>
```

## Commit staged changes to the local repository
```bash
git commit -m "<message>"
```

## Pushing the Local Branch to the Remote Repository
```bash
git push --set-upstream origin dev-feature
```

## Switch to the Main Branch:
```bash
git checkout main
```

## Update the Main Branch:
```bash
git pull origin main
```

## Merge Your Feature Branch into Main:
```bash
git merge dev-feature
```

## Push the Merged Changes to the Remote Repository:
```bash
git push origin main
```

## [Optional] Delete Your Local Feature Branch:
```bash
git branch -d dev-feature
```

## [Optional] Delete the Remote Feature Branch:
```bash
git push origin --delete dev-feature
```

## Keep Your Branch Up to Date
```bash
git checkout main
git fetch origin
git pull origin main
git checkout dev-feature
git rebase main
```

## Resolve Conflicts if Any During Rebase
## Manually resolve the conflict in the given file
```bash
git add <conflicted-file>
git rebase --continue
```

## Push Changes to Your Branch
```bash
git push origin dev-feature
```
or, if you've rebased:
```bash
git push origin dev-feature --force
```

## Keep Main Branch Up to Date Post-Merge
```bash
git checkout main
git pull origin main
```

## Starting a New Feature or Bugfix
```bash
git checkout main
git pull origin main
git checkout -b dev-newfeatureorbugfix
```

## Submit a New Feature
```bash
git add <filename>
git commit -m "<message>"
git push --set-upstream origin dev-newfeatureorbugfix
```

## Unstage a single file
```bash
git reset HEAD <filename>
```

## Unstage all changes
```bash
git reset
```

# Docker
## Pull an Image from Docker Hub
```bash
docker pull <repository>:<tag>
```

## Run a Docker Container
```bash
docker run -d
-p <host_port>:<container_port>
--name <container_name> <image_name>
```

## List Docker Containers
```bash
docker ps    (List running containers)  
docker ps -a (List all containers)
```

## Stop a Docker Container
```bash
docker stop <container_id_or_name>
```

## Remove a Docker Container
```bash
docker rm <container_id_or_name>
```

## Build a Docker Image from a Dockerfile
```bash
docker build -t <image_name>:<tag> .
```

## Push an Image to Docker Hub
```bash
docker push <repository>:<tag>
```

## View Logs of a Docker Container
```bash
docker logs <container_id_or_name>
```

## Execute a Command in a Running Container
```bash
docker exec -it <container_id_or_name> <command>  
docker exec -it <container_id_or_name> /bin/bash
```

# OpenShift
## Create a New Build Configuration
```bash
oc new-build --strategy=docker --binary --name apache-php-oracle
```

## Start a New Build
```bash
oc start-build apache-php-oracle --from-dir=.
```

## Deploy the Image
```bash
oc new-app apache-php-oracle
```

## Route Management
## To create:
```bash
oc expose service/apache-php-oracle --port=8080
```

## To verify:
```bash
oc get route apache-php-oracle
```

## Logs
To get pods:
```bash
oc get pods
```

## To view logs:
```bash
oc logs apache-php-oracle-9cd4b855f-ld2tx -c apache-php-oracle
```

## Delete Resources
## Deployment Configuration:
```bash
oc delete dc/apache-php-oracle
```

## Service:
```bash
oc delete svc/apache-php-oracle
```

## Route:
```bash
oc delete route/apache-php-oracle
