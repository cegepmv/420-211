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

### Mise en contexte
Avant que Git voit le jour, les équipes travaillaient principalement de deux façons: les commentaires de journal et des logiciels de versionnage centralisés.

Les commentaires de journal peuvent ressembler à ceci: 

```
// Philip Higgins 2026-01-26 Work Order 26: Refactor time-sensitive SQL queries
```

Certaines compagnies fonctionnent encore de cette manière, mais le code devient pollué: si 20 devs changent la même ligne de code, on a plus de commentaires que de lignes de code! Aussi, il devient difficile de voir la progression de cette ligne de code.

Avant, on utilisait le gestionnaire de versions centralisé SVN (Apache Subversion), mais il avait plusieurs hics: 

- Si deux personnes veulent modifier le même fichier en même temps, le premier à travailler dessus "verrouille" souvent le fichier, bloquant les autres développeurs.

- Si le serveur tombe en panne ou sans réseau, on ne peut pas faire de changements, ni voir l'historique, parce que c'est sur un serveur local.

- Chaque version (branche) du projet nécessite les fichiers complets de code, rendant les fusions de code pénibles et les branches lourdes (jusqu'à 1 Gig par branche).

![Linus](/420-211/images/0-intro/016-linus.jpg)


En 2005, en travaillant sur le noyau Linux, Linus Thorvalds, roi de l'*open source*, crée Git en quelques semaines et règle tous ces problèmes.

Maintenant, tout est décentralisé, il est possible de travailler à partir de partout: chaque ordinateur agit comme un serveur. Des équipes complètes peuvent travailler sur les mêmes fichiers en même temps. Aussi, une branche ne pèse plus que 40 octets.


##### Comprendre le Flux de Travail de Git

![Git Workflow](/420-211/images/0-intro/014-gitworkflow.png)

Cette image illustre le flux de travail fondamental de Git, qui repose sur trois zones clés :

**Working Directory (Répertoire de travail)** :
C’est là où tu modifies tes fichiers localement, dans tes dossiers locaux. Chaque changement est visible ici avant d’être suivi par Git.

**Staging Area (Zone de préparation)** :
Lorsque tu exécutes git add, tes fichiers sont placés dans cette zone temporaire et sont dits suivis (*tracked*). Cela te permet de sélectionner les modifications que tu souhaites inclure dans ton prochain commit.

**Git Repository (Dépôt Git)** :
Après avoir validé tes changements avec git commit, ils sont enregistrés de façon permanente dans l’historique du projet et accessibles sur le web pour tous les collaborateurs.

 
##### Comprendre les Branches dans Git
Les branches dans Git permettent de travailler sur différentes fonctionnalités ou corrections sans modifier la version du code officielle et déployée (généralement appelé main, anciennement master). Elles offrent un espace où tu peux expérimenter, développer et tester de nouvelles idées en toute sécurité.

![Git Branches](/420-211/images/0-intro/015-gitbranches.png)

**Créer une branche** : Tu peux démarrer une nouvelle fonctionnalité sans affecter le reste du projet.
**Fusionner une branche** : Une fois le travail terminé et testé, tu peux fusionner la branche avec le code principal.
**Travailler en parallèle** : Les branches facilitent le travail en équipe, chacun pouvant travailler sur sa propre branche sans conflits immédiats.

--- 

Nous allons, à travers ce guide, explorer deux méthodes d'utilisation de Git :

1. **Git Bash**, un outil en ligne de commande.
2. **Git intégré à Visual Studio Code**, une interface graphique directement dans l'éditeur de code.

---
