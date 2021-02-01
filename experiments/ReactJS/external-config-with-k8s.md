# Create react external configuration with k8s

## Problème 
Partage de configuration applicative d'une meme application react sans rebuild

## Methode rapide 
Au lancement de l'application charger un fichier de configuration (via GET) et propager la configuration a toute l'application 

- **Creation du fichier de configuration via configmap**
- dépose du fichier a la racine du projet


## La cible
être en mesure de déployer un ensemble de fichiers de configuration facilement au déploiement de l'application.

Roadmap 
- Créer un volume configmap dans k8s 
- Ajouter le volume a disposition du pod

Creation de la configmap 
```
# -- configmap --
apiVersion: v1
kind: ConfigMap
metadata:
  name: xx-xxx-xx-configmap
data:
  features.json: |{
      param: "val" 
  }
```

utilisation de la configmap


  extraVolumes:
    - name: volume-name
      configMap:
        name: xx-xxx-xx-configmap
  extraVolumeMounts:
    - name:  volume-name
      mountPath: /<path>
      subPath: features.json
      readOnly: true






# Links 
- https://stackoverflow.com/questions/49579028/adding-an-env-file-to-react-project
- https://www.newline.co/fullstack-react/30-days-of-react/day-27/
- https://medium.com/@dekauliya/adding-external-config-to-static-react-app-with-docker-and-kubernetes-in-ci-cd-96e988561096
- https://www.jeffgeerling.com/blog/2018/deploying-react-single-page-web-app-kubernetes
- https://stackoverflow.com/questions/49975735/rendering-an-environment-variable-to-the-browser-in-a-react-js-redux-production/49989975#49989975
