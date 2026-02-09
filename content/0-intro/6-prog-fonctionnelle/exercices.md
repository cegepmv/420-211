
+++
title = 'Exercices'
weight = '161'
draft = false
+++
-------------

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

#### Exercice 8
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

#### Exercice 9
Utiliser `filter()`, `map()` et `reduce()` pour calculer la somme des carrés des nombres positifs de `liste1`

```js
const liste1 = [-23,230,334,-90,-76,132,-77,305]
```

#### Exercice 10

Ecrivez une fonction qui utilise `forEach()` pour afficher chaque élément d'un tableau dans la console. La fonction ne doit prendre qu'un seul argument, le tableau. La fonction ne doit PAS utiliser une boucle `for` traditionnelle.

#### Exercice 11
Ecrivez une fonction appelée `sum` qui utilise la méthode `reduce` pour additionner un tableau de nombres.

Exemples :

```js
sum([1,2,3,4,5]) ; //rend 15
sum([6,7,7]) ; //rend 20
```

#### Exercice 12
Ecrivez une fonction appelée `reduceMin` qui utilise `reduce` pour retourner le minimum d'un tableau de nombres donné en argument.

Exemples :

```js
reduceMin([2, 3, 4, 5, 1]) ; //retourne 1
reduceMin([6, 7, 7, 4]) ; // retourne 4
reduceMin([10, 0, 100, 1, -100, 20, 33]) ; //retourne -100
```

#### Exercice 13
Ecrivez une fonction nommée `countOddsAndEvens` qui prend un tableau de nombres. Cette fonction doit renvoyer un objet ayant deux propriétés : `odds` et `evens`, qui contiennent respectivement le nombre de nombres impairs et pairs du tableau. N'utilisez pas de boucle for, while ou forEach.

Exemples :

```js
countOddsAndEvens([11, 2, 36, 4, 15]) ; // renvoie {odds : 2, pairs : 3}
countOddsAndEvens([1, 2, 3, 4, 5, 5, 99, 101]) ; // renvoie {odds : 6, pairs : 2}
```