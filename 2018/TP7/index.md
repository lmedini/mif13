## TP 7 : Device API


### Détection des capacités du dispositif

[Modernizr](https://modernizr.com/) est un outil qui permet de créer un script JS testant de manière efficace et fiable les capacités du dispositif sur lequel la page est chargée.

Créer une nouvelle route (nommée '''device''') pointant vers une page qui utilisera un script [Modernizr](https://modernizr.com/) pour tester les API suivantes :

- Geolocation API
- Orientation and Motion Events
- DOM Pointer Events API
- Local Storage
- Vibration API
- Canvas
- Battery API

[Le guide d'utilisation de Modernizr](https://modernizr.com/docs/#using-modernizr-with-javascript). Pour faire simple : 

1. on crée un script ad-hoc qui ne teste que les choses que l'ont souhaite. 
2. On importe le script. 
3. On teste chacune des API souhaitées avec du JS (ou du CSS) en suivant le code suivant :

```javascript
  if (Modernizr.awesomeNewFeature) {
    //supported
  } else {
    // not-supported
  }
```

Le composant affichera : oui ou non en face du nom de chaque API.

Tester sur votre ordinateur, puis sur un smartphone (voir ci-dessous).



### Set-up pour tester votre application depuis un téléphone

Plusieurs options sont possibles pour tester votre code depuis un téléphone. Les voici listées, à vous de choisir celle.

##### Créer un tunnel 
Par exemple en utilisant l'utilitaire [ngrok](https://ngrok.com/) qui fournit une URL publique vers votre machine (requiert une installation sur sa machine).

##### Déployer sur un serveur  
La technique la plus fiable. Vous pouvez déployer sur une VM de l'université, ou en une ligne de commande via des outils tels que [Now.sh de Zeit](https://zeit.co/now) ou [surge.sh](https://surge.sh/).

##### Brancher son téléphone (Android) en USB
[Voici les conseils de Google](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/local-server) pour accéder au localhost de l'ordinateur auquel est branché un téléphone portable.

##### Utiliser un émulateur

En installant les outils de développement Android, vous aurez accès à un émulateur permettant de simuler le dispositif Android de votre choix. Le processus d'installation prend des heures. Ne pas choisir cette option si vous n'avez pas déjà les outils de développement Android sur votre machine au début du TP.



### Accéder à votre position géographique

Re-prendre la page commencée et afficher les coordonnées GPS en face de "Geolocation API", au lieu d'un simple oui.



### Utiliser la position géographique pour recherche un trajet

Reprendre le composant d'autocomplétion. Rajouter un bouton qui permette d'utiliser sa position plutôt qu'une adresse.



### Utiliser l'appareil photo et l'accéléromètre pour de la pseudo Réalité Augmenté

En s'inspirant de [travaux en Réalité Augmenté](http://graphics.cs.columbia.edu/publications.newer/iswc97.pdf) remis [au gout du jour par Google dernièrement](https://arstechnica.com/gadgets/2018/05/google-maps-unveils-its-first-ever-augmented-reality-interface/), nous allons prototyper un système de guidage.

Créer une nouvelle route et un nouveau composant.

##### Afficher un flux vidéo

Le composant contiendra un element '''video''' affichant le flux vidéo de la caméra : 

```html
<video id="video" width="640" height="480" autoplay></video>
```

Suivre les explications de David Walsh pour afficher un flux vidéo : https://davidwalsh.name/browser-camera.

##### Afficher des flèches  

Rajouter un canvas par dessus la vidéo en s'inspirant de ce [jsfiddle](https://jsfiddle.net/7sk5k4gp/13/), le canvas ne peut avoir qu'une taille déterminéé, il doit donc être retaillé programatiquement.

Dessiner un triangle [en suivant le tutorial de la MDN](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Tutorial/Drawing_shapes).

##### Lier accéléromètre et flèches

En fonction de la valeur de l'accéléromètre sur l'axe Z ([`DeviceOrientationEvent.alpha`](https://developer.mozilla.org/en-US/docs/Web/API/DeviceOrientationEvent/alpha)) afficher une flèche pointant vers la droite (0 - 180) ou vers la gauche (180 - 360).