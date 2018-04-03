## TP 5 : Présentation avancée

Nous allons continuer le développement de l’application de conseil en mobilité. Dans ce TP et le suivant nous allons travailler l’accès et le stockage des données. 


### Découverte de Navitia.io

1. Se créer un compte sur [navitia.io](https://www.navitia.io/) si ce n’est pas encore le cas.
2. Récupérer une clé (token) pour que votre application puisse requête l’API [https://www.navitia.io/profile](https://www.navitia.io/profile).
3. [Tester l’api](http://doc.navitia.io/#third-step) depuis votre navigateur. Par exemple en accédant à [la liste des lignes](https://api.navitia.io/v1/coverage/sandbox/lines) disponibles dans le bac à sable de Navitia. Ou à un trajet entre deux points à Paris : [https://api.navitia.io/v1/coverage/sandbox/journeys?from=2.3749036%3B48.8467927&to=2.2922926%3B48.8583736&](http://canaltp.github.io/navitia-playground/play.html?request=https%3A%2F%2Fapi.navitia.io%2Fv1%2Fcoverage%2Fsandbox%2Fjourneys%3Ffrom%3D2.3749036%3B48.8467927%26to%3D2.2922926%3B48.8583736&token=3b036afe-0110-4202-b9ed-99718476c2e0)

4. Navitia utilise une [Basic authentication](http://doc.navitia.io/#authentication). Il suffit d’utiliser votre token comme nom d’utilisateur.


### Requêtage depuis votre application

Nous allons implémenter deux types de requêtes : 


1. des requêtes pour obtenir les propositions de trajets souhaités.
2. des requêtes lors de changements sur le champs de formulaire pour faciliter la saisie avec de l’auto-complétion.



#### Trajets

1. Pour le lieu de départ et le lieu d’arrivée faire deux requêtes sur [https://api.navitia.io/v1/coverage/fr-se/places?q=lieu](https://api.navitia.io/v1/coverage/fr-se/places?q=lieu).
2. Afficher la liste des lieux correspondant à la requête et laisser l’utilisateur choisir celui qui lui convient (pour le départ et l’arrivé).

3. Récupérer l’identifiant correspondant aux lieux de départ et d’arrivé, et effectuer une requête pour demander les trajets. Par exemple pour un trajet de l’Opéra à la Doua à Lyon:

```
https://api.navitia.io/v1/coverage/fr-se/journeys?from=4.8363608;45.7675475&to=stop_area:DGL:SA:S10654
```
 

#### Auto-complétion

Cette partie consiste à reprendre les points 1 et 2 précédents en travaillant une vue qui affiche dynamiquement les lieux lors de changement dans les champs de formulaire.



