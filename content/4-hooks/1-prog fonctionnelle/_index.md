+++
pre = '<b>1. </b>'
title = "Programmation fonctionelle"
weight = '510'
draft = false 
+++

La **programmation fonctionnelle**, dans React, est un principe fondamental pour écrire des composants clairs, prévisibles et faciles à maintenir. Voici les trois concepts clés à retenir :

---

### Fonctions pures
Une **fonction pure** est une fonction qui, pour les mêmes **entrées**, retourne toujours les mêmes **résultats**, **sans modifier l’environnement extérieur**.

Dans React :
- Un *component* est comme une fonction pure : il prend des *props* et retourne une interface utilisateur (UI) - éléments du DOM affichés à l'ecran.
- Si le *component* est bien écrit, il produira toujours le même rendu pour les mêmes *props* et le même *state*.
- Lorsqu’un *state* change, React réexécute le *component* (*re-render*), mais si les valeurs sont identiques, le résultat reste le même.

Enfin, le développeur ayant pour tâche de traiter le code du component, et React d'executer celui-ci ; le corps de ce *component* doit rester pur et ne provoquer aucun effet secondaire.

### Immuabilité
En React, on ne **modifie jamais directement** :
- les *props* reçues (elles sont en lecture seule)
- le *state* (géré avec `useState`)

Au lieu de cela, on utilise la fonction de mise à jour (`setState`) pour créer une **nouvelle version** du *state*, en respectant le principe d’**immutabilité**. Cela garantit une gestion plus claire, plus prévisible, et facilite les optimisations internes de React.


### Éviter les *side effects*
Lorsqu’un *component* s’exécute, il ne doit **rien modifier en dehors de son propre système**.

**Exemple innadéquat** : envoyer une requête pour écrire dans une base de données **directement dans le corps du component**.  
Pourquoi ? Car React peut **réexécuter** ce *component* plusieurs fois (si le state change par exemple), ce qui pourrait déclencher une multitudes d'évènements indésirables et engendrer des problèmes majeurs.

En réalité, nous avons tout de même souvent besoin d’exécuter des opérations extérieures comme :
- faire un appel à une API ou une base de données, 
- écrire dans `localStorage`,
- ou écouter des événements du navigateur.

### La solution : séparer le **rendu** des **effets**

Il faut bien distinguer deux étapes :
1. **Récupérer les données** (fetch depuis une API, par exemple),
2. **Les utiliser dans l’interface** (les stocker dans le *state* et les afficher).

Cette séparation permet à React :
- de mieux contrôler le cycle de vie des *components*,
- d’éviter des comportements imprévisibles liés aux *side effects*,
- et de maintenir une application stable et performante.

C’est exactement le rôle du hook `useEffect`, que nous allons découvrir dans la prochaine section.
