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

Vous pouvez répondre à ces questions sur [ce formulaire](https://docs.google.com/forms/d/e/1FAIpQLScmeMTMrPkf8Raxu3jExpXwZkRO8EvKfMNhcjk5wVAxqMJDtQ/viewform?usp=sf_link).

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
Le code suivant permet de créer un lien vers une route Vue (utilisant #).
```html
    <router-link to="/route">nom du lien</router-link>
```

1. Déclarer des routes et ajouter des liens vers ces routes :
- *Autour de moi* pointera sur une route `/aroundme`
- *Ajouter* pointera sur une route `/myaddresses`

(Vous pouvez vous aider de la [documentation officielle](https://router.vuejs.org/fr/essentials/named-routes.html))

2. Créer les composants correspondants aux routes

3. Tester que les routes fonctionent. Versioner.

### Composant *AroundMe*
1. Créer un composant simple correspondant à la vue (B) des wireframes.

2. Pour le moment ce composant sera constitué d'un titre et d'une iframe contenant une Google map centrée sur le batîment Nautibus. (Cherchez "Intégrer la carte" depuis Google Maps)

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
<template>
  <div id="myaddresses">
    <h1>Mes adresses</h1>
    <address-list></address-list>
  </div>
</template>

<script>
import AddressList from './components/AddressList';

export default {
  name: 'MyAddresses',
  components: {
    // Reference to the AddressList component
    AddressList,
  },
};
</script>
```

Rajouter des données à `MyAddresses` :
```js
export default {
...
  data () {
    return {
      addresses: [{
        name: 'Maison',
        address: '34 rue Bolivar, 69005, Lyon',
        favorite: true
      }, {
        name: 'Travail',
        address: '43, bd du 11 novembre 1918, 69622 Villeurbanne cedex',
        favorite: true
      }, {
        name: 'Nautibus',
        address: '43, bd du 11 novembre 1918, 69622 Villeurbanne cedex',
        favorite: false
      }, {
        name: 'AML',
        address: '43, bd du 11 novembre 1918, 69622 Villeurbanne cedex',
        favorite: false
      }]
    }
};
```

On peut maintenant attacher (= `bind`) les données au composant liste.
```xml
<address-list v-bind:addresses="addresses"></address-list>
```

Pour que les addresses soient accessibles dans le composant liste, il faut déclarer la propriété qui permet d'utiliser les addresses.

```js
export default {  
    props: ['addresses'],
}
```

Cela prend la forme ci-dessous. On retrouve deux formes de templating : la boucle `for` sur les adresses, et la récupération de variables entre double accolade.

```html
<template>
  <div>
    <div class='' v-for="address in addresses">
      <div class='content'>
        <div class='header'>
          {{ address.name }}
        </div>
        <div class='meta'>
          {{ address.address }}
        </div>
      </div>
    </div>
  </div>
</template>

<script type="text/javascript" >

export default {
  props: ['addresses']
};
</script>
```

**Tester et versionner**

##### Modularisation : création d'un composant AddressItem

Pour plus de modularisation et de réutilisation, on va maintenant créer un composant `AddressItem` qui sera en charge de l'affichage d'une adresse et de son "petit" nom.

Créer un composant `AddressItem` en réutilisant le code provenant de `AddressList`

```html
<template>
  <p class='content'>
    <em class='label'>
        {{ "{{address.name "}}}} :
    </em>
    <span class='desc'>
        {{ "{{address.address "}}}}
    </span>
  </p>
</template>

<script>
export default {
  props: ['address']
}
</script>
```

Et modifier `AddressList` de manière à utiliser notre nouveau composant

```html
<div class='' v-for="address in addresses">
  <address-item v-bind:address="address"></address-item>
</div>
...
<script type = "text/javascript" >
import AddressItem from './AddressItem'

export default {
  props: ['addresses'],
  components: {
    AddressItem
  }
}
</script>
```

L'affichage de votre page `myaddresses` ne devrait pas avoir changé, mais si vous utilisez [l'extension de développement de Vue.js](https://github.com/vuejs/vue-devtools) vous pourrez remarquer que chaque adresse est désormais encapsulée dans un composant propre.


**Tester et versionner**

##### Création d'un composant AddAddress

Afin de pouvoir rajouter des adresses à notre liste, nous allons créer un composant `AddAddress` qui sera un simple formulaire à 2 champs.

```html
<template>
  <div>
    <p><input type="text" placeholder="Nom"></p>
    <p><input type="text" placeholder="Adresse"/></p>
    <button>Ajouter</button>
  </div>
</template>

<script type = "text/javascript" >

export default {
}
</script>
<style>
```

En l'état, le composant ne fait rien du tout. La première étape va être de lier les champs d'`input` à la propriété `data` de notre composant, de manière à ce que tout changement de valeur dans `data` soit automatiquement répercuté dans les `input` et inversement. Pour cela nous allons utiliser la directive [`v-model`](https://vuejs.org/v2/guide/forms.html).

```html
<p><input type="text" placeholder="Nom" v-model="name"></p>
<p><input type="text" placeholder="Adresse" v-model="address"/></p>
...
<script type = "text/javascript" >

export default {
  data : function(){
    return {
      name : '',
      address : ''
    }
  }
}
</script>
```

Vous pouvez tester que les changements dans `data` se répercutent automatiquement sur votre champ d'`input` (et inversement) en utilisant le devtool.

Maintenant que les valeurs des champs du formulaire sont captées, nous allons faire en sorte que le bouton `Ajouter` fonctionne. Pour cela nous allons capter l'évènement `click` de l'élément `button` et le lier à une méthode de notre composant.

```html
...
<button v-on:click="createAddress">Ajouter</button>
...
<script type = "text/javascript" >

export default {
  data : function(){...},
  methods: {
    createAddress: function(){
      const name = this.name
      const address = this.address
      this.$emit('add-address', {
        name: name,
        address: address,
        favorite: true
      })
    }
  }
}
</script>
```

La méthode `createAddress` appelée lors du click sur le bouton va se contenter d'émettre un évènement à son tour : `add-address` qui est accompagné par un objet contenant les proriétés de l'adresse que l'on vient de créer.

Notre composant `AddAddress` est désormais complet. Nous pouvons donc l'ajouter au composant `MyAddresses` et de capter l'évènement `add-address` qui est émis lors du click sur le bouton.

```html
<h1>Mes adresses</h1>
    <address-list v-bind:addresses="addresses"></address-list>
    <add-address v-on:add-address="addAddress"></add-address>
  </div>
</template>

<script>
...
  methods: {
    addAddress : function(newAddress){
      this.addresses.push(newAddress)
    }
  }
...
</script>
```

Désormais, lors du clic sur le bouton pour créer une adresse, une nouvelle ligne doit apparaître automatiquement dans votre liste d'adresses.

**Tester et versionner**

### Bonus
Maintenant que nous avons des composants réutilisables, pouvez-vous afficher la liste des adresses enregistrées dans le composant `HelloWorld` sous le titre "Mes adresses" ?