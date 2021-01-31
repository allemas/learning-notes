Création d'une instance mongodb avec docker & dockercompose 🚀

# **Mongodb**
_**Problèmes rencontrés** autour du système d'authentification et droits a la base de données._

## Déploiement via Docker-compose
```
version: '3'

services:
  mongo:
    image: mongo
    environment:
      - MONGO_INITDB_ROOT_USERNAME=**root**
      - MONGO_INITDB_ROOT_PASSWORD=**root**
      - MONGO_INITDB_DATABASE=test
    volumes:
      - ./etc/mongo-volume:/data/db
      - ./init-mongo.js:/docker-entrypoint-initdb.d/init-mongo.js:ro
    ports:
      - "27017:27017"
```

---

## Variables d'environnement
Ces variables créent un nouvel utilisateur : `MONGO_INITDB_ROOT_USERNAME`  `MONGO_INITDB_ROOT_PASSWORD`

**Cet utilisateur est crée dans la table : [`admin`](https://docs.mongodb.com/manual/core/security-users/#user-authentication-database) avec le role `ROOT`**

**Attention: l'initialisation de mongod se se base sur un fichier de configuration (docker-entrypoint)**

**si ces deux variables sont renségnées alors mongodb démarre avec le l'authentification obligatoire (voir `mongod --auth)`)**

---

## Initialisation d'une base de donnée avec système d'authentification

**Au lancement de mongodb les fichiers d'initialisation (//docker-entrypoint-initdb.d)sont exécutés dans l'ordre alphabetique.**
Si la variable d'environnement `MONGO_INITDB_DATABASE` est renseignée alors elle sera utilisée pour l'exécution de ces scripts.

```
db.createUser(
  {
    user: "auth_login",
    pwd: "pwd", // or cleartext password
    roles: [ { role: "readWrite", db: "db-project" } ]
  }
)
```

- [mongodb - Enable Access Control](https://docs.mongodb.com/manual/tutorial/enable-authentication/)
- [mongodb - Security](https://docs.mongodb.com/manual/security/)


## Authentification

Pour vous connecter il est possible d'utiliser :

```
$> mongo -u <login> -p <pwd> authentificationDatabase <db_name>

$> mongo -u <login> --authentificationDatabase <db_name>

// exemple
$> mongo -u auth_login --authentificationDatabase db-project
Enter your password: ...
```

Pour aller plus loins:
- [Encryption SSL](http://pierrepironin.github.io/docker-et-mongodb/#Lancer-le-server-MongoDB-en-mode-authentifie)


---

# Mongodb express

_**Problèmes rencontrés** authentification sur bdd mongo via mongo-express_

_> Ne pas se tromper dans les variables d'environnement pour disposer d'un accès root en dev (voir section variables d'environnement)_


## Déploiement via Docker-compose
```
  mongo-express:
    image: mongo-express
    restart: always
    environment:
      - ME_CONFIG_MONGODB_SERVER=mongo
      - ME_CONFIG_MONGODB_PORT=27017
      - ME_CONFIG_MONGODB_ENABLE_ADMIN=true
      - ME_CONFIG_MONGODB_ADMINUSERNAME=**root** <-- # Doit correspondre au compte root décrit plus haut
      - ME_CONFIG_MONGODB_ADMINPASSWORD=**root** <--
      - ME_CONFIG_BASICAUTH_USERNAME=dev
      - ME_CONFIG_BASICAUTH_PASSWORD=dev
    depends_on:
      - mongo
    ports:
      - "8888:8081"
```


## Authentification

Attention, a ne pas confondre `ME_CONFIG_MONGODB_ADMINUSERNAME` et `ME_CONFIG_MONGODB_AUTH_USERNAME`

**Les variables suivantes doivent être renseignés si `ME_CONFIG_MONGODB_ENABLE_ADMIN` est `false`**

Name                            | Default         | Description
--------------------------------|-----------------|------------
ME_CONFIG_MONGODB_AUTH_DATABASE | 'db'            | Database name
ME_CONFIG_MONGODB_AUTH_USERNAME | 'admin'         | Database username
ME_CONFIG_MONGODB_AUTH_PASSWORD | 'pass'          | Database password

**si `ME_CONFIG_MONGODB_ENABLE_ADMIN` est `false`** alors l'utilisateur définit va `ME_CONFIG_MONGODB_AUTH_USERNAME` et `ME_CONFIG_MONGODB_AUTH_PASSWORD` ne pourra pas voir toutes les bases de données.

Risque d'erreur : `MongoError: not authorized on admin to execute command { listDatabases: 1 }`


**Attention !** Si `ME_CONFIG_MONGODB_ENABLE_ADMIN` est a `true` alors, il sera possible d'effectuer des actions **critiques** via mongo-express.

_En dev :_ J'utilise `ME_CONFIG_MONGODB_ADMINUSERNAME` + compte root

## Variables d'environnement

	Name                            | Default         | Description
	--------------------------------|-----------------|------------
	ME_CONFIG_BASICAUTH_USERNAME    | ''              | mongo-express web username
	ME_CONFIG_BASICAUTH_PASSWORD    | ''              | mongo-express web password
	ME_CONFIG_MONGODB_ENABLE_ADMIN  | 'true'          | Enable admin access to all databases. Send strings: `"true"` or `"false"`
	ME_CONFIG_MONGODB_ADMINUSERNAME | ''              | MongoDB admin username
	ME_CONFIG_MONGODB_ADMINPASSWORD | ''              | MongoDB admin password
	ME_CONFIG_MONGODB_PORT          | 27017           | MongoDB port
	ME_CONFIG_MONGODB_SERVER        | 'mongo'         | MongoDB container name
	ME_CONFIG_OPTIONS_EDITORTHEME   | 'default'       | mongo-express editor color theme, [more here](http://codemirror.net/demo/theme.html)
	ME_CONFIG_REQUEST_SIZE          | '100kb'         | Maximum payload size. CRUD operations above this size will fail in [body-parser](https://www.npmjs.com/package/body-parser).
	ME_CONFIG_SITE_BASEURL          | '/'             | Set the baseUrl to ease mounting at a subdirectory. Remember to include a leading and trailing slash.
	ME_CONFIG_SITE_COOKIESECRET     | 'cookiesecret'  | String used by [cookie-parser middleware](https://www.npmjs.com/package/cookie-parser) to sign cookies.
	ME_CONFIG_SITE_SESSIONSECRET    | 'sessionsecret' | String used to sign the session ID cookie by [express-session middleware](https://www.npmjs.com/package/express-session).
	ME_CONFIG_SITE_SSL_ENABLED      | 'false'         | Enable SSL.
	ME_CONFIG_SITE_SSL_CRT_PATH     | ''              | SSL certificate file.
	ME_CONFIG_SITE_SSL_KEY_PATH     | ''              | SSL key file.