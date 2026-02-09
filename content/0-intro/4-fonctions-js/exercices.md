+++
title = 'Exercices'
weight = '141'
draft = false
+++
-------------

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