# Build image registry K3S

## Create new machine
`multipass launch --name registry --cpus 1 --mem 1G`

## Get informations

> multipass info registry

```Name:           registry
State:          Running
IPv4:           192.168.64.7
Release:        Ubuntu 18.04.4 LTS
Image hash:     fe3030939822 (Ubuntu 18.04 LTS)
Load:           0.42 0.13 0.05
Disk usage:     1001.5M out of 4.7G
Memory usage:   72.5M out of 985.7M```

## Run registry docker container
```
multipass --verbose exec ${registry_name} -- sudo -- sh -c "
  apt-get update
  apt-get install -y docker.io
  docker run -d -p 5000:5000 --restart=always --name registry registry:2
"
```
