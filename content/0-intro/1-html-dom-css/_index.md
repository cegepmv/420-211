+++
pre = '<b>1. </b>'
title = 'HTML, DOM et CSS'
weight = '01'
draft = false
+++

### Structure d’un document HTML
Un document HTML se compose d’éléments organisés comme une hiérarchie ayant la forme d’une arbre inversé. Chaque noeud dans cet arbre correspond à un type d’élément HTML qui peut avoir plusieurs noeuds enfants et au maximum un parent. Seule la racine (le noeud `document`, au sommet de la hiérarchie) n’a pas de parent.

L’exemple suivant correspond à un document HTML simple:

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

Ce qui correspond au modèle suivant:

![DOM](/images/010-dom.svg)


### Objet document
Javascript comprend un objet nommé `document` qui permet d’accéder aux informations du DOM, de modifier des valeurs d’attributs ou du texte, d’ajouter, de supprimer ou de déplacer des éléments HTML, etc.

L’objet `document` comprend plusieurs méthodes pour accéder aux éléments du DOM; Parmi celles-ci:

`getElementById()`

Retourne l’élément HTML dont l’attribut id correspond à la valeur passée.

`getElementByTagName()`

Retourne une collection d’éléments HTML dont les noms correspondent à la valeur passée.

`getElementByClassName()`

Retourne une collection d’éléments HTML dont les attributs class correspondent à la valeur passée.

Par exemple pour le code HTML suivant:

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


### Propriétés des éléments
Les éléments HTML contiennent d’innombrables propriétés et méthodes qu’on peut utiliser pour en modifier le contenu. Ici nous verrons les propriétés `innerHTML` et `style`.

{{% notice style="info" title="Note"%}}
Pour la référence complète de l’objet `Element` du DOM: https://www.w3schools.com/jsref/dom_obj_all.asp.
{{% /notice %}}


#### innerHTML

Permet d’accéder le contenu HTML d’un élément ou de le modifier. Par exemple, pour le document HTML de l’exemple plus haut:

```js
let el = document.getElementById("par1");
el.innerHTML="Bonjour";
```

Le texte “Premier paragraphe” sera remplacé par “Bonjour”.

Attention, le texte ainsi inséré est interprété comme du HTML. On peut ainsi modifier indirectement la structure du DOM; par exmeple:

```js
let elems = document.getElementsByClassName("parag");
for (let i=0;i<elems.length;i++) {
    elems[i].innerHTML="<h1>Bonjour</h1>";
}
```

Les deux éléments `<p>` contiendront chacun un élément `<h1>` ayant le texte “Bonjour”.

#### style

La propriété `style` permet de changer les attributs de style. Tous les styles qui peuvent être définis par l’attribut HTML “style” ou dans un fichier CSS sont accessibles par javascript. Les noms des styles sont légèrement différents cependant car ils suivent la nomenclature “camelCase”: par exemple, la propriété CSS background-color est appelée backgroundColor dans javascript.

Par exemple, pour mettre en gras le texte des paragraphes d’un document:

```js
let elems = document.getElementsByTagName("p");
for (let i=0;i<elems.length;i++) {
    elems[i].style.fontWeight="bold";
}
```

{{% notice style="info" title="Note"%}}
Pour la référence complète des propriétés de style : https://www.w3schools.com/jsref/dom_obj_style.asp
{{% /notice %}}

### CSS

Il est possible de modifier l’apparence des éléments d’une page directement dans le code HTML en utilisant les attributs de style. Par exemple, pour changer la couleur du texte d’un paragraphe:

```html
<div>
    <p>Texte normal</p>
    <p style="color:red">Texte rouge</p>
    <p style="background-color:yellow">Arrière-plan jaune</p>
</div>
```

On recommande cependant de regrouper ces propriétés dans un fichier CSS: ceci permet de centraliser les éléments de style et de permettre plus facilement les modifications. Par exemple, si on souhaite que les citations dans un texte soient en italique, sans serif et de couleur grise, on pourra définir une classe nommée `quote` dans un fichier CSS et y spécifier ces propriétés typographiques, comme suit:

```css
.quote {
    font-family: sans-serif;
    color: grey;
    font-style: italic;
}
```

Par la suite, on attribue la classe `quote` à l’élément HTML dont on veut modifier le style:

```html
<p class="quote">Alea Jacta Est</p>
```

Pour que le navigateur puisse retrouver le fichier CSS où le style est défini, il faut y ajouter une référence dans le fichier HTML dans un élément `<link>`. En supposant que le fichier qui contient les styles se nomme styles.css, on aura donc le code HTML suivant:

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

### Exercices

#### Exercice 1

À partir du DOM suivant, faites le fichier HTML correspondant (Nommez votre fichier *exercice-dom-1.html*) :

![DOM](/images/0-intro/011-ex1.png)

#### Exercice 2
Dans le document *exercice-dom-2.html*, les éléments ont des attributs `id`. En utilisant des appels à la fonction `getElementById()`, remplacez les mots "apple", "pear" et "banana" par "pomme", "poire" et "banane". (vous devez créer le fichier *exercice-dom-2.js*)

#### Exercice 3
Dans le document *exercice-dom-3.html*, certains éléments ont un attribut `class`. Créez le fichier exercice-dom-3.js et utilisez la fonction `getElementsByClass()`, pour modifier le style du texte afin que celui-ci utilise la fonte Arial et soit écrit en bleu.

#### Exercice 4 
À partir du document *exercice-dom-4.html*, définissez la fonction associée au bouton pour basculer en mode sombre en modifiant les styles des éléments HTML. 
Vous pouvez utiliser le site suivant pour les références aux couleurs : https://htmlcolorcodes.com/. 

Le résultat devrait ressembler à ceci (les titres sont en vert pâle et le texte en gris) :

![DOM](/images/0-intro/012-ex4.jpg)

#### Exercice 5
En utilisant un fichier css, définissez des classes de style pour obtenir la page suivante à partir du fichier *s2-exercice1.html* fourni : 