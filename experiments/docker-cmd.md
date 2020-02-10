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
_remove all inactive containers_`docker container prune`

# Container network
## Create network
`docker network create <name>`
## connect container to bridge
When you create a new container, you can specify one or more --network flags. This example connects a Nginx container to the my-net network. It also publishes port 80 in the container to port 8080 on the Docker host, so external clients can access that port. Any other container connected to the my-net network has access to all ports on the my-nginx container, and vice versa.
`docker network connect <network_name> <container2>`


## inspect network
`docker network inspect`
```

    {
        "Name": "my-net",
        "Id": "b57e393b7c9ab38d596ad13b5a5341812cdc44600370afd74c25be0daada5663",
        "Created": "2020-02-10T18:17:27.283066902Z",
[...]
        "IPAM": {
            "Driver": "default",
            "Options": {},
            "Config": [
                {
                    "Subnet": "172.18.0.0/16",
                    "Gateway": "172.18.0.1"
                }
            ]
        },
[...]
        "ConfigOnly": false,
        "Containers": {
            "13dee2f...7f907": {
                "Name": "n2",
                "EndpointID": "1d2b53ec0...e398c3bbf312",
                "MacAddress": "02:42:ac:12:00:03",
                "IPv4Address": "172.18.0.3/16",
                "IPv6Address": ""
            },
            "89d2c008d9e6...049d5679a9a13ad": {
                "Name": "n1",
                "EndpointID": "30d1cd...9b5e246fd7b7fc133",
                "MacAddress": "02:42:ac:12:00:02",
                "IPv4Address": "172.18.0.2/16",
                "IPv6Address": ""
            }
        },
        "Options": {},
        "Labels": {}
    }
]
```


- [basic networking](https://runnable.com/docker/basic-docker-networking)



### Links
- [how-to-build-a-node-js-application-with-docker-quickstart](https://www.digitalocean.com/community/tutorials/how-to-build-a-node-js-application-with-docker-quickstart)