+++
pre = '<b>7. </b>'
title = 'Git/GitHub'
weight = '170'
draft = false
+++

### Introduction
Git est un système de gestion de versions distribué, conçu pour suivre et gérer les modifications apportées aux fichiers au fil du temps. Il est largement utilisé dans le développement logiciel, permettant une collaboration efficace entre les développeurs tout en conservant un historique complet des changements.

Les principales fonctionnalités de Git incluent :

-  La gestion simultanée de plusieurs versions d’un projet.
- La possibilité de revenir à des états antérieurs en cas de besoin.
- La facilitation du travail en équipe sur un même projet, tout en minimisant les conflits liés aux modifications.


##### Comprendre le Flux de Travail de Git

![Git Workflow](/420-211/images/0-intro/014-gitworkflow.png)

Cette image illustre le flux de travail fondamental de Git, qui repose sur trois zones clés :

**Working Directory (Répertoire de travail)** :
C’est là où tu modifies tes fichiers localement. Chaque changement est visible ici avant d’être suivi par Git.

**Staging Area (Zone de préparation)** :
Lorsque tu exécutes git add, tes fichiers sont placés dans cette zone temporaire. Cela te permet de sélectionner les modifications que tu souhaites inclure dans ton prochain commit.

**Git Repository (Dépôt Git)** :
Après avoir validé tes changements avec git commit, ils sont enregistrés de façon permanente dans l’historique du projet.

 
##### Comprendre les Branches dans Git
Les branches dans Git permettent de travailler sur différentes fonctionnalités ou corrections sans modifier le code principal (généralement appelé main ou master). Elles offrent un espace où tu peux expérimenter, développer et tester de nouvelles idées en toute sécurité.

![Git Branches](/420-211/images/0-intro/015-gitbranches.png)

**Créer une branche** : Tu peux démarrer une nouvelle fonctionnalité sans affecter le reste du projet.
**Fusionner une branche** : Une fois le travail terminé et testé, tu peux fusionner la branche avec le code principal.
**Travailler en parallèle** : Les branches facilitent le travail en équipe, chacun pouvant travailler sur sa propre branche sans conflits immédiats.

--- 

Nous allons, à travers ce guide, explorer deux méthodes d'utilisation de Git :

1. **Git Bash**, un outil en ligne de commande.
2. **Git intégré à Visual Studio Code**, une interface graphique directement dans l'éditeur de code.

---
