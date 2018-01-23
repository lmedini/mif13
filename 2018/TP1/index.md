## TP 1 : Mise en place d'une stack JavaScript

**Répondre au [formulaire en parallèle de la réalisation du TP](https://docs.google.com/forms/d/1_E5Cgg5tn6-Tx-hfDcQl6CrV-Gxlzk_CxcIjZkjtdOs/).** Il est simple et peut être réalisé dans le temps du TP, il est à remplir au plus tard à minuit.

### Présentation de l'application

Nous allons construire une application de conseil en mobilité (comme [Citymapper](http://citymapper.com/)) en utilisant [Vue.js](http://vuejs.org/) et l'API de [navitia.io](https://www.navitia.io/)

Cette application sera une Single Page Application (SPA), développée principalement côté client, avec un serveur très léger. Client et serveur seront codés en JavaScript.

### Outils

Nous conseillons [Webstorm](https://www.jetbrains.com/webstorm/) comme IDE (vous pouvez demander une clé étudiant), ou un éditeur de code avancé (Emacs, [Atom](https://atom.io), [Visual Studio Code](https://code.visualstudio.com/), Vim...)

Nous utiliserons intensivement [npm](https://www.npmjs.com/), le gestionnaire de paquet pour JavaScript. Installez [nodejs](https://nodejs.org/en/) pour avoir npm sur votre machine.

Nous utiliserons [Webpack](https://webpack.github.io/) (plutôt que Gulp, Grunt, ou browswerify) pour gérer le processus de build des projets de l'UE.

Les logiciels nécessaires sur ce TP et les suivants sont ceux présentés dans le CM stack JS. Ils sont pré-installés sur des VMs que nous pouvons instancier à la demande. Ces machines ne sont accessibles que depuis l'intérieur de l'université.

Pour utiliser ces VMs, le plus simple est :
- d'ouvrir une console en ssh : ssh login@192.168.74.XXX
- d'éditer votre code sur votre machine locale à l'aide de votre IDE, et de le pusher sur votre repo quand vous voulez le tester
- de cloner et votre dépôt et redémarrer votre serveur sur la VM
- de tester avec le navigateur de votre machine locale


### Mise en place d'un projet simple Vue.js + Express

Pour ce premier TP nous allons créer un projet Vue.js simple servi par un serveur Nodejs et le framework simple [Express](http://expressjs.com/).


**Répondre au [formulaire en parallèle de la réalisation du TP](https://docs.google.com/forms/d/1_E5Cgg5tn6-Tx-hfDcQl6CrV-Gxlzk_CxcIjZkjtdOs/).**

#### 1. Créer un projet Vue.js (partie client)

Commencez par créer un projet (vide) sur la forge, et clonez le sur votre machine.

Créez un fichier README.md décrivant le projet et le processus de build, ainsi qu'un fichier .gitignore :

```
.DS_Store
node_modules/
dist/
*.log

# Fichiers de votre IDE
```

Installez globalement le Command Line Interface (CLI) de Vue [vue-cli](https://github.com/vuejs/vue-cli) qui nous sera utile pour créer des projets Vuejs :

```
npm install -g vue-cli
```

Nous pouvons maintenant créer un projet Vue.js (= partie client) simple qui s'appuiera sur l'outil de build webpack :

```
vue init webpack-simple NOM_PARTIE_CLIENT
```

Suivez les instructions de vue-cli, en vous plaçant dans le répertoire client projet pour lancer le projet.

La commande `npm install` va installer dans le dossier `node_modules/` les dépendances définies dans le fichier `package.json` à votre projet Vue.

La commande `npm run dev` va lancer la commande `dev` telle que définie dans `package.json`.

Tester, et *verser les changements sur la forge*.

#### 2. Créer un serveur Express (partie serveur)

À la racine du projet créer un dossier `serveur`.

Se placer dans le dossier et créer un fichier de configuration pour nodejs en tapant `npm init`, suivre les instructions.

Nous allons maintenant rajouter la dépendance à `Express` dans le partie serveur. Pour cela, exécuter :

```
npm install --save express
```

Observez les changements dans `package.json`, la dépendance a été rajoutée avec le numéro de version actuel.

Rajouter une dépendance à [eslint](https://eslint.org/) et à [nodemon](https://nodemon.io/).


Rajouter une section devDependencies dans le fichier `package.json` si elle n'existe pas encore, et y déplacer les dépendances qui ne sont utiles que pour le développement :

```json
"devDependencies": {
 à compléter
}
```


Éditer un fichier principal (nous l'appelerons `app.js` par la suite du sujet) de votre application côté serveur :

```javascript
const express = require('express')
const app = express()

app.get('/', (req, res) => res.send('Hello World!'))

app.listen(3000, () => console.log('Example app listening on port 3000!'))
```

Lancer l'application avec `node app.js` (ou tout autre nom de votre fichier js).

Dans la partie script rajouter un racourci pour lancer le projet plus facilement :

```json
"scripts": {
  "start": "node app.js"
},
```

Compléter la partie script pour intégrer nodemon et eslint :

```json
"scripts": {
  "start": "node app.js",
  "nodemon": "nodemon app.js --exec 'npm run lint && node'",
  "lint": "eslint *.js"
},
```

Valider la syntaxe de votre code avec `eslint` (effectuer les configurations nécessaires), et corriger le code au besoin :

```
npm run lint
```

Quand seule une erreur liée à l'utilisation de la console reste, rajouter une exception en haut de votre fichier :

```javascript
/*eslint no-console: ["error", { allow: ["log", "warn", "error"] }] */
```

Lancer maintenant le projet avec nodemon : tout changement dans app.js sera automatiquement validé via eslint, puis le serveur rechargé.

```
npm run nodemon
```

**Tester et commiter votre code.**


#### 4. Lier client et serveur

On va maintenant servir les fichiers client depuis notre serveur express.

Dans app.js nous allons maintenant servir le fichier index.html créé par vuejs :

```javascript
app.get("/", (req,res) => {
	res.sendFile(path.join(__dirname+"/../client/index.html"))
})
```

Charger la page dans le navigateur et ouvrir la console du navigateur. Qu'est ce qui chargé ? Et qu'est ce qui ne l'est pas ?

On va maintenant gérer les fichiers manquant. Ces derniers sont statiques (il ne changent pas). On peut donc faire un lien "dur" vers le dossier qui les contient.

```javascript
app.use("/dist", express.static(path.join(__dirname, "/../client/dist")))
```

**Tester.**

Si la page ne s'affiche toujours pas, vérifié qu'un dossier dist est bien présent côté client. Ce dossier est créé lorsque que l'on lance un bundling webpack pour la production. Effectuer cette opération le cas échéant.

**Tester et commiter votre code.**

#### 4. Debugging avec vue-devtools et postman

Installer l'addon [vue-devtools](https://github.com/vuejs/vue-devtools) dans votre navigateur.

Tester sur la page suivante : [http://todomvc.com/examples/vue/](http://todomvc.com/examples/vue/)

<!-- Installer [Postman](https://www.getpostman.com/) pour tester des endpoints d'API. -->
Créer un compte chez [navitia.io](https://www.navitia.io/) pour tester leur API [depuis leur plateforme](http://canaltp.github.io/navitia-playground/), puis avec Postman.

**Tester et commiter votre code.**

#### 5. OPTIONNEL : C.I.

Configurer une C.I. dans la forge (GitLab), pour déployer votre projet sur une VM ou sur Heroku. Si nous avons le temps, nous reviendrons là dessus lors des prochain TPs.

#### 6. Fin


**Le [formulaire](https://docs.google.com/forms/d/e/1FAIpQLSdK7N7A25PJguIRAuN6pTf3ng_6crzKhL755cnb23f5fY02Lw/viewform?usp=sf_link) est à terminer pour minuit**. Au prochain TP nous mettrons en place la même stack mais pour le "vrai" projet qui sera développé tout au long des TP de l'UE.


<!-- #### Questions

- A quoi correspond le dossier node_modules ?
  - aux fichiers de configuration de nodejs
  - aux dépendances du projet
  - aux modules du projet
  - au résultat de la compilation du projet

- A quoi correspond le dossier dist ?
  - aux fichiers de configuration de nodejs
  - aux dépendances du projet
  - aux modules du projet
  - au résultat de la compilation du projet


- Dans le fichier package.json, Pourquoi la `dependencies`, n'a pas besoin de tous les modules spécifiés dans `dev-dependencies` ?

- Pourquoi node_modules contient il tant de modules alors que le fichier app.js ne fait que quelques `require()` ?

- À quoi sert eslint ?
  - à compiler le code
  - à valider la syntaxe du code
  - à tester le code
  - à minifier le code

- Comment réutiliser une variable définie dans le fichier package.json plus tard dans le fichier. Par exemple pour accéder au numéro de version définit comme cela : `"version": "1.0.0"` -->
