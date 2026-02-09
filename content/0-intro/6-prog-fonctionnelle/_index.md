+++
pre = '<b>6. </b>'
title = 'Programmation fonctionnelle'
weight = '160'
draft = false
+++
-----------------

La programmation fonctionnelle est un paradigme de programmation qui insiste sur l’évaluation d’appel de fonctions plutôt que sur l’utilisation de variables et de blocs imbriqués (for, if…).

Les fonctions ont toujours été des objets de plein droit en JavaScript. Il est par exemple possible de créer des fonctions anonymes et de les affecter à des variables ou de les passer en paramètre d’autres fonctions.

### Impératif vs déclaratif

La programmation fonctionnelle fait partie d'un paradigme de programmation plus large : **la programmation déclarative**. 

La programmation déclarative est un style de programmation dans lequel les applications sont structurées de telle sorte à donner la priorité à **qu'est-ce qui doit se produire** plutôt qu'à **comment cela doit se produire**.

### Utilisation de .forEach()

Une première application de la programmation fonctionnelle consiste à repenser le parcours de boucle sous la forme d’un appel à la méthode `Array.forEach` à laquelle on passe une fonction à appeler pour chaque élément.

```js
let t = [1, 2, 3, 4];
t.forEach(e => console.log(e));
```

### Le modèle filter/map/reduce

Un modèle classique de traitement d’un tableau d’éléments dans une approche fonctionnelle consiste à envisager trois opérations fondamentales :

+ **filter :** Permet de ne retenir qu’une partie des éléments d’un tableau.
+ **map :** Permet de changer la nature des éléments lors du traitement.
+ **reduce :** permet de réduire l’ensemble des éléments à une seule valeur grâce à l’utilisation d’un accumulateur.

JavaScript fournit depuis ES5 les méthodes `Array.filter`, `Array.map` et `Array.reduce` qui attendent toutes en paramètre une fonction à appliquer pour chaque élément du tableau.

Si on désire filtrer les éléments d’un tableau pour créer un autre tableau, on peut utiliser la méthode `Array.filter`.

```js
let t = [1, 2, 3, 4];
let odds = t.filter(x => x % 2);
console.log(odds); // Affiche [1, 3]
```
Si on veut modifier les éléments d’un tableau en créant un nouveau tableau, on peut utiliser la méthode `Array.map`. Le code ci-dessous, permet de créer un tableau de nombres à partir d’un tableau de chaînes de caractères.

```js
let t = ["2", "101", "324"];
let numbers = t.map(x => parseInt(x, 10));
console.log(numbers); // Affiche [2, 101, 324]
```

Si on veut créer un résultat unique à partir d’un tableau, on peut utiliser la méthode `Array.reduce`. Cette dernière attend en paramètre une fonction qui prend deux paramètres : l’élément courant et l’élément résultat de l’appel précédent. On parle d’une fonction accumulatrice.

```js
let t = [1, 2, 3];
let result = t.reduce((a, b) => a + b);
console.log(result); // Affiche 6
```

On peut chaîner ces méthodes pour obtenir des traitements complexes.

```js
let celsius = [0, 12, -2, 6, -18, 32];

let min_farenheit = celsius.filter(x => x > 0)
                           .map(x => 1.8 * x + 32)
                           .reduce((x, y) => x < y ? x : y);

console.log(min_farenheit); // Affiche 48.8
```

Le code ci-dessous parcourt un tableau de températures en degré Celsius, élimine les températures négatives ou égales à zéro, transforme les températures en degré Fahrenheit, puis conserve la température minimale par réduction.
