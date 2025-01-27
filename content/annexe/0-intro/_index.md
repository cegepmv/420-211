+++
title = "JS - Exercices préalables"
weight = '01'
draf = true
+++

---

Cette section propose une série d'exercices pour pratiquer les bases de JavaScript ainsi que la manipulation du DOM. 

### 1. Manipulation des variables et types de données
**Objectif** : Comprendre comment manipuler les variables, les types de données et les structures de contrôle.

**Exercice**
1. Créez une variable `nom` contenant votre prénom.
2. Créez une constante `age` contenant votre âge.
3. Ecrivez une fonction qui retourne une chaîne de caractères comme :  
   ```javascript
   "Bonjour, je m'appelle [nom] et j'ai [age] ans."
   ```
4. Testez la fonction avec vos variables.
---
### 2. Les tableaux et les boucles
**Objectif** : Savoir manipuler des tableaux et parcourir leurs éléments.

**Exercice**
1. Créez un tableau contenant les nombres suivants : `[10, 20, 30, 40, 50]`.
2. Écrivez un script qui affiche chaque élément du tableau dans la console à l'aide d'une boucle `for`.
3. Modifiez le script pour calculer et afficher la somme des éléments du tableau.
```javascript
const numbers = [10, 20, 30, 40, 50];
// Votre code ici
```

**Exercice**
1. Créez un tableau 2D représentant une grille de 3x3 cases (par exemple, un tableau contenant des "X" et "O").
2. Affichez chaque ligne dans la console avec une boucle.

```javascript
const grille = [
  ["X", "O", "X"],
  ["O", "X", "O"],
  ["X", "O", "X"],
];

// Votre code ici
```
---
### 3.  Les objets et les fonctions
**Objectif** : Apprendre à manipuler des objets et comprendre leur structure.

**Exercice**
1. Créez un objet `user` avec les propriétés suivantes :
   - `nom` : votre prénom.
   - `age` : votre âge.
   - `estEtudiant` : une valeur booléenne indiquant si vous êtes étudiant.
2. Ajoutez une méthode `sePresenter` qui affiche une présentation de l'utilisateur sous forme de chaîne de caractères ; : "Bonjour, je m'appelle [nom], j'ai [age] ans et je vis à [ville]."
3. Appelez la méthode et affichez le résultat dans la console.

```javascript
const personne = {
  nom: "Alice",
  age: 25,
  ville: "Montréal",
  // Votre code ici
};

console.log(personne.sePresenter());
```
**Exercice**
1. Créez une fonction appelée `estPair` qui prend un nombre en paramètre et retourne `true` s'il est pair, `false` sinon.
2. Appelez cette fonction pour tester les nombres de 1 à 10 et affichez le résultat dans la console.
```javascript
function estPair(nombre) {
  // Votre code ici
}

// testez la fonction avec une boucle
```
---

### 4. La déstructuration
**Objectif** : Comprendre la déstructuration des objets et des tableaux.

**Exercice**
1. Utilisez la déstructuration pour extraire `nom` et `age` de l'objet `user` créé précédemment.
2. Créez un tableau contenant trois couleurs (par exemple : "rouge", "vert", "bleu") et utilisez la déstructuration pour assigner ces valeurs à trois variables distinctes.

---

### 5. Les fonctions et les conditions
**Objectif** : Travailler avec des fonctions, manipuler des structures conditionnelles et des boucles simples.

**Exercice**
1. Demandez à l'utilisateur d'entrer un nombre via `prompt`.
2. Écrivez un script qui vérifie si ce nombre est :
   - Pair ou impair.
   - Positif ou négatif.
3. Affichez un message correspondant dans la console.
```javascript
const userInput = parseInt(prompt("Entrez un nombre :"), 10);
// Votre code ici
```
**Exercice**
1. Ecrivez une fonction `compterJusqua` qui prend un nombre en paramètre et utilise une boucle `for` pour afficher tous les nombres de 1 jusqu'à ce nombre inclus.

---

### 6. La manipulation de chaînes de caractères
**Objectif** : Savoir manipuler des chaînes de caractères.

**Exercice**
1. Créez une chaîne de caractères contenant une phrase (par exemple : "JavaScript est génial").
2. Ecrivez une fonction qui retourne la longueur de cette chaîne.
3. Ecrivez une fonction qui convertit cette chaîne en majuscules.
4. Ecrivez une fonction qui remplace un mot dans la chaîne (par exemple, remplacez "génial" par "super").

---

### 7. Les opérations mathématiques
**Objectif** : Travailler avec des nombres et des calculs simples.

**Exercice**
1. Ecrivez une fonction `addition` qui prend deux nombres en paramètres et retourne leur somme.
2. Ecrivez une fonction `calculerSurfaceCarre` qui prend la longueur d'un côté d'un carré et retourne sa surface.
3. Ecrivez une fonction `calculerPerimetreRectangle` qui prend la longueur et la largeur d'un rectangle et retourne son périmètre.
---
# Manipulation du DOM

### 8. Modification du contenu HTML
**Objectif** : Pratiquer la manipulation du DOM avec `document.getElementById` et `innerHTML`.

**Exercice** 
1. Créez une page HTML contenant une balise `<div>` avec l'identifiant `message`.
2. Écrivez un script JavaScript qui modifie le contenu de la balise pour afficher "Bonjour, monde !".

**Exemple de départ :**
```html
<div id="message">Texte initial</div>
<script>
  // Votre code ici
</script>
```
---
### 7. Modification de styles CSS
**Objectif** : Appliquer des styles en utilisant `style`.

**Exercice** 
1. Créez une page HTML contenant un bouton `<button>` avec l'identifiant `changeStyle`.
2. Ajoutez une balise `<p>` contenant du texte.
3. Écrivez un script JavaScript qui change la couleur et la taille de la police du texte lorsque l'utilisateur clique sur le bouton.

**Exemple de départ :**
```html
<p id="text">Texte à modifier</p>
<button id="changeStyle">Changer le style</button>
<script>
  // Votre code ici
</script>
```
---
### 8. Ajout d'éléments au DOM
**Objectif** : Ajouter dynamiquement des éléments HTML.

**Exercice** 
1. Créez une page HTML contenant une balise `<ul>` vide avec l'identifiant `liste`.
2. Ajoutez un bouton avec l'identifiant `addItem`.
3. Écrivez un script JavaScript qui ajoute un nouvel élément `<li>` avec un texte spécifique (par exemple, "Nouvel élément") chaque fois que le bouton est cliqué.

**Exemple de départ :**
```html
<ul id="liste"></ul>
<button id="addItem">Ajouter un élément</button>
<script>
  // Votre code ici
</script>
```
---

### 9. Validation de formulaire
**Objectif** : Vérifier les entrées utilisateur en JavaScript.

**Exercice** 
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
  // Votre code ici
</script>
```