# Découverte K3S

Suivi d'installation d'un cluster mini-kubernetes. Par curiosité je souhaite simuler des systèmes complexe.
J'aimerais découvrir de nouveaux concepts et apprendre des choses par cet apprentissage.

Ce que je partage ici n'est que des expérimentations, elles ne sont peut être pas poussées jusqu'au bout ni viable en prod.
Simplement des sujets que je souhaite débunker.



## **Outillage**
- [Multipass](https://multipass.run/docs/installing-on-macos)
- [K3S](https://k3s.io/)

---
## [**Multipass**](multipass-cmd.md)
---

## **Cluster K3S**

### Création des machines

```console
multipass launch -n basemaster --cpus 2 --mem 2G
multipass launch -n raiderone --cpus 2 --mem 2G
multipass launch -n raidertwo --cpus 2 --mem 2G
```

### Creation du master

```console
multipass --verbose exec basemaster -- sh -c "
  curl -sfL https://get.k3s.io | sh -
"
```

### Creation des noeud 2 et 3
Comme dit dans la [documentation](https://rancher.com/docs/k3s/latest/en/quick-start/).

`K3S_URL` Configure k3s en `worker mode` l'agent s'abonnera au master définit dans K3S_URL='https://$IP:6443' _(IP de basemaster)_.

`K3S_TOKEN` est le tocken d'auth stocké dans /var/lib/rancher/k3s/server/node-token du k3s master _(basemaster dans notre exemple)_.

_Il est possible d'utiliser les variables d'environnements_
```console
export TOKEN=$(multipass exec basemaster sudo cat /var/lib/rancher/k3s/server/node-token)

export IP=$(multipass info basemaster | grep IPv4 | awk '{print $2}')
```

### Création noeud 2
```console
multipass --verbose exec raiderone -- sh -c " curl -sfL https://get.k3s.io | K3S_URL='https://$IP:6443' K3S_TOKEN='$TOKEN' sh - "
```
### Création noeud 3
```console
multipass --verbose exec raidertwo -- sh -c " curl -sfL https://get.k3s.io | K3S_URL='https://$IP:6443' K3S_TOKEN='$TOKEN' sh - "
```

### Environnement k3s
Pour que kublectl(CLI kubernetes) puisse intéroger le k3s-master il est necessaire d'y passer un fichier décrivant l'environnement. _Avec l'ip du cluster et le token_ 🙂

Pour cela il est necessaire de copier localement la configuration du master et de remplacer l'IP locale par son IP réseau :
```
multipass exec basemaster sudo cat /etc/rancher/k3s/k3s.yaml > k3s.yaml
sed -i '' "s/127.0.0.1/$IP/" k3s.yaml
```

_sed -i '' "s/schema/remplaceent" <file>_

On renseignera la configuration a utiliser via : `export KUBECONFIG=./k3s.yaml`

## Descriptif des noeuds

```console
export KUBECONFIG=./k3s.yaml
kubectl top nodes

NAME         CPU(cores)   CPU%   MEMORY(bytes)   MEMORY%
basemaster   198m         9%     747Mi           37%
raidone      17m          0%     263Mi           13%
raidtwo      16m          0%     258Mi           12%
```


### Ressources
- https://medium.com/better-programming/local-k3s-cluster-made-easy-with-multipass-108bf6ce577c
- https://k33g.gitlab.io/articles/2020-02-21-K3S-01-CLUSTER.html
- https://rancher.com/docs/k3s/latest/en/quick-start/
- https://itnext.io/setup-a-private-registry-on-k3s-f30404f8e4d3