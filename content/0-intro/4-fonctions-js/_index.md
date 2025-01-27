+++
pre = '<b>4. </b>'
title = 'Fonctions JS'
weight = '14'
draft = false
+++

Chaque fois que l'on souhaite effectuer une tâche répétitive, on utilise des fonctions. En Javascript, il existe plusieurs syntaxes pour déclarer une fonction.

### Fonctions nommées

Une fonction nommée commence par le mot-clé `function`, suivi du nom de la fonction (dans l'exemple ci-dessous : `logCompliment`). Le corps de la fonction et ses instructions (i.e. son bloc d'instruction) sont définis entre des accolades :

```js
function logCompliment() {
    console.log("Vous vous débrouillez très bien !") ;
}
```
Une fois la fonction déclarée, vous l'invoquez ou l'appelez pour la voir s'exécuter :

```js
function logCompliment() {
    console.log("Vous vous débrouillez très bien !") ;
}

logCompliment() ;
```

### Fonctions anonymes 

Une autre option serait d'utiliser la syntaxe de **fonction anonyme**, ce qui revient à déclarer la fonction comme une variable :

```js
const logCompliment = function() {
    console.log("Vous vous débrouillez très bien !") ;
};

logCompliment();
```

Le resultat est le même. La seule différence, c'est qu'il n'est pas possible d'invoquer une fonction anonyme avant de la déclarer : 

```js
// Invoquer la fonction avant de la déclarer
hey();

// Fonction nommée
function hey() {
    alert("hey!");
}
```

```js
// Invoquer la fonction avant de la déclarer
hey();

// Fonction anonyme
const hey = function() {
    alert("hey!");
    };

```
    TypeError: hey is not a function


#### Passage d'arguments

Une fonction peut prendre un ou plusieurs arguments en entrée : 

```js
const logCompliment = function(firstName) {
    console.log(`Vous vous débrouillez très bien, ${firstName}`);
};

logCompliment("Molly");
```

```js
const logCompliment = function(firstName, message) {
    console.log(`${firstName}: ${message}`);
};

logCompliment("Molly", "Tu es vraiment cool !");
```

#### Retour de fonctions

La fonction `logCompliment` affiche un compliment sur la console, mais le plus souvent, une fonction est utilisée pour **retourner** une valeur.

Pour cela, on utilise le mot-clé `return`.

```js
const createCompliment = function(firstName, message) {
    return `${firstName} : ${message}` ;
} ;

createCompliment("Molly", "You're so cool") ;
```

```js
console.log(createCompliment("You're so cool", "Molly")) ;
```

#### Arguments par défaut

Il est possible d'avoir des valeurs par défaut pour les arguments. Dans le cas ou la valeur n'est pas fournie, la valeur par défaut est utilisée : 

```js
function logActivity(name = "Shane McConkey", activity = "skier") {
    console.log(`${name} adore ${activity}`);
}
```
```js
const defaultPerson = {
    name: {
        first: "Shane",
        last: "McConkey"
    },
    favActivity: "skier"
};

function logActivity(person = defaultPerson) {
    console.log(`${person.name.first} adore ${person.favActivity}`);
}
```

### Fonctions fléchées

Une façon plus "moderne" de déclarer une fonction est d'utiliser la syntaxe des **fonctions fléchées**. Avec les fonctions fléchées, il est possible de déclarer des fonctions sans utiliser le mot-clé `function`. Souvent, il n'est pas non plus nécessaire d'utiliser le mot-clé `return`.

**Fonction anonyme :**
```js
const lordify = function(firstName) {
    return `${firstName} de Canterbury`;
};

console.log(lordify("Dale")); // Seigneur Dale de Canterbury
console.log(lordify("Gail")); // Seigneur Gail de Canterbury
```

**Fonction fléchées :**

```js
const lordify = firstName => `${firstName} de Canterbury`;
```

Si la fonction possède plus d'un argument, il doivent être entourés de parenthèses :

```js
// Fonction anonyme
const lordify = function(firstName, land) {
    return `${firstName} de ${land}`;
};

// Fonction fléchée
const lordify = (firstName, land) => `${firstName} of ${land}`;

console.log(lordify("Don", "Piscataway")); // Don de Piscataway
console.log(lordify("Todd", "Schenectady")); // Todd de Schenectady
```

Cette fonction peut tenir sur une seule ligne car il n'y a qu'une seule déclaration à renvoyer. S'il y a plusieurs lignes, il faut utiliser des accolades :

```js
const lordify = (firstName, land) => {
    if (!firstName) {
        throw new Error("Un prénom doit être fourni");
    }
    
    if (!land) {
        throw new Error("Un territoire doit être fourni");
    }
    
    return `${firstName} de ${land}`;
};

console.log(lordify("Kelly", "Sonoma")); // Kelly de Sonoma
console.log(lordify("Dave")); // ! JAVASCRIPT ERROR
```

---

### Exercices

#### Exercice 1 
Faites un programme qui génère deux nombres aléatoires entre 0 et 100, fait les 4
opérations arithmétiques dessus et affiche les résultats à la console. Votre programme doit
être composé de :

+ Une fonction nommée `add` qui prend deux paramètres et retourne leur somme;
+ Une fonction nommée `sub` qui prend deux paramètres et retourne leur
différence;
+ Une fonction nommée `mult` qui prend deux paramètres et retourne leur
produit;
+ Une fonction nommée `div` qui prend deux paramètres et retourne leur division;
+ Une fonction nommée `calc` qui prend deux paramètres et affiche à la console le
résultat des 4 opérations sur ces deux nombres;
+ Une fonction anonyme (sans paramètres) qui génère deux entiers aléatoirement et
appelle `calc()` avec ces deux nombres.
+ Toutes les fonctions doivent être dans le même fichier, *s1-ex2.js*
+ Pour générer un nombre aléatoire et le stocker dans une variable (par exemple la variable
`x`), utilisez l'instruction suivante:

```js
let x = Math.floor(Math.random() * 100)
```

#### Exercice 2

Tranformer les fonctions de l'exercice 1 en fonctions fléchées. Les fonctions `add`, `sub`, `mult`, `div` et `calc` doivent tenir sur une seule ligne.