# Projet Transversal 4IRC

Membres : 
* Antoine Gamain (https://github.com/Fyndir)
* Tom Blanchet (https://github.com/frontBOI)
* léo Meynet (https://github.com/Neexos)
* Lucas Philippe (https://github.com/Tenebry)

## Contexte

Ce projet consiste à simuler des incendies sur une ville, et leur prise en charge par les flottes d’urgence qui vont intervenir.

le projet se découpe en plusieurs briques : 

* Le centre de simulation (https://github.com/Fyndir/ClientJavaSimulation) : 

Son rôle est de générer des feux dont les coordonnées, l’intensité et la fréquence sont à définir dans le programme. Ces données sont par la site transmit au serveur Flash de simulation à l'aide d'une API mise à disposition par le dit serveur.
Par la site la gestion des déplacements des camions sera également gérer par ce programme et sera envoyée sur le serveur de l'emergencyManager à l'aide d'une API mis à disposition par celui-ci.

* Le serveur de simulation (https://github.com/Fyndir/FireSimulation) :

Son role est d'afficher la simulation en temps réel pour voir l'état des feu sur une map. Il permet également de récuper les données à un instant T grace a une URL qui renvoi les données sous un format prédéfinies.

* La brique IOT :

Son role est de transmettre les information du serveur de simulation au serveur d'emergency manager à l'aide de deux microcontrolleur , 2 rasberry et d'APIs devellopées sur les deux serveurs.

* Le serveur Emergency Manager (https://github.com/Fyndir/EmergencyManager):

Son role est d'inserer les données qu'il recoit dans la base de données à l'aide d'API. Il permet également d'afficher en temps réel le contenu de la base (feu / déplacement des camions)

* La base de données de l'emergency Manager : 

Son role est de stocker les données des feux et d'affecté les camions au dit feux à l'aide d'un ensemble de trigger SQL

* Le réseau Virtuel :

Le but de cette brique est de recreer l'environnement informatique des casernes avec des LAN virtuel interconnecté via une backbone. C'est depuis des VM branchées sur ce réseau que l'on peux accèder à l'ensemble des services.

## Le  réseau Virtuel

### Fonctionnement

Les technologies réseau mis en oeuvre sur les routeurs :
  - **configuration IP** : 
  - **OSPF** : Open Shortest Path First, un protocol de routage mis en place dans la backbone et ne servant qu'a annoncer les différents sous-réseau de l'Autonomous System BGP. Les interfaces étant connectés à un autre AS sont passé en passive et ne participerons pas à l'OSPF.
  - **BGP** :
    - **IBGP**:
    - **EBGP**:
    - **peer-group**:
    - **route reflector**:
  - **ACL**:
  - **routage**: 
  - **VRRP**: Virtual Rouder Redondancy Protocol, mis en place sur le LAN 2, il permet d'assurer une redondance des routeurs via une adresse IP virtuel unique connus des hôtes.
 
 Les technologies mis en oeuvre sur l'infrastructure virtuel : 
  - **Serveurs** : L'intégralité des serveurs de production sont externalisés dans le cloud Azure : simulation & emergency_manager
  - **DHCP** : Seul serveur local, présent dans la caserne "data-center", et servant à octroyer des IP dynamiquement aux hôtes dans tout les LAN des casernes.
  - **Client** : VM MXLinux sous VirtualBox, elle peux joindre les autres casernes et sortir sur internet pour accèder a l'emergency manager.

 Les technologies de templating des LAN de casernes :
  - **Template JINJA**: Fichier de template faisant appel aux variables définis dans le fichier data.yaml. 
  - **Fichier Python**: Fichier de compilation et de "rendu" du template.
  - **Fichier DATA YAML**: Fichier dictionnaire de données à remplir par l'administrateur réseau avec les informations nécessaire au déploiement.
