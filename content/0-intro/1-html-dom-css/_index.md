+++
pre = '<b>1. </b>'
title = 'HTML, DOM et CSS'
weight = '110'
draft = false
+++

Cette section constitue un rappel des notions essentielles vues dans le cours *Création de sites web*. Elle vise à s’assurer que tous les étudiants partagent une base commune avant d’aborder le développement d’applications Web avec un **cadriciel moderne (React)**.

L’objectif n’est pas de tout revoir en profondeur, mais de réactiver les concepts clés : la structure HTML, le DOM, la manipulation avec JavaScript et les principes fondamentaux du CSS.

### Structure d’un document HTML
Un document HTML est composé d’éléments organisés de façon hiérarchique, formant une structure en arbre inversé appelée **DOM (*Document Object Model*)**.

+ Chaque élément HTML correspond à un **nœud** de l’arbre
+ Un nœud peut avoir plusieurs **enfants**
+ Chaque nœud a au maximum **un parent**
+ Le nœud racine (document) n’a pas de parent

#### Exemple de document HTML simple
```html
<!DOCTYPE html>
<html>
    <head>
        <script src="lib.js"></script>
        <title>Page perso</title>
    </head>
    <body>
        <h1>Bienvenue</h1>
        <div>Voici du texte</div>
        <a href="https://www.google.com">Voici un lien</a>
    </body>
</html>
```

Ce document génère un arbre DOM où les éléments `<h1>`, `<div>` et `<a>` sont des enfants de `<body>`, lui-même enfant de `<html>`

Ce qui correspond au modèle suivant:

![DOM](/420-211/images/0-intro/010-dom.svg)


### DOM et l'objet `document`
JavaScript permet d’interagir avec le DOM grâce à l’objet global `document`. Celui-ci offre des méthodes pour:

+ accéder aux éléments HTML
+ modifier le contenu ou les attributs
+ ajouter, supprimer ou déplacer des éléments
+ modifier l’apparence des éléments

#### Méthodes courantes d’accès au DOM

+ `getElementById(id)` - Retourne **un seul élément** dont l’attribut `id` correspond à la valeur fournie.

+ `getElementsByTagName(nom)` - Retourne une **collection d’éléments** ayant le nom de balise donné.

+ `getElementsByClassName(classe)` - Retourne une **collection d’éléments** possédant la classe spécifiée.

+ `querySelector(selecteur)` - Retourne le **premier élément** du DOM correspondant au sélecteur CSS fourni.

+ `querySelectorAll(selecteur)` - Retourne une **collection d’éléments** correspondant au sélecteur CSS fourni.

Les sélecteurs utilisés sont les mêmes qu’en CSS (`#id`, `.classe`, `balise`, combinaisons, etc.).

##### Exemple
```html
<!DOCTYPE html>
<html>
    <body>
        <h1 class="title">Titre</h1>
        <h2 class="title">Sous-titre</h2>
        <div>
            <p id="par1" class="parag">Premier paragraphe</p>
            <p id="par2" class="parag" >Deuxième paragraphe</p>
        </div>
    </body>
</html>
```

+ `getElementById("par1")` retourne l’élément `<p>` “Premier paragraphe”;
+ `getElementsByTagName("p")` retourne tous les éléments `<p>`;
+ `getElementsByClassName("title")` retourne les éléments `<h1>` et `<h2>`.

{{% notice style="warning" title="Attention"%}}
Lorsque ces méthodes retournent plus d’un élément, ceux-ci font partie d’une collection et on doit utiliser une boucle pour accéder à chacun individuellement.
{{% /notice %}}

##### Exemples avec `querySelector`
+ `document.querySelector("#par1")` est équivalent à `getElementById("par1")`
+ `document.querySelectorAll(".title")` est équivalent à `getElementsByClassName("title")`
+ `document.querySelectorAll("div p")` retourne les `<p>` à l’intérieur des `<div>`

{{% notice style="info" title="Remarque"%}}
Les méthodes `querySelector` et `querySelectorAll` sont plus flexibles et modernes que les méthodes traditionnelles, et sont très utilisées dans les projets actuels.
{{% /notice %}}



### Propriétés des éléments DOM
Les éléments HTML exposent de nombreuses propriétés permettant de modifier leur contenu et leur apparence. Nous nous concentrons ici sur deux propriétés fondamentales : `innerHTML` et `style`.

{{% notice style="info" title="Note"%}}
Pour la référence complète de l’objet `Element` du DOM: https://www.w3schools.com/jsref/dom_obj_all.asp.
{{% /notice %}}


#### innerHTML

La propriété `innerHTML` permet de **lire ou modifier le contenu HTML** d’un élément.

```js
let el = document.getElementById("par1");
el.innerHTML="Bonjour";
```

Le texte *Premier paragraphe* sera remplacé par *Bonjour*.

Attention, le texte ainsi inséré est interprété comme du HTML. On peut ainsi modifier indirectement la structure du DOM:

```js
let elems = document.getElementsByClassName("parag");
for (let i=0;i<elems.length;i++) {
    elems[i].innerHTML="<h1>Bonjour</h1>";
}
```

Les deux éléments `<p>` contiendront chacun un élément `<h1>` ayant le texte “Bonjour”.

#### style

La propriété `style` permet de modifier dynamiquement les styles CSS d’un élément.

+ Les propriétés CSS sont accessibles en **camelCase**
+ Exemple : `background-color` devient `backgroundColor`

```js
let elems = document.getElementsByTagName("p");
for (let i=0;i<elems.length;i++) {
    elems[i].style.fontWeight="bold";
}
```

{{% notice style="info" title="Note"%}}
Pour la référence complète des propriétés de style : https://www.w3schools.com/jsref/dom_obj_style.asp
{{% /notice %}}

### CSS: principes de base

Il est possible de modifier l’apparence des éléments d’une page directement dans le code HTML en utilisant les attributs de `style`. Par exemple, pour changer la couleur du texte d’un paragraphe:

```html
<section>
    <p>Texte normal</p>
    <p style="color:red">Texte rouge</p>
    <p style="background-color:yellow">Arrière-plan jaune</p>
</section>
```

Cependant, cette approche est déconseillée à grande échelle. On privilégie plutôt l’utilisation de **fichiers CSS externes**, qui permettent :

+ une meilleure organisation
+ une réutilisation des styles
+ une maintenance plus simple

#### Définition d'une classe CSS
```css
.quote {
    font-family: sans-serif;
    color: grey;
    font-style: italic;
}
```
#### Utilisation de la classe dans le HTML
```html
<p class="quote">Alea Jacta Est</p>
```

#### Lier un fichier CSS à un document HTML
```html
<!DOCTYPE html>
<html>
    <head>
        <link href="styles.css" rel="stylesheet">
    </head>
    <body>
        <p class="quote">Alea Jacta Est</p>
        <p>- Jules César</p>
    </body>
</html>
```

{{% notice style="info" title="Note"%}}
Une référence complète des propriétés CSS est disponible sur le site https://www.w3schools.com/cssref/index.php.
{{% /notice %}}

### Bonnes pratiques: sémantique HTML
L’utilisation de balises HTML **sémantiques** permet de donner du sens à la structure d’une page, autant pour les navigateurs que pour les moteurs de recherche, les technologies d’assistance (lecteurs d’écran) et les développeurs.

Plutôt que d’utiliser uniquement des `<div>` génériques, HTML5 propose des balises décrivant explicitement le rôle du contenu.

#### Exemples de balises sémantiques courantes

+ `<header>` : en-tête d’une page ou d’une section
+ `<nav>` : zone de navigation
+ `<main>` : contenu principal du document (une seule fois par page)
+ `<section>` : section thématique d’un document
+ `<article>` : contenu autonome (article, billet, carte, etc.)
+ `<aside>` : contenu secondaire ou complémentaire
+ `<footer>` : pied de page ou de section

#### Comparaison : non sémantique vs sémantique

❌ Structure peu sémantique :
```html
<div class="header">
    <div class="title">Mon site</div>
</div>
<div class="content">
    <div class="block">Article 1</div>
    <div class="block">Article 2</div>
</div>
```

#### Exercice 3
Dans le document [exercice-dom-3.html](/420-211/ressources/exercice-dom-3.html), certains éléments ont un attribut `class`. Créez le fichier exercice-dom-3.js et utilisez la fonction `getElementsByClassName()`, pour modifier le style du texte afin que celui-ci utilise la fonte Arial et soit écrit en bleu.

+ Utiliser `<div>` uniquement lorsque aucune balise sémantique appropriée n’existe pas.
+ Ne pas choisir une balise pour son style, mais pour sa **signification**.
+ Une bonne sémantique facilite l’**accessibilité** et la **lisibilité du code**
