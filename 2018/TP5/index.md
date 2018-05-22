## TP 5 : Présentation avancée

Nous allons continuer le développement de l’application de conseil en mobilité. Dans ce TP et le suivant nous allons travailler l’accès et le stockage des données. 


### Découverte de Navitia.io

1. Se créer un compte sur [navitia.io](https://www.navitia.io/) si ce n’est pas encore le cas.
2. Récupérer une clé (token) pour que votre application puisse requête l’API [https://www.navitia.io/profile](https://www.navitia.io/profile).
3. [Tester l’api](http://doc.navitia.io/#third-step) depuis votre navigateur. Par exemple en accédant à [la liste des lignes](https://api.navitia.io/v1/coverage/sandbox/lines) disponibles dans le bac à sable de Navitia. Ou à un trajet entre deux points à Paris : [https://api.navitia.io/v1/coverage/sandbox/journeys?from=2.3749036%3B48.8467927&to=2.2922926%3B48.8583736&](http://canaltp.github.io/navitia-playground/play.html?request=https%3A%2F%2Fapi.navitia.io%2Fv1%2Fcoverage%2Fsandbox%2Fjourneys%3Ffrom%3D2.3749036%3B48.8467927%26to%3D2.2922926%3B48.8583736&token=3b036afe-0110-4202-b9ed-99718476c2e0)
4. Navitia utilise une [Basic authentication](http://doc.navitia.io/#authentication). Il suffit d’utiliser votre token comme nom d’utilisateur. *NB : il n'est pas possible d'utiliser votre token directement dans l'URL, les navigateurs modernes bloquent ce procédé à la sécurité douteuse. Il vous faudra ajouter votre token dans un un champ `Authorization` dans les headers de votre requête.*

5. Tester des requêtes de base depuis [Postman](https://www.getpostman.com/), le [playground de Navitia](http://canaltp.github.io/navitia-playground/play.html) ou les outils de développement de votre navigateur.

### Requêtage depuis votre application

Nous allons implémenter plusieurs requêtes vers l'API de navitia et créer des composants associés.

##### Composant de saisie de lieu (Départ/Arrivée)

Pour le lieu de départ et le lieu d’arrivée créer un nouveau composant : un `<v-select>` disponible avec la bibliothèque Vuetify. Afin de faciliter la saisie de lieu, ce composant proposera une autocomplétion tirant parti de l'API Navitia.

La création d'un `<v-select>` permettant l'auto-complétion est présentée [avec cet exemple](https://vuetifyjs.com/en/components/selects#example-autocomplete).

Votre `<v-select>` pourrait ressembler à ceci :

```xml
<v-select
 v-bind:label="label"
 autocomplete
 v-bind:loading="loading"
 v-bind:items="items"
 return-object
 v-bind:search-input.sync="search"
 v-bind:filter="noFilter"
 v-model="select"
 >
</v-select>
```

Lors de changements sur l'élement, la fonction `watch` est appelée via la propriété suivante `v-bind:search-input.sync="search"`

Dans votre script rajouter une propriété `search` dans `data`. Et implémenter une fonction `search()` qui sera déclenchée lors d'un changement dans le champ v-select.`

```js
data () {
 return {
 search: null,
}},
watch: {
   search (val) { 
    // val est la valeur du champ texte
    val   &&   this.querySelections(val)
  }
}
```
Rajouter une méthode `querySelections(val)` à votre script qui va requêter navitia.io


##### Requêtage de l'API `places`

La méthode `querySelections(val)` exécutera une requête vers l'API de Navitia à chaque changement dans le select.

La requête à exécuter devrait être sous cette forme :  [http://api.navitia.io/v1/coverage/fr-se/places?q=lieu](http://api.navitia.io/v1/coverage/fr-se/places?q=lieu)

Votre token est à inclure dans les headers de votre requête (champ `Authorization`). Pour réaliser votre requête la fonction `fetch` est supportée par les navigateurs modernes. [La documentation](https://developer.mozilla.org/fr/docs/Web/API/WindowOrWorkerGlobalScope/fetch) vous aidera correctement compléter votre header.

Dans l'idéal votre token devrait être stocké sur votre serveur et votre application Web ne le conserverait [surtout pas dans son code source](https://github.com/dxa4481/truffleHog). Pour des raisons de simplicité dans le cadre de ce TP, ces considérations de sécurité peuvent être ignorées.

Vous pouvez récupérer la liste des suggestions proposées par Navitia dans une propriété `items` de votre composant. Si le binding a été fait correctement dans votre `<v-select>` (`
 v-bind:items="items"`), le champ de saisie devrait vous proposer les résultats de la requête en autocompletion.

 ![exemple]({{"screen_autocomplete.PNG"}})

Les suggestions retournées par l'API sont sous la forme d'un tableau d'objets Javascript. Si vous essayez de les afficher tels quels dans l'autocomplete, vous ne verrez affiché que `[Object object]` à chaque ligne. Pour obtenir une affichage plus élégant tel que dans l'exemple ci-dessus, vous allez devoir utiliser des [scoped slots](https://vuetifyjs.com/en/components/selects#example-scoped-slots) pour customiser votre affichage.

Les templates suivant permettent un affichage basique :

```js
<template slot="selection" slot-scope="data">
  {{ "{{data.item.name "}}}}
</template>
<template slot="item" slot-scope="data">
  {{ "{{data.item.name "}}}}
</template>
```

##### Stockage dans le store

Enregistrer le lieu de départ et d'arrivée dans le store. La liaison entre un select et le store est expliquée dans [cette partie de la documentation de Vuex](https://vuex.vuejs.org/fr/forms.html)

Lors de la déclaration de l'élément `<v-select>` nous avons spécifié que le select utilisait en tant que v-model la propriété select. Cette propriété select est une propriété calculée ([cf documentation sus-citée](https://vuex.vuejs.org/fr/forms.html)):

```js
computed: {
 select: {
     get () {
         return this.$store.getters[this.storeProperty]
    },
     set (v) {
         this.$store.dispatch(this.storeProperty, v)
    }
  }
},
```

Pour faciliter la réutilisation du composant LocationTextField que nous venons de créer nous pouvons déclarer un props `storeProperty` qui permettra de mettre à jour le bon élément du store. *D'autres approches sont possibles*
```js
props: ['label', 'storeProperty'],
```
L'utilisation du composant peut alors se faire de la manière suivante :
```xml
<location-text-field label="Départ" storeProperty="departure"></location-text-field>
```

##### Requêtage de l'itinéraire

[Rajouter un bouton](https://vuetifyjs.com/en/components/buttons) "Rechercher" à votre formulaire (dans le composant parent) si ce n'est déjà fait. Le clic sur ce bouton provoquera une requête vers [l'API `journeys`](http://doc.navitia.io/#journeys) de Navitia :
`http://api.navitia.io/v1/coverage/fr-se/journeys?from=4.8363608;45.7675475&to=stop_area:DGL:SA:S10654`

Cette requête se fera sur le même mode que la précédente.

Les paramètres `from` et `to` correspondent à l'`id` du `place` choisi à récupérer via un getter du store.

##### Affichage des itinéraires

Créer un composant dédié à l'affichage des itinéraires. Ce composant utilisera une [v-list](https://vuetifyjs.com/en/components/lists). 

Ce composant suivra une liste `journeys` store pour modifier ses propositions :

```js
<script>
export default {
  computed: {
    journeys: function () {
      return this.$store.getters.journeys
    }
  }
}
</script>
```

Utiliser les valeurs de `journeys` pour peupler la liste via un `v-for`. S'appuyer sur les exemples de documentation de [v-list](https://vuetifyjs.com/en/components/lists). 
