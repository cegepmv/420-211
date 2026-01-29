+++
pre = '<b>3. </b>'
title = "Premier projet React"
weight = '230'
draft = false
+++
------------

**Pré-requis:** `Node` et `npm` installés.

Pour créer un projet *React*, nous allons utiliser l'outil *Vite* :

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

### Structure d'un projet React
Le répertoire où l’application a été créée contient trois sous-répertoires:

+ `public`: contient les fichiers accessibles directement
+ `src`: contient le code de l’application (JSX, CSS, images)
+ `node_modules`: contient les dépendances externes du projet. Chaque fois que nous installons un paquet externe via `npm` (comme lorsqu'on a utilisé la commande `npm install`), il est stocké dans ce répertoire. 

#### index.html
Ce fichier contient la structure HTML de base.

Le `<div id="root">` est le point d’entrée de React.

#### main.jsx
Ce fichier initialise l’application React et indique où afficher le composant principal.

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
Le code commence par importer deux éléments de la librairie React, un fichier de style CSS ainsi qu'une fonction `App` à partir du fichier `App.jsx`.

Ensuite, le code appelle la fonction `createRoot()`. Cette fonction prend en argument l'élément `<div>` que nous avons vu dans le fichier `index.html`.

Enfin, le résultat appelle la fonction `render()` avec (entre autres) l’élément `<App />` comme paramètre.

Ceci a pour effet d’appeler la fonction `App()` du fichier `App.jsx`. C’est cette fonction qui contient le code HTML qui sera affiché dans la page.

#### App.jsx
Avec React, les pages HTML sont générées à partir de **fonctions JavaScript**.

La fonction `App()` retourne les éléments qui seront immédiatement rattachés au `<div>` dont l'id est `root`:

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
+ Ces particulartiés viennent du fait que le langage utilisé dans cette page n’est pas exactement du JavaScript, mais une extension de JavaScript qu’on nomme **JSX**.

