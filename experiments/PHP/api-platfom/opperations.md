# API platform - Opérations

API platform propose d'automatiquement générer le CRUD de vos entités avec une API.

C'est très gros gain de temps quand vous avez a besoin de rapidement creer un système avec persistance. Personnellement je m'en sert pour tester/valider mes hypothèses. L'approche "oppération" permettra d'étendre les api et spécifier vos spécificités.


Les verbes HTTP les plus couramment utilisés sont POST, GET, PUT, PATCH et DELETE. Ces verbes correspondent aux **opérations** de création, de lecture, de mise à jour et de suppression (ou CRUD).
Suivant les besoins, il arrive que nous devions surcharger ces opérations native a APIPLatform. _par exemple: pour publier un evenement dans un message broker quand on modifie une entité du système._

## Configurer les oppérations

La configuration des oppérations se fait par les annotations @ApiResource, en amont des entités. `collectionOperations` et `itemOperation` permettent de défnir quelles ressources diponibles.

Exemple ci dessous, on ne rend accéssible qu'uniquement les opérations GET sur les entités de type User
```
/**
 * ...
 * @ApiResource(
 *     collectionOperations={"get"},
 *     itemOperations={"get"}
 * )
 class User
 ```

Il existe deux types d'oppérations `collectionOperations` et `itemOperation`

`collectionOperations` Sont par défaut configuré avec : GET et POST et définissent les oppérations disponible  pour une **collection** d'entitée. Généralement ces opérations sont exécutés quand nous demandons au système **plusieurs** resultats (entités).

`itemOperation` Sont par défaut configuré avec : GET et POST et DELETE et définissent les oppérations disponible pour **une** entité uniquement

**exemple: pour une collection de livres.**
`collectionOperations` par défaut est configuré avec GET et POST. Permet donc de créer un livre et de l'ajouter a la collecter et de récupérer un ou plusieurs livres.

`itemOperation` par défaut est configuré avec GET et PUT et DELETE . Permet d'éffectuer des oppérations sur un livre uniquement. Le récupérer, le modifier ou le supprimer.


_Informations:_
- `collectionOperations` et `itemOperation` sont complètement indépendants il n'est **pas** necessaire de les définirs tous les deux.
- `collectionOperations` Si non définit automatiquement configuré avec les valeurs GET et POST


## Pour rajouter un endpoint a une ressource :
[documentation ici](https://api-platform.com/docs/core/operations/)


- Mettre a jour la section `@ApiRessource()` en ajoutant dans la section correspondante (`collectionOperations` ou `itemOperation`) le code suivant :
```
/**
 * @ApiResource(
 *     [item/collection]perations={
 *          .....
 *         "get_weather": {                     <-
 *             "method": "GET",                 <-
 *             "path": "/places/{id}/weather",  <-
 *             "controller": GetWeather::class  <-
 *         }                                    <-
 * }, collectionOperations={"get", "post"})
 */
```

*Note contextuelles*
- Si on ajoute cette annotation dans `collectionOperations` nous pouvosn récupérer **UN ou PLUSIEURS** elements
- Si on ajoute cette annotation dans `itemOperation` nous pouvons récupérer **UN seul** element de plus la route aura comme prérequis un identifiant.



## Creation d'une opération

Api platform utilise l'approche (ADR)[https://github.com/pmjones/adr] pour les oppérations dérière les ressources d'API.

L'autowriring abonne toutes les classes comme services "oppération"




# Tips
- Creer une oppération avec une information
