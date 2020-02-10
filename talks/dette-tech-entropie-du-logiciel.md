# [Dette technique & entropie du logiciel ](https://www.youtube.com/watch?v=R8QYVZIVSBE)

La taille du logiciel ne compte pas
Il est necessaire de connaitre une grande quantité d'information pour ne pas "mal développer"

Cette problématique réside sur deux points :
- L'interdépendance entre module oblige a la mémorisation du contexte commun
- Si l'interdépendance est forte quand un module meur --> le logiciel s'écroule

## Complexité

3 grand types :
- Complexité essentielle : Complexité du process métier (par ex)
- Complexité obligatoire : Complexité des briques qui permet de fonctionner (ex: API -> HTTP)
- Complexité accidentelle : Ne devrait pas être la, rajouté en plus.

### Complexité

- N'augmente pas lineairement en fct du nombre de features
- Plutot forme polynomiale

Alan Kay explique que la complexité est spécifique a l'ouvrage qu'on développe : Cabane -> immeuble
Suivant les ouvrages : on adresse pas les memes problématiques

La complexité accèlere l'entropie : _Capacité d'un système a se désordonner_ et fait chuter la qualité du logiciel

### DRY et ses limites
Un objet identique dans deux modules du système n'est pas forcément paratageable

Ils peuvent quand meme être différents:
- Par leurs cycles de vie
- Objectif métier différents

Mélanger les cycles de vie et les objectifs est vecteur decouplage et donc de bug en cas de changements.

## Dette technique

Avoir un time to market court : simplifier la conception du logiciel pour aller en contact avec le marchier plus rapidement. *c'est un gain pour l'oganisation*

Problèmes oubliés :
- Une dette ca se rembourse
  - Temps de reboursement : on *redéveloppe* la fonctionnalité
  - le PO on accepte de redévelopper 2 fois la fonctionnalité
- C'est les développeurs qui décident quand rembourser

### Agilité

Problème très fréquent dans les équipes agiles.
Pour répondre a des problématiques de delivery : on contracte de la dette (principalement : en supprimant les process qualité).

*Problème* : au prochain sprint le mode expériemental des devs est encore en place et se perpétue de sprint en sprint --> *bloquage* : Soit correction de bugs soit production de dette technique


## symptome != cause

Cause :
- Organisation
- Culture
- Humain

### Over ingenieurie

Développement très complexe pour répondre a un problème classique.
_Question a se poser_ : est-ce que l'outil répond a mon besoin ?

_Whenever i see job title like React Developper, I think anout Hammer carpenter or spoon cook. @salomvary_

### cargo culting
On va chercher les effets sans se demander d'ou viennent les causes. Notre industrie est devenu experte dans cette pratique.

Beaucoup d'équipes intègrent des outils et des concepts sans réelement les tester.
Quand on leurs pose la question : _parce que Netflix le fait_
Souvent on a pas les moyens de maintenir ces système en production _alors que netflix : oui_.

_La plus forte cause d'aliénation dans le monde contemporain réside dans cette méconnaissance de la machine,_
_qui n'est pas aliénation causé par la machine mais par la non connaissance de son essence @simondon_

_This second is the most dangerous system a man ever designs. [...] The general tendency is to over-design_
_the second system, using all the ideas and frills that were cautiously sidetracked one the first one. - Brooks_
Explique généralement pourquoi un projet de refonte rate : sur le second systeme on se lache

## Frameworks
Projet ou le métier est entré dans le frameworks de force. Il devient invisible dans le systeme.
Génère un bigbang technique dans le cas de virages dans le métier.

## Frameworks entreprise
Dépendance très lourde dans les projets, ne modélise pas/mal le métier.
Couplage a travers TOUS les projets de l'entreprise
Bad idea

## Solution spécifique - métier
Autrement appelé DDD : on essaie de piloter l'architecture logicielle par les besoins métiers

_Une des pire dette est la dette fonctionnelle : quand le métier finit par s'aligner sur une mauvaise applicaiton @ygrenzinger_

Comment les entreprises tech arrivent a casser des projets : parce que ces entreprises développement des application capable d'absorber le **metier** et *non* mettre l'application dans le métier.


## decouvrir et non inventer
En tant que developpeur on est null en divination, toujours prendre le temps de découvrir la généricité.
Si on développe plusieurs fois le meme métier alors on peut penser a générer
- examplemaping
- eventstorming

## Legacy
Code that's too scary to update and too profitable to delete.
On produit énormément d'énergie pour maintenir en vie le logiciel.


## Comment ne plus avoir peur de changer le code
Dépend du contexte :
- organisationnel
- pratique
- etc..

Les devs créent de la complexité quand ils se projettent dans le futur dans le developpement.
On réussit a ré ecrire du code quand on a plus peur de le changer : **TDD**

_We tend to get sidetracked by tools when we should really be thinking about what our tools are supposed to achieve. Chef instead of recepice book user_ @_edejong
