# Docker Basics Cmd

# .dockerignore
_example:_
```
node_modules
npm-debug.log
Dockerfile
.dockerignore
```

# Build image
`docker build -t <docker_repository>/<image_name> .`
The `.` specifies that the build context is the current directory.

# List available images
`docker images`

# Run container
`docker run --name <container_name> -p <local_port>:<container_port> -d <docker_repository>/<image_name>`

# Run shell
if stoped :
`docker exec -it <name_container> bash`
_bash not stoped after exit because interactive mode_

# Remove container and image
`docker rm -v container_name`


### Links
- [how-to-build-a-node-js-application-with-docker-quickstart](https://www.digitalocean.com/community/tutorials/how-to-build-a-node-js-application-with-docker-quickstart)