# Prise en mains de Multipass - Canonical

Il existe une multitupde d'outils pour virutaliser des machines (VM). Aujourd'hui j'ai décidé pour mes atelier et mes expérience d'utiliser Multipass, un outil de la team [Canonical](https://multipass.run/).
Multipass est un outil de construction de VMs sous ubuntu, je compte utiliser cet outil pour construire très rapidement un environnement de developpement.

## Lancer une instance
> multipass launch --name <VM_name>

## lister toutes les instance
> multipass list

## Arreter / démarrer une instance
> multipass stop <VM_name>
> multipass start <VM_name>

## Supprimer une instance
Attention, lorsque vous supprimez une instance elle ne l'est pas réellement.
Il faut d'abord la supprimer et ensuite purger les Vms.

### Supprimer
> multipass delete <vm_name>
### Purger
> multipass purge

## Exécuter commande

Dans cet exemple installation de k3s
```
multipass --verbose exec <vm_name> -- sh -c "
  curl -sfL https://get.k3s.io | sh -
"
```

`multipass --verbose exec node_name -- sh -c "ls /"` : lance une commande sur une machine

## N'hésitez pas a scripter !
