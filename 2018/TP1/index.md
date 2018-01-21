## TP 1 : Mise en place d'une stack JavaScript


### Outils

<!-- Les logiciels nécessaires sur ce TP sont ceux présentés dans le CM stack JS. Ils sont pré-installés sur des VMs que nous pouvons instancier à la demande. Ces machines ne sont accessibles que depuis l'intérieur de l'université.
Pour utiliser ces VMs, le plus simple est :

    d'ouvrir une console en ssh : ssh login@192.168.74.XXX
    d'éditer votre code sur votre machine locale à l'aide de votre IDE, et de le pusher sur votre repo quand vous voulez le tester
    de cloner et votre dépôt et redémarrer votre serveur sur la VM
    de tester avec le navigateur de votre machnie locale -->

### Présentation de l'application

<!-- Vous partirez de l'application située ici (sur la forge). Vous pouvez tester cette application pour voir ce qu'elle doit donner. Cette application est un gestionnaire d'annuaires de sites Web très basique, que vous développerez tout au long de ce TP.
Références

    Les documentations des outils JS que vous allez utiliser sont là :
        Cours Stack JS
        API jQuery
        Underscore.js
        Backbone.js
    Cette description des patterns MV* en JS inclut également de nombreux exemples utilisant Backbone et vous sera probablement utile.

...Plus tout ce que vous trouverez par vous-mêmes.
Prise en main des outils JS

Dans cette partie, vous allez vous approprier les outils présentés en cours. -->

### Outils de gestion de projet
<!-- 
Commencez par cloner le projet sur la forge et importez-le dans WebStorm. Lancez-le avec Grunt build. Logiquement, vous devriez être bloqués dès cette première étape. Vous allez utiliser la commande npm install avec différentes options pour résoudre ce problème. -->

### Mise en place d'un serveur Node / Express



Intallation de Grunt : La procédure est indiquée ici et l'explication là :

    Installez la ligne de commande (grunt-cli) globalement
    Installez la version de grunt souhaitée en tant que dépendances de développement dans votre projet

Installez ensuite les packages NPM manquants en les sauvegardant dans le fichier package.json.

L'étape d'après est de passer la validation JSHint. Pour cela, corrigez le code JavaScript pour qu'il soit valide et relancez Grunt. Procédez ainsi jusqu'à ce que l'application se lance.

Avant de pusher sur la forge, rappelez-vous d'ignorer dans votre repo le répertoire node_modules et les autres répertoires inutiles (.idea ?).
JavaScript côté serveur

Actuellement, votre serveur Express ne sert que des fichiers statiques et tout le métier s'exécute côté client. Vous allez créer une gestion des tags côté serveur, partagée entre les différents utilisateurs. Pour cela :

    Créez une arborescence de fichiers, avec :
        un répertoire pour les fichiers statiques (HTML, CSS, images, scripts à exécuter côté client)
        un répertoire pour les fichiers JS à exécuter côté serveur (contrôleur, modèle)
    Vous pourrez ensuite affiner cette arborescence.
    "Rangez" les différents fichiers applicatifs (la page web et les deux scripts) dans les répertoires appropriés. Testez : le comportement de l'application doit rester exactement le même que dans la version initiale (gestion des bookmarks côté client).
    Faites en sorte de réaliser également les traitements applicatifs (ajout, suppression, liste de bookmarks) côté serveur :
        Modifiez votre contrôleur (server.js) pour qu'il réponde à plusieurs types de requêtes et qu'il accepte plusieurs méthodes HTTP, ainsi que les paramètres dans ces requêtes
        Recopiez le code métier (annuaire.js) dans le contrôleur du serveur et ajoutez les fonctions JS permettant de l'appeler depuis ce contrôleur
        Rajoutez un script JS côté client capable de l'interroger en AJAX et d'afficher les résultats sur la page HTML
        Dupliquez également les éléments de l'UI et modifiez ceux à lier au serveur en conséquence.
    Attention : ne supprimez pas le fichier annuaire.js qui réalise les traitements côté client.

À la fin de cette étape, vous devez avoir une application qui gère deux types de bookmarks, côté client et côté serveur.
