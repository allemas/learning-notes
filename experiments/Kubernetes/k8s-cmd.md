# Kubectl

## Remove all pods
> kubectl delete --all pods

## Remove Application
>kubectl delete -f ./kube/deploy.yaml

## Create namespace
Allow to separate pods and environements. Usefull if you separate your work by team or project.
> kubectl create namespace <name_space>

# Apply and specify namespace
```console
export KUBECONFIG=../create-cluster/k3s.yaml
kubectl apply -f ./kube/deploy.yaml -n training
```
