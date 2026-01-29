+++
pre = '<b>2. </b>'
title = "Pourquoi React?"
weight = '220'
draft = false
+++
---------

## Avantages
+ Forte demande sur le marché du travail
+ Communauté très active
+ Écosystème riche
+ Peu de "magie cachée"
+ Approche déclarative et composable
+ Développement actif et durable


## Particularités
### Virtual DOM

L’une des forces majeures de React est l’utilisation du **Virtual DOM** qui une représentation en mémoire du DOM réel. 

À chaque changement d’état de l'application, React compare l’ancienne version et la nouvelle version du *Virtual DOM* afin de n’**appliquer que les modifications strictement nécessaires** au navigateur. Cette optimisation améliore considérablement les performances et permet à React d’être rapide et efficace, même avec des interfaces complexes.

### Composable 
React nous permet de créer des "blocs" de page web réutilisables et interchangeables appelés **composants** (*components*).

Un composant est une unité autonome qui :
+ représente une partie de l’interface ;
+ peut recevoir des données (*props*) ;
+ peut être réutilisée ;
+ permet de construire des interfaces complexes à partir de petites briques simples.

#### Exemple: composant simple
Imaginons que l'on veuille afficher un message personnalisé dans notre application. Voici comment le faire avec un composant React :

```jsx
function Message({ name }) {
  return <h1>Hello, {name}!</h1>;
}
```
Ici, `Message` est un composant qui reçoit une **prop** `name` et l’affiche dans un élément `<h1>`.

#### Exemple: plusieurs composants enfants
Il est aussi possible de combiner plusieurs composants pour créer des interfaces plus complexes. Par exemple, un composant parent `UserCard` qui utilise un composant `UserProfile` :

```jsx
function UserProfile({ name, age }) {
  return (
    <section>
      <h2 className = "titre-principal">{name}</h2>
      <p>Age: {age}</p>
    </section>
  );
}

function UserCard() {
  return (
    <main>
      <h1>User Profile</h1>
      <UserProfile name="Alice" age={30} />
      <UserProfile name="Bob" age={25} />
    </main>
  );
}
```

Ici, le composant **`UserCard`** utilise deux instances du composant **`UserProfile`** pour afficher des informations de profil utilisateur.

{{%notice style="info" title="Ancienne approche : les composants de classe" %}}
Avant l’arrivée des *hooks*, React utilisait principalement des composants basés sur des classes. Avec cette approche, chaque composant devait obligatoirement contenir une méthode `render()` qui définissait ce que le composant affichait à l'écran.

```jsx
class HelloWorld extends React.Component {
  render() {
    return <h1>Hello, world!</h1>;
  }
}
```

Cette approche  était largement utilisée avant l’introduction des **composants fonctionnels** et les **hooks** qui ont simplifié la syntaxe en supprimant le besoin d’une classe et d’une méthode `render()`. 

Aujourd'hui, cette approche est considérée comme **legacy**.
{{%/notice %}}

#### Exemple: composant [bootstrap](https://getbootstrap.com/docs/4.0/components/navbar/)

```html
<nav class="navbar navbar-expand-lg navbar-light bg-light">
  <a class="navbar-brand" href="#">Navbar</a>
  <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
    <span class="navbar-toggler-icon"></span>
  </button>

  <div class="collapse navbar-collapse" id="navbarSupportedContent">
    <ul class="navbar-nav mr-auto">
      <li class="nav-item active">
        <a class="nav-link" href="#">Home <span class="sr-only">(current)</span></a>
      </li>
      <li class="nav-item">
        <a class="nav-link" href="#">Link</a>
      </li>
      <li class="nav-item dropdown">
        <a class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
          Dropdown
        </a>
        <div class="dropdown-menu" aria-labelledby="navbarDropdown">
          <a class="dropdown-item" href="#">Action</a>
          <a class="dropdown-item" href="#">Another action</a>
          <div class="dropdown-divider"></div>
          <a class="dropdown-item" href="#">Something else here</a>
        </div>
      </li>
      <li class="nav-item">
        <a class="nav-link disabled" href="#">Disabled</a>
      </li>
    </ul>
    <form class="form-inline my-2 my-lg-0">
      <input class="form-control mr-sm-2" type="search" placeholder="Search" aria-label="Search">
      <button class="btn btn-outline-success my-2 my-sm-0" type="submit">Search</button>
    </form>
  </div>
</nav>
```

Le code HTML d’une navbar *Bootstrap* est long et peu lisible lorsqu’il est répété.
Avec React, on peut l’encapsuler dans un composant.
```jsx
function MyAwesomeNavbar() {
    return (
        <nav className="navbar navbar-expand-lg navbar-light bg-light">
            ....
        </nav>
    )
}
```

Une fois ce composant créé, il peut être utilisé comme une balise HTML personnalisée à plusieurs endroits dans une application :
```jsx
<MyAwesomeNavbar />
```

👉 L’interface devient plus claire, plus propre et plus maintenable.

![Analogie sculpture de David](/420-211/images/1-intro-react/1-02-david.png)
*Analogie avec la sculpture de David*



### Déclaratif 
{{%notice style="tip" title="Rappel"%}}
+ **Déclaratif** (*"Qu'est ce qui doit être fait ?"*) : "Dit moi ce qui doit être fait, je me soucierai de comment le faire".
+ **Impératif** (*Comment doit-je le faire ?*) : "Décrit moi toutes les étapes sur comment faire quelque chose, et je le ferai".
{{%/notice%}}

React adopte une **approche déclarative**: on **décrit le résultat attendu**, pas les étapes techniques.

**JavaScript vanille (impératif)**
```jsx
const h1 = document.createElement("h1")
h1.textContent = "Ceci est un code impératif!"
h1.className = "header"
document.getElementById("root").appendChild(h1)
```

**React (déclaratif)**
```jsx
root.render(<h1 className="header">Ceci est un code déclaratif!</h1>)
```


👉 React masque la complexité et gère ces étapes automatiquement.


