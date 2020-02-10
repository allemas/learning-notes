# Manage and cleanup Image - Container and Volumes

## Docker cleanup
`docker system prune`
To remove any stopped container and all unused images add -a
`docker system prune -a`

## Docker images
List `docker images -a`
remove `docker rmi Image`

_Dangling images are layers that have no relationship to any tagged images. They no longer serve a purpose and consume disk space._
list : `docker images -f dangling=true`
remove : `docker images purge`

## Docker Container
- List `docker ps -a`
- Remove `docker rm <ID_or_name>`
- Auto remove after run : `docker run --rm image_name`

### Remove containers using more than one filter
- List exited containers `docker ps -a -f status=exited`
- Remove exited containers `docker rm $(docker ps -a -f status=exited -q)`
- List exited and created `docker ps -a -f status=exited -f status=created`
- Remove them  `docker rm $(docker ps -a -f status=exited -f status=created -q)`

### Stop and remove all containers
- List `docker ps -a`
- Stop `docker stop $(docker ps -a -q)`
- Remove `docker rm $(docker ps -a -q)`

## Docker volumes
### Remove one or more specific volumes
- List `docker volume ls`
- Stop `docker volume rm volume_name`

_Support filter agument (-f) `docker volume ls -f dangling=true`_
`docker volume prune`

### Remove a container and its volume
`docker rm -v container_name`