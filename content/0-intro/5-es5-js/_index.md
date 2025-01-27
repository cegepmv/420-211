+++
pre = '<b>5. </b>'
title = 'JS depuis ES5'
weight = '15'
draft = false
+++

Depuis la version 5 de ECMAScript (et surtout avec la version 6), la syntaxe de JavaScript a beaucoup évolué pour aller vers une meilleure cohérence et une meilleure robustesse dans le code produit. Ce chapitre résume les évolutions les plus importantes.


### Déclaration de variable avec let et const
Le mot-clé `var` est utilisé en JavaScript pour déclarer des variables.

```js
var i = 0;
```
Cependant la notion de déclaration de variable est particulière en JavaScript par rapport à la plupart des autres langages de programmation proches. `var` n’empêche pas de déclarer à nouveau une variable avec le même nom et la portée des variables est particulière à JavaScript. Si la variable est déclarée au plus haut niveau, il s’agit d’une variable globale mais si elle déclarée ailleurs, sa portée correspond à la fonction dans laquelle elle est déclarée. Cela peut entraîner des effets de bord difficiles à comprendre :

```js
var globalVar = "globale";

function myFunction() {

    var localVar = "locale";
    if (true) {
        var localVar2 = "locale 2";
    }
    console.log(globalVar);
    console.log(localVar);
    console.log(localVar2);
}

myFunction();
// Affiche
// globale
// locale
// locale 2
```

À la ligne 7, la variable `localVar2` est déclarée dans le bloc `if` mais, contrairement à d’autres langages de programmation, la portée de cette variable est la fonction. Donc il est possible d’accéder à sa valeur à la ligne 11 après le bloc `if`.

Pour corriger ce comportement tout en maintenant la rétro-compatibilité pour le code existant, ES6 introduit le mot-clé `let`.

```js
let j = 0;
```

Une variable déclarée avec `let` ne peut pas être déclarée à nouveau et sa portée est limitée au bloc dans lequel elle est déclarée.

{{% notice style="warning" title="Attention"%}}
Pour tout nouveau code, il est recommandé d’utiliser `let` pour déclarer toutes les variables.
{{% /notice %}}


Avec ES6, on dispose également du mot-clé `const` pour garantir que la déclaration est constante (une fois déclarée, sa valeur ne peut pas être modifiée) :

```js
const pi = 3.1416;
```

### Structure for … of
Une nouvelle structure de contrôle `for` a été ajoutée avec ES6 pour permettre de parcourir les objets itérables. Il s’agit de la structure `for ... of`

```js
for (let v of vowels) {
    console.log(v);
}

// Affiche
// a
// e
// i
// o
// u
// y
```

Les tableaux et les chaînes de caractères sont des objets itérables. Il est donc très facile de les parcourir avec cette nouvelle structure de contrôle.

```js
for (let i of [1, 2, 3, 4]) {
    console.log(i);
}

for (let l of "Bonjour") {
    console.log(l);
}
```

### Gabarit de chaîne de caractères
ES6 introduit les gabarits de chaîne de caractères (*template string*) pour formater plus facilement des données dans des chaînes de caractères. Plutôt que d’utiliser l’opérateur `+` de concaténation :

```js
let a = 1;
let b = 2;
let message = "La somme de " + a + " et de " + b + " est " + (a + b) + ".";
```
On peut utiliser le caractère ` pour délimiter la chaîne de caractères et préciser les noms des variables avec ${} :

```js
let a = 1;
let b = 2;
let message = `La somme de ${a} et de ${b} est ${a + b}`;
```

La syntaxe est plus concise et bien plus lisible. La valeur donnée avec `${}` peut être une expression complète : un appel de fonction, l’attribut d’un objet…

```js
let message = `La circonférence d'un cercle de rayon 3 est ${(2 * Math.PI * 3).toFixed(3)}`;

console.log(message); // Affiche La circonférence d'un cercle de rayon 3 est 18.850
```
L’utilisation du caractère *`* pour délimiter une chaîne de caractères permet également d’écrire cette chaîne sur plusieurs lignes :

```js
let message = `Ceci est un message.
Ce message est sur plusieurs lignes.
Il sera affiché également sur plusieurs lignes.`;

console.log(message);

// Affiche :
// Ceci est un message.
// Ce message est sur plusieurs lignes.
// Il sera affiché également sur plusieurs lignes.
```

### Paramètre de reste (*Spread Operator*)
Avec l’opérateur `...`, il est possible de déclarer une liste quelconque de paramètres correspondant au reste des paramètres. Cette liste sera vue comme un tableau à l’intérieur de la fonction

```js
function add(x1, x2, ...others) {
    let result = x1 + x2;
    for (let n of others) {
        result += n;
    }
    return result;
}

console.log(add(1, 2)); // Affiche 3
console.log(add(1, 2, 4)); // Affiche 7
console.log(add(1, 2, 4, 8)); // Affiche 15
```

### Décomposition de tableaux
L’opérateur `...` sert également à la décomposition de tableau qui permet de passer les paramètres à l’appel d’une fonction sous la forme d’un tableau.

```js
let args = [2, 3];

function add(x, y) {
    console.log(x + y);
}

add(...args); // Affiche 5
```


### Affectation de tableau par décomposition
L’affectation par décomposition (*destructuring assignment*) permet de réaliser des affectations multiples à partir d’un tableau.

On peut déclarer un tableau de variables à gauche de l’affectation.

```js
const arr = [1, 2, 3];
let [a, b, c] = arr;
console.log(a); // Affiche 1
console.log(b); // Affiche 2
console.log(c); // Affiche 3
```

Nous pouvons utiliser cette syntaxe pour intervertir la valeur de deux variables.

```js
let a = 1:
let b = 2:
[a, b] = [b, a]; // a vaut 2 et b vaut 1
```
Le tableau à gauche de l’affectation peut avoir une taille différent du tableau à droite de l’affectation. Si le tableau à gauche est plus petit, les éléments en plus à droite ne sont pas pris en compte.

```js
let [a, b] = [1, 2, 3, 4]; // a vaut 1 et b vaut 2
```
Si le tableau à gauche de l’affectation est plus grand, les éléments en plus reçoivent la valeur `undefined`.

```js
let [a, b, c, d] = [1, 2]; // a vaut 1, b vaut 2, c et d valent undefined
```

On peut utiliser l’opérateur de reste `...` pour affecter à une variable tous les éléments restant :

```js
let [a, ...b] = [1, 2, 3, 4]; // a vaut 1 et b vaut [2, 3, 4]
```

### Affectation d’objet par décomposition
L’affectation par décomposition (destructuring assignment) permet également de réaliser des affectations multiples à partir d’un objet. Dans ce cas, le nom des variables à gauche de l’affectation correspondent au nom des propriétés de l’objet.

```js
const person = {
    firstName: "David",
    lastName: "Gayerie"
};

let {firstName, lastName} = person;
console.log(firstName); // Affiche David
console.log(lastName); // Affiche Gayerie
```

Comme pour l’affectation de tableau par décomposition, on peut spécifier moins de variables à gauche ou plus de variables ou utiliser l’opérateur de reste ... pour affecter les propriétés restantes sous la forme d’un nouvel objet.

```js
const person = {
    firstName: "David",
    lastName: "Gayerie",
    height: 174
};

let {firstName, lastName} = person; // firstName vaut "David" et lastName vaut "Gayerie"
```

```js
const person = {
    lastName: "Gayerie",
};

let {firstName, lastName} = person; // nom vaut "David" et prenom vaut undefined
```

```js
const person = {
    firstName: "David",
    lastName: "Gayerie",
    height: 174
};
let {height, ...fullName} = personne; // height vaut 174
                                      // fullName vaut {firstName: "David", lastName: "Gayerie"}
```

---

### Exercices

#### Exercice 1

Réécrivez le code ci-dessous pour utiliser la décomposition pour assigner chaque valeur du tableau `items` :

```js
let items = ["Egg", 0.25, 12];

let name = items[0];
let price = items[1];
let quantity = items[2];

console.log(`Item: ${name}, Quantité: ${quantity}, Prix: ${price}`);
```

#### Exercice 2

Nous avons un objet `user`. Affectez par décomposition :
- la propriété `name` dans une variable `name`.
- la propriété `years` dans une variable `age`.
- la propriété `isAdmin` dans une variable `isAdmin` (`false`, si cette propriété n'existe pas).

```js
const user = { name: "John", years: 30 };

// Votre code ici :
const {} = user;

console.log(name); // John
console.log(age); // 30
console.log(isAdmin); // false
```

#### Exercice 3
Réécrivez le code ci-dessous pour utiliser la décomposition au lieu d'assigner chaque valeur à une variable : 

```js
const person = [12, "Chris", "Owen"];

const firstName = person[1];
const lastName = person[2];
const age = person[0];

console.log(`Personne : - Age: ${age}, Nom: ${firstName} ${lastName}`);
```

#### Exercice 4
Utilisez l'affectation par décomposition pour récupérer tous les noms des tableaux imbriqués dans `moreStudents` : 

```js
const moreStudents = [
    'Chris', 
    ['Ahmad', 'Antigoni'], 
    ['Toby', 'Sam']
];

// Votre code ici : 
const [] = moreStudents;

console.log(student1, student2, student3, student4, student5);
```

#### Exercice 5
Écrivez une fonction `combineTwoArrays` qui prend deux tableaux en argument et retourne un seul tableau qui fusionne les deux (en utilisant l'opérateur *spread*).

#### Exercice 6
Écrivez une fonction `combineAllArrays` qui peut prendre un nombre quelconque de tableaux en argument et retourne un seul tableau qui les fusionne tous.