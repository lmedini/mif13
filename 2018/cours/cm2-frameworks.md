<!-- $theme: gaia -->
<!-- page_number: true -->



# Programmation Web Avancée et Mobile

### CM 2 : Bibliothèques et frameworks côté client

Aurélien Tabard - Lionel Médini


--- 

### Plan du cours

- Rappels JavaScript
- Introduction aux principes partagés par les frameworks JavaScripts modernes
- Introduction à Vue

---

### Ressources

Page à compléter :
- (Hacks et liens utiles)[https://aurelient.github.io/mif13/2018/hack]Hack

Livres
- [Eloquent Javascript (3rd edition EN)](http://eloquentjavascript.net/3rd_edition/)
- [Eloquent Javascript (1e edition FR)](https://fr.eloquentjavascript.net/)

---

### Rappels JavaScript

- Faiblement typé
  <small>Conversions de types implicites, opérateur ===  </small>
- Fonctionnel
  <small>Basé sur le scope des variables</small>
- Orienté évènement
  <small>Trick : une callback peut être une alternative aux threads</small>
- Orienté prototype
  <small>Les objets peuvent partager un prototype, mais pas d'héritage entre classes</small>

→ Langage très permissif ("assembleur du Web")

---
### Rappels JavaScript

À quoi sert la notation suivante ?

```
(function() {
	var toto = 12;
	console.log(toto);
})();
```

---

## Rappels JavaScript

À quoi sert la notation suivante ?

```js
(function() {
	var toto = 12;
	console.log(toto);
})();
```

[Comprendre la portée](https://scotch.io/tutorials/understanding-scope-in-javascript)


---

## Closures (fermetures)

- Permet de capturer l'environnement d'une fonction.
  C'est-à-dire les variables des scopes externes à celui de la fonction.

```js
  function makeFunc() {
    var name = "Mozilla";
    function displayName() {
      alert(name);
    }
    return displayName;
  }

  var myFunc = makeFunc();
  myFunc();
```

---

## Function factory

- Permet de passer des paramètres au moment de la création d'une fonction

```js
function creerAdditionneur(a) {
  return function(b) {
    return a + b;
  }
}
var add5 = creerAdditionneur(5);
var add20 = creerAdditionneur(20);
```

---

### À quoi servent les Closures ?

- Gérer la nature asynchrone de JavaScript
  - Ajouter des données locales à un callback
- Gérer des "objets"
- Émuler des méthodes privées



En savoir plus : [Closures (MDN)](https://developer.mozilla.org/fr/docs/Web/JavaScript/Closures)


--- 
## Web apps




--- 
### Années 2005-2010 : bibliothèques JS

Milieu des années 2000 : bascule d'un Web centré documents et formulaires vers un Web centré application

  - Essor des applications Web riches (RIA)
  - Toujours beaucoup de logique côté serveur
  - Développement d'AJAX et de REST
  - Bibliothèques très permissives



--- 
### Années 2005-2010 : bibliothèques JS

  La plus emblématique : **JQuery**

  - Implémentations incomplètes des standards existants
  - Standards eux-mêmes incomplets

→ Besoin de "workarounds" pour homogénéiser les comportements des navigateurs



--- 
### Années 2010 : frameworks JS

- Émergeance des Single Page Applications
- Déplacement de la logique sur le client
- Structuration du code
- Développement du "tooling" : Paquets, CSS, Javascript.

--- 
### Les frameworks JS aujourd'hui

- Angular
- React
- **Vue**
- Emberjs
- Meteor
- Backbone
- ...

[Liste sur wikipedia](https://en.wikipedia.org/wiki/Comparison_of_JavaScript_frameworks)

--- 
###



--- 
### 


--- 
### 



--- 
### 



--- 
### 



--- 
###



--- 
### 
--- 
### 



--- 
### 



--- 
### 



--- 
###



--- 
### 


--- 
### 



--- 
### 



--- 
### 



--- 
###



--- 
### 
