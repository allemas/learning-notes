# Dockerfile

## Build
`docker build -f <dockerfile_file> -t <tag/name>`


## Dockerfile
### Example
```
FROM <os>:<version>
RUN apt-get update && \
    apt-get install <binary> -y

EXPOSE <port>
CMD ["<cmd>", "<arg1>", "<arg2>"]
```
