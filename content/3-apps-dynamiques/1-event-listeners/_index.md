+++
pre = '<b>1. </b>'
title = "Écouteurs d'évènements"
weight = '410'
draft = false 
+++

En Javascript, on utilise des **écouteurs d'évènenements** (*Event Listeners*) pour permettre à l'utilisateur d'interagir avec notre application.

Dans une application Javascript "vanille", il y a 2 façons d'ajouter des événements :

+ Avec la méthode `.addEventListener()` : 

```html
<button id="btn">
```

```js
const btn = document.getElementById('btn');

function handleClick() {
  console.log("Le bouton a été cliqué");
}

btn.addEventListener("click", handleClick);
```

+ Avec `onclick="fonction()"` sur l'élément HTML qu'on veut écouter : 

```html

<button onclick="fonction()">

```

```js
function fonction() {
    
    // Tâche à faire quand le bouton est cliqué
    console.log("Le bouton a été cliqué");
}
```

Cette deuxième méthode ressemble beaucoup à celle qu'on utilise avec React. Par exemple. Si on veut faire en sorte que, lorsque nous cliquons sur un bouton, quelque chose est affiché dans la console, il suffit simplement d'ajouter un `onClick={fonction}` au bouton. Contrairement à la méthode précédente, vous remarquerez qu'**on utilise un C majuscule** :

```jsx
export default function App() {
    function handleClick() {
        console.log("J'ai été cliqué!")
    }
    
    return (
        <>
            <img src="https://picsum.photos/640/360" />
            <button onClick={handleClick}>Bouton</button>
        </>
    )
}

```

Contrairement à la méthode JS "vanille", on n'utilise pas une chaîne de caractères. À la place, on met des accolades et on insère une fonction à l'intérieur (notez qu'**on ne met pas de parenthèses après le nom de la fonction**).

Il est aussi possible d'injecter directement la fonction entre les accolades :

```jsx
export default function App() {

    return (
        <div className="container">
            <img src="https://picsum.photos/640/360" />
            <button 
                onClick={() => console.log("J'ai été cliqué!")}>Bouton</button>
        </div>
    )
}

```


{{% notice style="info" title="Note"%}}
Pour en savoir plus sur les différents évènements disponibles, voici [un lien qui mène vers la documentation React](https://react.dev/reference/react-dom/components/common#mouseevent-handler) qui décrit les évènemnts disponibles pour la souris (qui représente la grande majorité des évènements utilisés dans les applications Web).{{% /notice %}}

#### Exemple 1
Complétez le composant `App()` pour que la fonction `handleClick()` s'exécute quand on clique sur le bouton.
{{< tabs >}}
{{% tab title="App.jsx" color="blue" %}}
```jsx
export default function App() {
   
   function handleClick() {
       console.log("J'ai été cliqué!")
   }
    
   return (
        <div className="container">
            <img src="https://picsum.photos/640/360" />
            <button>Bouton</button> 
        </div>
    )
}
```
{{% /tab %}}
{{% tab title="index.css" style="blue" %}}
```css
* {
    box-sizing: border-box;
}

body {
    margin: 0;
    padding: 30px;
    background-color: whitesmoke;
}

.container {
    display: flex;
    flex-direction: column;
    align-items: center;
}

.container > img {
    width: 100%;
    border-radius: 10px;
    transition: filter .1s ease-in-out;
}

.container > img:hover {
    filter: brightness(120%);
}

.container > button {
    width: 100%;
    border-radius: 10px;
    padding: 1rem;
    border: 2px solid lightgray;
    background-color: white;
    cursor: pointer;
    margin-top: 20px;
    font-family: 'Karla', sans-serif;
    font-size: 1.3rem;
}
```
{{% /tab %}}

{{< /tabs >}}





#### Exemple 2
Complétez le composant `App()` suivant pour afficher quelque chose sur la console lorsqu'on "survole" l'image avec la souris :

```jsx
export default function App() {
    function handleClick() {
        console.log("J'ai été cliqué!")
    }
    
    
    return (
        <div className="container">
            <img src="https://picsum.photos/640/360" />
            <button>Bouton</button>
        </div>
    )
}
```