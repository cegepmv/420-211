+++
title = "Javascript"
weight = '11'
draf = true
+++

# Exercices préalables en JavaScript

Cette section propose une série d'exercices pour pratiquer les bases de JavaScript ainsi que la manipulation du DOM. Ces exercices vous permettront de développer vos compétences en programmation et en manipulation d'éléments web.

---

## Exercices Généraux

### Exercice 1: Boucles et Tableaux
**Objectif** : Utiliser les boucles pour parcourir un tableau.

1. Créez un tableau contenant les nombres suivants : `[10, 20, 30, 40, 50]`.
2. Écrivez un script qui affiche chaque élément du tableau dans la console à l'aide d'une boucle `for`.
3. Modifiez le script pour calculer et afficher la somme des éléments du tableau.

```javascript
const numbers = [10, 20, 30, 40, 50];
// Code ici
```

---

### Exercice 2: Conditions
**Objectif** : Manipuler des structures conditionnelles.

1. Demandez à l'utilisateur d'entrer un nombre via `prompt`.
2. Écrivez un script qui vérifie si ce nombre est :
   - Pair ou impair.
   - Positif ou négatif.
3. Affichez un message correspondant dans la console.

```javascript
const userInput = parseInt(prompt("Entrez un nombre :"), 10);
// Code ici
```

---

### Exercice 3: Fonctions
**Objectif** : Écrire et utiliser des fonctions.

1. Créez une fonction appelée `estPair` qui prend un nombre en paramètre et retourne `true` s'il est pair, `false` sinon.
2. Appelez cette fonction pour tester les nombres de 1 à 10 et affichez le résultat dans la console.

```javascript
function estPair(nombre) {
  // Code ici
}

// Testez la fonction avec une boucle
```

---

### Exercice 4: Objets
**Objectif** : Manipuler des objets simples.

1. Créez un objet représentant une personne avec les propriétés suivantes : `nom`, `age`, et `ville`.
2. Ajoutez une méthode `sePresenter` qui retourne une phrase comme : "Bonjour, je m'appelle [nom], j'ai [age] ans et je vis à [ville]."
3. Appelez la méthode et affichez le résultat dans la console.

```javascript
const personne = {
  nom: "Alice",
  age: 25,
  ville: "Montréal",
  // Code ici
};

console.log(personne.sePresenter());
```

---

### Exercice 5: Tableaux Multidimensionnels
**Objectif** : Manipuler des tableaux 2D.

1. Créez un tableau 2D représentant une grille de 3x3 cases (par exemple, un tableau contenant des "X" et "O").
2. Affichez chaque ligne dans la console avec une boucle.

```javascript
const grille = [
  ["X", "O", "X"],
  ["O", "X", "O"],
  ["X", "O", "X"],
];

// Code ici
```

---

## Exercices DOM

### Exercice 6: Modification du contenu HTML
**Objectif** : Pratiquer la manipulation du DOM avec `document.getElementById` et `innerHTML`.

1. Créez une page HTML contenant une balise `<div>` avec l'identifiant `message`.
2. Écrivez un script JavaScript qui modifie le contenu de la balise pour afficher "Bonjour, monde !".

**Exemple de départ :**
```html
<div id="message">Texte initial</div>
<script>
  // Code ici
</script>
```

---

### Exercice 7: Modification de styles CSS
**Objectif** : Appliquer des styles en utilisant `style`.

1. Créez une page HTML contenant un bouton `<button>` avec l'identifiant `changeStyle`.
2. Ajoutez une balise `<p>` contenant du texte.
3. Écrivez un script JavaScript qui change la couleur et la taille de la police du texte lorsque l'utilisateur clique sur le bouton.

**Exemple de départ :**
```html
<p id="text">Texte à modifier</p>
<button id="changeStyle">Changer le style</button>
<script>
  // Code ici
</script>
```

---

### Exercice 8: Ajout d'éléments au DOM
**Objectif** : Ajouter dynamiquement des éléments HTML.

1. Créez une page HTML contenant une balise `<ul>` vide avec l'identifiant `liste`.
2. Ajoutez un bouton avec l'identifiant `addItem`.
3. Écrivez un script JavaScript qui ajoute un nouvel élément `<li>` avec un texte spécifique (par exemple, "Nouvel élément") chaque fois que le bouton est cliqué.

**Exemple de départ :**
```html
<ul id="liste"></ul>
<button id="addItem">Ajouter un élément</button>
<script>
  // Code ici
</script>
```

---

### Exercice 9: Validation de formulaire
**Objectif** : Vérifier les entrées utilisateur en JavaScript.

1. Créez un formulaire HTML avec :
   - Un champ texte pour le nom (obligatoire).
   - Un champ texte pour l'email (obligatoire, doit contenir "@" dans la valeur).
   - Un bouton "Soumettre".
2. Écrivez un script JavaScript qui vérifie les champs à la soumission. Si un champ est vide ou invalide, affichez un message d'erreur sous le formulaire.

**Exemple de départ :**
```html
<form id="form">
  <label>Nom: <input type="text" id="name"></label><br>
  <label>Email: <input type="text" id="email"></label><br>
  <button type="button" id="submit">Soumettre</button>
</form>
<p id="error" style="color: red;"></p>
<script>
  // Code ici
</script>
```

---

### Exercice 10: Animation simple
**Objectif** : Créer une animation avec JavaScript en modifiant les propriétés CSS.

1. Créez une page contenant un cercle `<div>` avec une position initiale (par exemple, en haut à gauche).
2. Écrivez un script JavaScript qui déplace le cercle de gauche à droite sur la page lorsque l'utilisateur clique sur un bouton.

**Exemple de départ :**
```html
<div id="cercle" style="width: 50px; height: 50px; background-color: red; border-radius: 50%; position: absolute; top: 50px; left: 50px;"></div>
<button id="startAnimation">Animer</button>
<script>
  // Code ici
</script>
```

---

Ces exercices couvrent un éventail de concepts de base en JavaScript, allant des structures de contrôle aux manipulations du DOM. Ils sont conçus pour offrir une progression naturelle dans l'apprentissage et développer une bonne compréhension des bases de la programmation web.
