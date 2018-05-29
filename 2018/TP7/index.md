## TP 7 : Device API


### Set-up pour tester votre application depuis un téléphone

Plusieurs options sont possibles pour tester votre code depuis un téléphone. Les voici listées, à vous de choisir celle.

##### Déployer sur un serveur  
La technique la plus fiable. Vous pouvez déployer sur une VM de l'université, ou en une ligne de commande via des outils tels que [Now.sh de Zeit](https://zeit.co/now) ou [surge.sh](https://surge.sh/).

##### Créer un tunnel 
Par exemple en utilisant l'utilitaire [ngrok](https://ngrok.com/) qui fournit une URL publique vers votre machine (requiert une installation sur sa machine). Cette stratégie, entrainera probablement des problèmes lors des requêtes vers l'API de navitia.


##### Brancher son téléphone (Android) en USB
[Voici les conseils de Google](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/local-server) pour accéder au localhost de l'ordinateur auquel est branché un téléphone portable.

##### Utiliser un émulateur

En installant les outils de développement Android, vous aurez accès à un émulateur permettant de simuler le dispositif Android de votre choix. Le processus d'installation prend des heures. Ne pas choisir cette option si vous n'avez pas déjà les outils de développement Android sur votre machine au début du TP.



### Utiliser la position géographique pour recherche un trajet

Reprendre le composant d'autocomplétion. Rajouter un bouton qui permette d'utiliser sa position plutôt qu'une adresse. On utilisera pour cela l'[API de géolocalisation](https://developer.mozilla.org/en-US/docs/Web/API/Geolocation/Using_geolocation). 

L'API de [navitia de Journey Planning](http://doc.navitia.io/#journey-planning) prend aussi des coordonées géographique en paramètre.

### Utiliser l'appareil photo et l'accéléromètre pour de la pseudo Réalité Augmenté

En s'inspirant de [travaux en Réalité Augmenté](http://graphics.cs.columbia.edu/publications.newer/iswc97.pdf) remis [au gout du jour par Google dernièrement](https://arstechnica.com/gadgets/2018/05/google-maps-unveils-its-first-ever-augmented-reality-interface/), nous allons prototyper un système de guidage.

Créer une nouvelle route et un nouveau composant.

##### Afficher un flux vidéo

Le composant contiendra un element '''video''' affichant le flux vidéo de la caméra : 

```html
<video id="video" width="640" height="480" autoplay></video>
```

Suivre les explications de David Walsh pour afficher un flux vidéo : https://davidwalsh.name/browser-camera.

Attention, en fonction des navigateurs, il vous sera sans doute nécessaire d'exécuter le code nécessaire à l'utilisation de la caméra dans une fonction appelée à la suite d'un action utilisateur (onclick, ...).

##### Afficher une flèche montrant la direction à prendre

Pour afficher la direction fictive à prendre, vous pouvez simplement afficher une balise `img` par dessus l'élément `video`.

En fonction de la valeur de l'accéléromètre sur l'axe Z ([`DeviceOrientationEvent.alpha`](https://developer.mozilla.org/en-US/docs/Web/API/DeviceOrientationEvent/alpha)) vers une direction fixe.

Pour lire les valeurs de l'accéléromètre, vous pouvez vous référer à la [documentation MDN](https://developer.mozilla.org/fr/docs/WebAPI/Detecting_device_orientation).

Pour transformer l'image de flèche en fonction des valeurs que vous obtenez, vous pouvez utiliser une propriété CSS `transform` :

```js
document.getElementById('fleche').style.transform =
                      'rotateX(' + event.beta + 'deg) ' +
                      'rotateZ(' + event.alpha + 'deg)'
```
