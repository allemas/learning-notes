# Socle Front React

## Commandes

### `npm start`

Démarre l'application en mode développent<br />
Accéssible a l'adresse  [http://localhost:3000](http://localhost:3000)

### `npm test`
Documentation [running tests](https://facebook.github.io/create-react-app/docs/running-tests)

### `npm run build`

Construit l'application pour un environnement de production.<br />
Documentation [deployment](https://facebook.github.io/create-react-app/docs/deployment)

### `npm run eject`

**Note: this is a one-way operation. Once you `eject`, you can’t go back!**

If you aren’t satisfied with the build tool and configuration choices, you can `eject` at any time. This command will remove the single build dependency from your project.

Instead, it will copy all the configuration files and the transitive dependencies (webpack, Babel, ESLint, etc) right into your project so you have full control over them. All of the commands except `eject` will still work, but they will point to the copied scripts so you can tweak them. At this point you’re on your own.

You don’t have to ever use `eject`. The curated feature set is suitable for small and middle deployments, and you shouldn’t feel obligated to use this feature. However we understand that this tool wouldn’t be useful if you couldn’t customize it when you are ready for it.

## Structure du projet

- `src/` contient le code de l'application (api, components, containers, configuration, docs etc.)
- `build/` source du projet une fois construit

### src/containers
Le dossier `src/containers` contient les composants de l'application décrivant comment le système fonctionne, ces éléments s'appuient sur les composants présent dans `src\component` (par exemple: HomePage, AuthLogin, AdminPannel etc.)
Ces éléments sont fait construire des éléments fonctionnels, peuvent avoir un sytème d'etat (state) et être couplé a redux.

### src/components
Le dossier `src\component` contient la liste des composants graphique de l'application. Ils n'ont aucune notion du métier de l'application
Ces composants ne sont pas connecté a un système de management d'états (redux)

### src/modules
Le dossier `src/modules` contient les composants portables FDJ.

## Bonnes pratiques

### Organisation du projet

#### Composant graphique
Les composants graphiques seront situées dans le dossier src/components, ils ne seront pas abonnés a un manageur d'etats.
Ils seront dans la mesure du possible non couplé a d'autres components, s'ils devaient l'être les dépendances seront dans le meme dossier

#### Les Containers
Un container est un element graphique composé de plusieurs components. L'agreggation des différents components se fait dans un container.
Un container pourra être abonné a un gestionnaire d'état. Un container peut représenter une page, ou un élément graphique complexe.
Il est conseillé d'éviter au maximum le couplage entre différents containers.

#### Les API
La gestion des API sera faite dans le dossier API, chaque API seront isolées et pourront au besoin fonctionner en synchrone ou asynchrone (async / promise)

#### La configuration
La configuration technique de l'application sera positionnée dans le dossier config.
il est conseillé de séparer au maximum les différentes configuration ex: keycloak.config.js, esb.technical.config.js etc.

#### Modules
Les composants graphique (simples ou complexes) spécifiques *devant etres partagés* seront placés dans le dossier modules.
Ces containers seront utilisés dans les containers situés dans le dossier containers.


### Convention de nommage
- Utilisez le nom de fichier comme nom de composant.
- Utilisez PascalCase pour les noms de fichiers (LoginComponent)
- Les événements React sont nommés à l’aide de camelCase et commencent par ‘on’ (par exemple, onSubmitButtonClick).
- Les gestionnaires d’événements doivent commencer par ‘handle’ (par exemple, handleSubmitButtonClicked).
- Les fonctions doivent être nommées pour ce qu’elles font et non comment elles le font


### Déstructurer
Il est possible d'extraire les propriétés d'un objet ou des éléments d'un tableau.

```
return &lt;GreatingsUser title={this.props.title} options={this.props.attributes} isUserLoginIn={this.state.isLoggedIn}/>;
```

```
//clean
const {title, attributes} = this.props;
const {isLoggedIn} = this.state;
return &lt;GreatingsUser title={title} options={attributes}  isUserLoginIn={isLoggedIn}/>;
```

```
//dirty
const splitLocale = locale.split('-');
const language = splitLocale[0];
const country = splitLocale[1];
```

```
//clean
const [language, country] = locale.split('-');
```

### Gestion des class css

classnames est un excellent package pour générer des noms de classes de composants. En pratique, il existe de nombreux cas où différents styles doivent être appliqués à même composant. Pour éviter l’abondance de conditions dans votre code, qui alourdisse la lisibilité, vous pouvez préparer les noms de classe à l’aide de ce package.

```
//dirty
return &lt;button className={‘btn ’ + (isPressed? 'btn-pressed': (!isPressed &amp;&amp; isHovered) ? 'btn-over':’’)}>{ label }&lt;/button>;
```

```
// clean
const btnClass = classnames('btn', {
      'btn-pressed': isPressed,
      'btn-over': !isPressed &amp;&amp; isHovered
    });
return &lt;button className={btnClass}>{label}&lt;/button>;
```

## Stack technique

-  [React](https://facebook.github.io/react/)
-  [React Router](https://github.com/ReactTraining/react-router)
-  [Redux](http://redux.js.org/)
-  [Reselect](https://github.com/reduxjs/reselect)
-  [classname](https://github.com/reduxjs/reselect)
-  [react-testing-library](https://github.com/kentcdodds/react-testing-library)
-  [ESLint](http://eslint.org/)
