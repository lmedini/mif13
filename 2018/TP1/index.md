## TP 1 : Mise en place d'une stack JavaScript

### Présentation de l'application

Nous allons construire une application de conseil en mobilité (comme [Citymapper](http://citymapper.fr/)) en utilisant [Vue.js](http://vuejs.org/) et l'API de [navitia.io](https://www.navitia.io/)

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
- de tester avec le navigateur de votre machnie locale


### Mise en place d'un projet simple Vue.js + Express

Pour ce premier TP nous allons créer un projet Vue.js simple servit par un serveur Nodejs et le framework simple [Express](http://expressjs.com/).


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

Nous pouvons maintenant créer un projet Vue.js simple qui s'appuiera sur l'outil de build webpack :

```
vue init webpack-simple client
```

Suivez les instructions de vue-cli pour lancer le projet.


#### 2. Créer un serveur Express (partie serveur)



#### 3. Déployer

Pousser le code


#### 4. Fin

Ce TP est à terminer pour dimanche. Au prochain TP nous mettrons en place la même stack mais pour le "vrai" projet qui sera développé tout au long des TP de l'UE.
