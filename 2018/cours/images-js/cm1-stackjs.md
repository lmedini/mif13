<!-- $theme: gaia -->
<!-- page_number: true -->



# Programmation Web Avancée et Mobile

### CM 1 : Stack JavaScript

Aurélien Tabard - Lionel Médini


--- 

## But de ce cours

- Introduire les outils d'aide au développement JS
  Quelques [rappels sur JS au besoin](http://kmicinski.com/cmsc245/slides/javascript-intro.pdf).

- Vous rendre plus efficaces pour :
  - développer
  - packager une application Web
  - débugger


--- 

## Contenu de ce cours

- Grands principes d'un outil
- Lien vers le site / la doc
- Remarques sur l'utilisation pratique


---

## JavaScript c'est cool

Parfois un peu trop...

![center 75%](gag_cm_stack_js_mif38.png)

- [Wat par Gary Bernhardt (vidéo)](https://www.destroyallsoftware.com/talks/wat)
- [How it feels to learn JavaScript in 2016](https://hackernoon.com/how-it-feels-to-learn-javascript-in-2016-d3a717dd577f)

--- 

##  [Node.js](http://nodejs.org/)	 ![80%](images-js/nodejs.png)

Plateforme d'exécution basée sur le moteur Chrome

- Permet de :
	- mettre en place de “grosses” applications
	  - en JS
	  - modulaires
	- programmer dans le même langage côté serveur et côté client


--- 

## Quelques différences 
avec du JS côté navigateur

- Pas de Browser Object Model (BOM)
- Paquets spécifiques
- Mode de gestion des modules : CommonJS

---

## [npm](http://npmjs.com/) ![12%](images-js/npm.png)

- Gestionnaire de paquets pour node
- S'utilise “à la” apt-get
  - localement : `npm install <package>`
  - globalement : `npm install -g <package>`
- Description de l'application dans un fichier package.json

---

## Gestion des dépendances

**Require** 
- Chargement des dépendances dans les modules
- S'utilise 
  - côté navigateur (utilise [require.js](http://requirejs.org/) ou d'autre méthodes)
  - côté Node (vient avec sa propre commande require)
- Configuration en JSON 

--- 

## ![20%](images-js/bower.png) [Bower](http://bower.io/)

- Gestionnaire de paquets applicatif côté client
- Description de l'application dans un fichier bower.json
- Exécution : bower install
- Différence avec NPM :
	- Optimisé pour le front-end
	- Meilleure gestion des dépendances croisées
 Graphe de dépendance plat : on télécharge pas jquery 2x côté client

---

## ![20%](images-js/grunt.png) [Grunt](http://gruntjs.com/)

- Task manager / runner
- S'appuie sur un ensemble de plugins (cf. Maven)
- Configuration du projet : Gruntfile
- Utilisation : lancement des tâches via la Command Line Interface (CLI)


Voir aussi [Gulp](https://gulpjs.com/)

---

## ![50%](images-js/yeoman.png) Yeoman 

- Outil de “Scaffolding” d'applications Web
- Permet de créer rapidement un projet avec de nombreux composants
- 2 possibilités
	- CLI
    - Bibliothèque de générateurs prêts à l'emploi


--- 
## Webpack

![center](images-js/what-is-webpack.png)

--- 
## Webpack

1. Permet la gestion de module (require / import)
2. Agnostique au type de modules : AMD, UMD, CommonJS etc.
3. Traite les assets statiques comme des modules (CSS, images)
4. Découpe le code pour optimiser le chargement
5. Injection de dépendance et multi-compilation
6. S'intègre aux autres outils de build (Grunt/Gulp/etc)


--- 

## Webpack

![120%](images-js/webpack.png)


via [Getting started with Webpack](https://webpack.js.org/) 


--- 

## Webpack debugging

Problème : tout est optimisé / minifié

Solution : création d'une [source-map](http://blog.teamtreehouse.com/introduction-source-maps) liant code bundlé au code "réel".

[Intro au debbuging Vuejs](https://medium.com/@BjornKrols/a-basic-introduction-to-debugging-vue-applications-using-breakpoints-2ef76ce419f2)


--- 
## Autres outils JS

- Framework node : [Express](http://expressjs.com/)
- Tests : [Mocha](https://mochajs.org/) ou [Jasmine](https://jasmine.github.io/)
- Vérification de code : [ESLint](https://eslint.org/)
- Compilation ES6 → ES5 : [Babel](https://babeljs.io/)


---
# Modularité

---


---
## Modularité Principes

- isolation
- réutilisabilité
- gestion des dépendances
- téléchargement

---

## Différentes solutions
- Asynchronous Module Definition (AMD)
- CommonJS (CJS)
- Universal Module Definition (UMD)
- ES6 modules

Référence : http://addyosmani.com/writing-modular-js/ 

---

## Deux approches

- Approche serveur
	- un répertoire node_modules avec une arborescence de dépendances
	- chaque module peut avoir ses propres dépendances, avec des versions différentes
- Approche client
	- un répertoire avec des dépendances “à plat”
	- les dépendances partagées doivent avoir les mêmes versions
    - il faut gérer les conflits

Reférence : http://exploringjs.com/es6/ch_modules.html#sec_modules-in-javascript

---

## Modules et sécurité

Lire:

[I’m harvesting credit card numbers and passwords from your site. Here’s how.](https://hackernoon.com/im-harvesting-credit-card-numbers-and-passwords-from-your-site-here-s-how-9a8cb347c5b5)