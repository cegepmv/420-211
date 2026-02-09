+++
title = 'Exercices'
weight = '151'
draft = false
+++
-------------
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
const user = { name: "John", years: 30, isAdmin: false };

// Votre code ici

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

console.log(student1, student2, student3, student4, student5);
```

#### Exercice 5
Écrivez une fonction `combineTwoArrays` qui prend deux tableaux en argument et retourne un seul tableau qui fusionne les deux (en utilisant l'opérateur *spread*).

#### Exercice 6
Écrivez une fonction `combineAllArrays` qui peut prendre un nombre quelconque de tableaux en argument et retourne un seul tableau qui les fusionne tous.