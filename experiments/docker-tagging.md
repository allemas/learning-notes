# Docker local repository

## docker local repository
Si vous voulez disposer d'un repository dans un container

> docker run -d -p 5005:5000 --restart always --name my-registry registry:latest
_faire recherche pour stack dans VM_

## Docker Tagging
> docker tag [OPTIONS] SOURCE_IMAGE[:TAG] [REGISTRYHOST/][USERNAME/]IMAGE_NAME[:TAG]

- SOURCE_IMAGE[:TAG]: Image dispo déja installée et visible dans `docker images`
- [REGISTRYHOST/][USERNAME/]IMAGE_NAME[:TAG]
_exemple:_
>docker tag [SOURCE_IMAGE]:latest localhost:50000/[USERNAME]/[IMAGE_NAME]:v1


## Docker pushing to localrepository
Il est necessaire d'avoir tag l'image en respectant la convention de nommage `localhost:50000/[USERNAME]/[IMAGE_NAME]:v1`
_exemple:_
>docker push  localhost:50000/[USERNAME]/[IMAGE_NAME]:v1





- https://code-maze.com/docker-hub-vs-creating-docker-registry/