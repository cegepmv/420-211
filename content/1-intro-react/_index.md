+++
pre = '<b>1. </b>'
title = "Introduction à React"
weight = '200'
draft = false

+++

Dans cette section, nous allons apprendre comment créer une page statique avec React.

Vous devez sûrement vous dire "*Mais je sais déjà comment faire des pages statiques...*", mais pour écrire du bon code avec React, nous devons d'abord apprendre à *réfléchir en React* et poser les fondations qui nous permettrons de développer des applications plus complexes par la suite. 

Ce que nous allons apprendre dans ce module :

1. Pourquoi il est intéressant d'utiliser React
2. Mettre en place un nouveau projet React
3. La syntaxe JSX
4. Créer nos premiers composants React
5. Styliser nos composants avec des classes CSS

### Libraire vs Frameworks

**Librairie**
+ Une collection de code réutilisable
+ Réduit le besoin d'écrire des choses complexes et répétitives en partant de zéro
+ Il est possible de contrôler comment et quand c'est utilisé dans un projet
+ Pas/peu de limites 

**Framework (cadriciel)** 
+ Architecture prédeterminée : Vous devez suivre un "pattern" de développement (*une façon de développer*) spécifique au *framework*.
+ Vous devez travailler dans les limites établies par le *framework*.
+ "Bonnes" et "mauvaises" façons d'utiliser un *framework*.
+ Un 

### Historique

![Historique frameworks](/420-211/images/1-intro-react/1-01-historique.png)


### Pourquoi React ?
+ La plus forte demande dans le marché de l'emploi
+ Large écosystème/communauté
+ Moins de "magie" dans les coulisses
+ Composable/déclaratif (plus de détails dans une prochaine section)
+ Développement actif 

### Mise en place d'un projet React local

#### Pré-requis
- Avoir `Node` installé
- Avoir `npm` installé

1. Créer un projet React avec la commande suivante :

```bash
npm create vite@latest
```

+ Dans **Project name**, tapez un nom pour votre projet
+ Dans **Select a framework**, sélectionnez `React`
+ Dans **Select a variant**, sélectionnez `JavaScript`

Ensuite, rendez vous dans le répertoire nouvellement crée, lancez la commande `npm install` puis `npm run dev` :

```bash
cd NOM_DU_PROJET
npm install
npm run dev
```

### Structure des fichiers d'un projet React
Le répertoire où l’application a été créée contient trois sous-répertoires:

+ `public`: contient la page elle-même et les fichiers qui peuvent faire l’objet d’une requête HTTP directe;
+ `src`: contient les fichiers de ressources de l’application, tant les composantes javascript que les feuilles de style, images ou autres.
+ `node_modules`: contient les dépendances externes du projet. Chaque fois que nous installons un paquet externe via `npm` (comme lorsqu'on a utilisé la commande `npm install`), il est stocké dans ce répertoire. 

#### `index.html`
Le fichier qui contient le code HTML de l’application est `index.html`. Ce fichier a la structure habituelle d’un fichier HTML (éléments HEAD, BODY, DIV etc.). Remarquez l’élément `<div>` ayant l’identifiant `root` : il constitue la racine/ la porte d'entrée de l’application; tout ce qu’il contient sera généré à partir de React.

#### `main.jsx`
Ce fichier est le point d’entrée de l’application. Il contient le code qui génère la page.

Le code commence par importer deux éléments de la librairie React, un fichier de style CSS (?!) ainsi qu'une fonction `App` à partir du fichier `App.jsx` :

```jsx
import { StrictMode } from 'react'
import { createRoot } from 'react-dom/client'
import './index.css'
import App from './App.jsx'

createRoot(document.getElementById('root')).render(
  <StrictMode>
    <App />
  </StrictMode>,
)
```
Ensuite, le code appelle la fonction `createRoot()`. Cette fonction prend en argument l'élément `<div>` que nous avons vu dans le fichier `index.html`.

Enfin, le résultat appelle la fonction `render()` avec (entre autres) l’élément `<App />` comme paramètre:
```jsx
root.render(
  <StrictMode>
    <App />
  </StrictMode>
)
```

Ceci a pour effet d’appeler la fonction `App()` du fichier `App.jsx`. C’est cette fonction qui contient le code HTML qui sera affiché dans la page.

#### `App.jsx`
Avec React, les page HTML sont construites grâce à des appels de fonction : les valeurs retournées par les fonctions seront rattachées aux différents éléments du DOM dans la page.

La fonction `App()` retourne les éléments qui seront immédiatement rattachés au DIV dont l'id est `root`:

```jsx
function App() {
  const [count, setCount] = useState(0)

  return (
    <>
      <div>
        <a href="https://vite.dev" target="_blank">
          <img src={viteLogo} className="logo" alt="Vite logo" />
        </a>
        <a href="https://react.dev" target="_blank">
          <img src={reactLogo} className="logo react" alt="React logo" />
        </a>
      </div>
      <h1>Vite + React</h1>
      <div className="card">
        <button onClick={() => setCount((count) => count + 1)}>
          count is {count}
        </button>
        <p>
          Edit <code>src/App.jsx</code> and save to test HMR
        </p>
      </div>
      <p className="read-the-docs">
        Click on the Vite and React logos to learn more
      </p>
    </>
  )
}
```

Quelques remarques au sujet de l’exemple précédent:

+ Le code est similaire à du JavaScript
+ L'extension du fichier n'est pas `.js` mais `.jsx` 
+ Le HTML retourné par la fonction n’est pas entre guillemets
+ L’attribut HTML `class` s’appelle ici `className`
+ Ces particulartiés viennent du fait que le langage utilisé dans cette page n’est pas exactement du javascript, mais une extension de javascript qu’on nomme JSX.

### Particularités de React

+ **Composable :** Vous pouvez facilement créer des "blocs" de page web réutilisables et interchangeables appelés **composants** (*components*), ce qui facilite le développement de systèmes/applications plus complexes.

Exemple d'un code pris de [la documentation de Bootstrap](https://getbootstrap.com/docs/4.0/components/navbar/) :

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
Exemple de syntaxe React qui utilise des composants (permet d'éviter la duplication de code et rend le code plus lisible) :

```jsx
<body>
    <NavBar />
    <MainContent />
    <Footer />
</body>
```

+ **Déclaratif :** React s'appuye sur sa librairie pour effectuer les tâches manuelles et fastidieuses à notre place.


![Analogie sculpture de David](/420-211/images/1-intro-react/1-02-david.png)
*Analogie avec la sculpture de David*

#### Rappel : déclaratif vs. impératif
+ **Déclaratif** (*"Qu'est ce qui doit être fait ?"*) : "Dit moi ce qui doit être fait, je me soucierai de comment le faire".
+ **Impératif** (*Comment doit-je le faire ?*) : "Décrit moi toutes les étapes sur comment faire quelque chose, et je le ferais".


