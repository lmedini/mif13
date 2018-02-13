## TP 2 : Composants, Routes, et Templates Vue.js

### Présentation de l'application

Nous allons construire une application de conseil en mobilité (comme [Citymapper](http://citymapper.com/)) en utilisant [Vue.js](http://vuejs.org/) et l'API de [navitia.io](https://www.navitia.io/)

Cette application sera une Single Page Application (SPA), développée principalement côté client, avec un serveur très léger. Client et serveur seront codés en JavaScript.

### Outils
Voir le [TP précédent](../TP1).

Visual Studio Code, combiné aux modules Vetur, ESLint et de debug navigateur est un bonne combinaison.


### Objectifs
Ce TP vise à se familiariser avec les templates Vue et la notion de route.

Nous allons construire le squelette d'une application qui reprend les éléments suivants : 

![wireframes]({{"wireframes.png"}})


### Mise en place d'un projet Vue.js avancé

Créer un nouveau projet Vue.js en utilisation `vue init`. Cette approche crée beaucoup de boilerplate (= code de mise en place), mais a l'avantage d'offrir un projet prêt à l'emploi et de se concentrer sur la logique de l'application.

```
vue init webpack nom_de_lapplication
```

Répondre aux questions de la façon suivante :
- `Vue build` : `standalone`
- `Install vue-router?` : `Yes`
- `Use ESLint to lint your code?` : `Yes`
- `Pick an ESLint preset` : `Standard`
- `Set up unit tests` : `Yes` (on verra plus tard).
- `Pick a test runner` : noTest
- `Setup e2e tests with Nightwatch?` : `No`
- Should we run `npm install` for you after the project has been created? : `yes`


*Explorer le projet créé (regarder les fichiers invisibles)*

##### Questions 
- Pour chaque fichier ou dossier à la racine expliquer à quoi il correspond en une phrase
- Quelle est la commande pour assembler le projet en mode développement ?
- Quelle est la commande pour assembler le projet en mode production ?
- Dans quel fichier sont définies ces commandes ?

### Versioner

Éditer le fichier `README` pour qu'il contienne les noms, prénoms et numéro d'étudiant du projet. 

Ne garder que les instructions de build qui sont utiles (et valides). 

Rajouter une description du projet.

**Versioner**



### Composant principal

Les applications Vue sont structurées autour de [composants](https://vuejs.org/v2/guide/components.html) 

`App.vue` est le composant parent qui contiendra les autres.

Modifier `HelloWorld.vue` pour avoir une structure proche du premier écran (A) (renommer le fichier pour que son nom se rapporte à sa fonction).


### Ajout de nouvelles routes et des composants associés

Nous allons maintenant rajouter des routes correspondant à chaque écran.
Le code suivant permet de créer une route Vue (utilisant de #).
```html
    <router-link to="/route">nom du lien</router-link>
```

1. Créer des routes et ajouter des pointeurs vers ces routes :
- *Autour de moi* pointera sur une route `/aroundme`
- *Ajouter* pointera sur une route `/myaddresses`

2. Créer les composants correspondants aux routes

3. Tester que les routes fonctionent. Versioner.

### Composant *AroundMe*
1. Créer un composant simple correspondant à la vue (B) des wireframes.

2. Pour le moment ce composant sera constitué d'un titre et d'une iframe contenant une google map centrée sur le batîment Nautibus. 

3. Rajouter un lien permettant de revenir à l'écran d'accueil

4. Tester le composant, les routes, puis versioner.

### Composant *MyAddresses*
Ce composant est plus complexe, il va permettre d'ajouter et de stocker les adresses préférées de l'usager.

Il est composé de 3 sous composants :
- Un composant de liste d'adresses (qui pourra être réutilisé sur la page d'accueil).
- Un composant affichant une adresse
- Un composant d'ajout d'adresse

##### Composant liste d'adresses

Créer un composant `AddressList` qui contienne une liste d'adresse:

```html
<template>
  <div>
    <ul>
        <li> Adresse 1 </li> 
        <li> Adresse 2 </li> 
        <li> Adresse 3 </li> 
    </ul> 
  </div>
</template>

<script type = "text/javascript" >

export default {
};
</script>
<style>
</style>

```

Créer un compostant `MyAddresses` si ce n'est pas encore fait, et y importer ce composant dans `AddressList`

```html
<script>
import AddressList from './components/AddressList';

export default {
  components: {
    // Reference to the AddressList component
    AddressList,
  },
};
</script>
```