+++
pre = '<b>1. </b>'
title = "Concepts fondamentaux"
weight = '510'
draft = false 
+++

---
<!-- 
## Programmation fonctionnelle
La **programmation fonctionnelle**, dans React, est un principe fondamental pour écrire des composants clairs, prévisibles et faciles à maintenir. Voici les trois concepts clés à retenir :

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

**Exemple inadéquat** : envoyer une requête pour écrire dans une base de données **directement dans le corps du component**.  
Pourquoi ? Car React peut **réexécuter** ce *component* plusieurs fois (si le state change par exemple), ce qui pourrait déclencher une multitudes d'évènements indésirables et engendrer des problèmes majeurs.

En réalité, nous avons tout de même souvent besoin d’exécuter des opérations extérieures comme :
- faire un appel à un serveur externe (API) ou une base de données, 
- ou écouter des événements du navigateur.

### Solution : séparer le **rendu** des **effets**

Il faut bien distinguer deux étapes :
1. **Récupérer les données** (fetch depuis une API, par exemple),
2. **Les utiliser dans l’interface** (les stocker dans le *state* et les afficher).

Cette séparation permet à React :
- de mieux contrôler le cycle de vie des *components*,
- d’éviter des comportements imprévisibles liés aux *side effects*,
- et de maintenir une application stable et performante.

C’est exactement le rôle du hook `useEffect`, que nous allons découvrir dans la prochaine section. -->


## Communication et récupération de données
Dans les sections précédentes, nous avons utilisé des données "en dur" (*mock data*) ou locales (généralement un fichier `data.js` dans le répertoire **/assets/** de nos projets). Dans une application réelle, les données vivent sur un **serveur distant**.

### Cycle de vie d'une donnée
Imaginez le flux suivant :
1. **Le Frontend (React)** envoie une requête (ex: "Donne-moi le profil de l'utilisateur 42").
2. **L'API (Backend)** reçoit la requête, vérifie les permissions, et communique avec la Base de données.
3. **La Base de données** exécute une opération (ex: `SELECT * FROM users...`).
4. **Le Serveur** formate le résultat (souvent en JSON) et le renvoie au Frontend.
5. **React** reçoit la donnée, met à jour son `state`, et déclenche un nouveau rendu.

### Les bases du protocole HTTP
Pour communiquer, le client et le serveur utilisent le **protocole HTTP**. Chaque requête utilise une "méthode" qui indique l'intention de l'action :

|Méthode|	Action SQL équivalente|	Description|
|-------|-----------------------|------------|
|`GET`|	`SELECT`|	Récupérer une ressource (ex: lire un article).|
|`POST`|	`INSERT`|	Créer une nouvelle ressource (ex: envoyer un formulaire).|
|`PUT` / `PATCH`|	`UPDATE`|	Modifier une ressource existante.|
|`DELETE`|	`DELETE`|	Supprimer une ressource.|

## Programmation asynchrone
Jusqu’à présent, nous avons écrit du code synchrone, c’est-à-dire que les instructions s’exécutent une par une, dans l’ordre.

Cependant, lorsqu’une application doit interagir avec une ressource externe (comme une API), certaines opérations peuvent prendre du temps (réseau, serveur, etc.). On ne veut pas bloquer l’application pendant ce temps.

C’est là qu’intervient la **programmation asynchrone**.

Prenons un exemple simple :
```js
console.log("Début");

fetch("https://api.exemple.com/data");

console.log("Fin");
```
Même si la requête prend du temps, "Fin" s’affiche immédiatement.
{{%notice style="tip" title="Comportement de JavaScript" %}}
JavaScript ne bloque pas l’exécution : il continue pendant que la requête est en cours.
{{%/notice%}}

### Les Promises
Les appels asynchrones en JavaScript reposent souvent sur des **Promises**. Une **Promise** représente une valeur qui sera disponible maintenant (résolue), plus tard (en attente), ou jamais (rejetée).

### Syntaxes des requêtes

#### Utilisation de .then()
La première façon de gérer une **Promise** est avec la syntaxe `.then()`.

**Exemple :**
```js
fetch("https://api.exemple.com/data")
  .then(response => response.json())
  .then((data) => console.log(data))
  .catch((error) => console.error(error))
```

1. `fetch()` retourne une **Promise**
2. `.then()` permet de traiter le résultat
3. `.catch()` permet de gérer les erreurs

**Inconvénients :**
+ Peut devenir difficile à lire (enchaînement de `.then()`)
+ Moins intuitif

#### Utilisation de async / await
`async/await` est une syntaxe moderne qui simplifie la lecture du code asynchrone. Elle permet d’écrire du code asynchrone **comme s’il était synchrone**

Exemple équivalent :
```js
async function getData() {
  try {
    const response = await fetch("https://api.exemple.com/data");
    const data = await response.json();
    console.log(data);
  } catch (error) {
    console.error(error);
  }
}
```
**Explication :**
+ `async` indique que la fonction est asynchrone
+ `await` suspend l’exécution jusqu’à ce que la **Promise** soit résolue
+ `try`/`catch` remplace `.catch()`
