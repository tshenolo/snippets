# Git

## Clone the Repository
git clone https://github.com/<USERNAME>/<project>.git
cd <project>

## Create and Checkout New Branch
git checkout -b dev-feature

## Stage a specific file for the next commit
git add <filename>

## Commit staged changes to the local repository
git commit -m "<message>"

## Pushing the Local Branch to the Remote Repository
git push --set-upstream origin dev-feature

## Switch to the Main Branch:
git checkout main

## Update the Main Branch:
git pull origin main

## Merge Your Feature Branch into Main:
git merge dev-feature

## Push the Merged Changes to the Remote Repository:
git push origin main

## [Optional] Delete Your Local Feature Branch:
git branch -d dev-feature

## [Optional] Delete the Remote Feature Branch:
git push origin --delete dev-feature

## Keep Your Branch Up to Date
git checkout main
git fetch origin
git pull origin main
git checkout dev-feature
git rebase main

## Resolve Conflicts if Any During Rebase
## Manually resolve the conflict in the given file
git add <conflicted-file>
git rebase --continue

## Push Changes to Your Branch
git push origin dev-feature
or, if you've rebased:
git push origin dev-feature --force

## Keep Main Branch Up to Date Post-Merge
git checkout main
git pull origin main

## Starting a New Feature or Bugfix
git checkout main
git pull origin main
git checkout -b dev-newfeatureorbugfix

## Submit a New Feature
git add <filename>
git commit -m "<message>"
git push --set-upstream origin dev-newfeatureorbugfix

## Unstage a single file
git reset HEAD <filename>

## Unstage all changes
git reset

# Docker
## Pull an Image from Docker Hub
docker pull <repository>:<tag>

## Run a Docker Container
docker run -d
-p <host_port>:<container_port>
--name <container_name> <image_name>

## List Docker Containers
docker ps    (List running containers)  
docker ps -a (List all containers)  

## Stop a Docker Container
docker stop <container_id_or_name>

## Remove a Docker Container
docker rm <container_id_or_name>

## Build a Docker Image from a Dockerfile
docker build -t <image_name>:<tag> .

## Push an Image to Docker Hub
docker push <repository>:<tag>

## View Logs of a Docker Container
docker logs <container_id_or_name>

## Execute a Command in a Running Container
docker exec -it <container_id_or_name> <command>  
docker exec -it <container_id_or_name> /bin/bash

# OpenShift
## Create a New Build Configuration
oc new-build --strategy=docker --binary --name apache-php-oracle

## Start a New Build
oc start-build apache-php-oracle --from-dir=.

## Deploy the Image
oc new-app apache-php-oracle

## Route Management
## To create:
oc expose service/apache-php-oracle --port=8080

## To verify:
oc get route apache-php-oracle

## Logs
To get pods:
oc get pods

## To view logs:
oc logs apache-php-oracle-9cd4b855f-ld2tx -c apache-php-oracle

## Delete Resources
## Deployment Configuration:
oc delete dc/apache-php-oracle

## Service:
oc delete svc/apache-php-oracle

## Route:
oc delete route/apache-php-oracle
