+++
pre = '<b>6. </b>'
title = 'Programmation fonctionnelle'
weight = '160'
draft = false
+++


### Définition

La programmation fonctionnelle est un paradigme de programmation qui insiste sur l’évaluation d’appel de fonctions plutôt que sur l’utilisation de variables et de blocs imbriqués (for, if…).

Les fonctions ont toujours été des objets de plein droit en JavaScript. Il est par exemple possible de créer des fonctions anonymes et de les affecter à des variables ou de les passer en paramètre d’autres fonctions.

#### Impératif vs déclaratif

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

---

### Exercices

#### Exercice 1

Utilisez `filter()` pour créer une nouvelle liste (liste2) qui ne contient que les nombres positifs de liste1

```js
const liste1 = [-23,230,334,-90,-76,132,-77,305]
```

#### Exercice 2

Utilisez `filter()` pour créer une nouvelle liste (`liste2`) qui ne contient que les nombres pairs positifs de `liste1`

```js
const liste1 = [-23,230,334,-90,-76,132,-77,305]
```

#### Exercice 3
Utilisez `filter()` pour éliminer les multiples de 10 dans liste1

```js
const liste1 = [-23,230,334,-90,-76,132,-77,305]
```

#### Exercice 4
Utilisez `filter()` pour éliminer les mots de plus de 5 caractères dans `liste1`

```js
const liste1 = ['ami','carotte','midi','toujours','hier','demain']
```

#### Exercice 5
Utilisez `filter()` pour conserver les personnes dont le email ne se termine pas par `.com` dans `liste1`

```js
const liste1 = [
    {"nom":"Charity","prenom":"Selar","email":"cselar0@cloudflare.com"},
    {"nom":"Noel","prenom":"Jermy","email":"njermy1@bbb.org"},
    {"nom":"Killian","prenom":"Keri","email":"kkeri2@sphinn.com"},
    {"nom":"Aleta","prenom":"Thurl","email":"athurl3@bandcamp.com"},
    {"nom":"Edna","prenom":"Ingyon","email":"eingyon4@telus.ca"}
]
```

#### Exercice 6
Utilisez `map()` pour créer une liste qui ne contient que la taille des mots de `liste1`

```js
const liste1 = ['ami','carotte','midi','toujours','hier','demain']
```

#### Exercice 7
Utilisez `map()` pour créer une liste qui ne contient que le carré des nombres de `liste1`

```js
const liste1 = [-23,230,334,-90,-76,132,-77,305]
```

#### Exercice 7
Utilisez `map()` pour créer une liste qui ne contient que les prénoms des personnes dans liste1

```js
const liste1 = [
    {"nom":"Charity","prenom":"Selar","email":"cselar0@cloudflare.com"},
    {"nom":"Noel","prenom":"Jermy","email":"njermy1@bbb.org"},
    {"nom":"Killian","prenom":"Keri","email":"kkeri2@sphinn.com"},
    {"nom":"Aleta","prenom":"Thurl","email":"athurl3@bandcamp.com"},
    {"nom":"Edna","prenom":"Ingyon","email":"eingyon4@telus.ca"}
]
```

#### Exercice 8
Utiliser `filter()`, `map()` et `reduce()` pour calculer la somme des carrés des nombres positifs de `liste1`

```js
const liste1 = [-23,230,334,-90,-76,132,-77,305]
```

#### Exercice 9

Ecrivez une fonction qui utilise `forEach()` pour afficher chaque élément d'un tableau dans la console. La fonction ne doit prendre qu'un seul argument, le tableau. La fonction ne doit PAS utiliser une boucle `for` traditionnelle.

#### Exercice 10
Ecrivez une fonction appelée `sum` qui utilise la méthode `reduce` pour additionner un tableau de nombres.

Exemples :

```js
sum([1,2,3,4,5]) ; //rend 15
sum([6,7,7]) ; //rend 20
```

#### Exercice 11
Ecrivez une fonction appelée `reduceMin` qui utilise `reduce` pour retourner le minimum d'un tableau de nombres donné en argument.

Exemples :

```js
reduceMin([2, 3, 4, 5, 1]) ; //retourne 1
reduceMin([6, 7, 7, 4]) ; // retourne 4
reduceMin([10, 0, 100, 1, -100, 20, 33]) ; //retourne -100
```

#### Exercice 12
Ecrivez une fonction nommée `countOddsAndEvens` qui prend un tableau de nombres. Cette fonction doit renvoyer un objet ayant deux propriétés : `odds` et `evens`, qui contiennent respectivement le nombre de nombres impairs et pairs du tableau. N'utilisez pas de boucle for, while ou forEach.

Exemples :

```js
countOddsAndEvens([11, 2, 36, 4, 15]) ; // renvoie {odds : 2, pairs : 3}
countOddsAndEvens([1, 2, 3, 4, 5, 5, 99, 101]) ; // renvoie {odds : 6, pairs : 2}
```