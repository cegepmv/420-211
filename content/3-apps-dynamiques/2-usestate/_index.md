+++
pre = '<b>2. </b>'
title = "useState()"
weight = '420'
draft = false 
+++

### Props vs State

+ **Props** fait référence aux **propriétés transmises à un composant** pour qu'il fonctionne correctement, de la même manière qu'une fonction reçoit des paramètres. Un composant recevant des props n'est pas autorisé à les modifier (i.e. il sont immuables).

```js
function addTwoNumbers(a, b) {
    
    // NE FAITES PAS ÇA
    a = 42
    
    return a + b
}

console.log(addTwoNumbers(1, 2))
```
```jsx
function Navbar(props) {
    
    // NE FAITES PAS ÇA
    props.logoIcon = "some-other-icon.png"
}

<Navbar logoIcon="spatula.png" />
```

+ **State** fait référence aux valeurs **gérées par le composant**, comme les variables déclarées à l'intérieur d'une fonction. Chaque fois que vous avez des valeurs changeantes qui doivent être sauvegardées/affichées, vous utiliserez probablement un *state*.

### Gestion de variables avec state

Prenons un exemple pour comprendre l'utilité des *states* en React :

{{< tabs >}}
{{% tab title="App.jsx" color="blue" %}}
```jsx
export default function App() {
    let state = "Oui"
    
    function handleClick() {
        state = "Bien sûr"
    }
    
    return (
        <main>
            <h1 className="title">Est-il important de connaître les states?</h1>
            <button onClick={handleClick} className="value">{state}</button>
        </main>
    )
}
```
{{< /tab >}}
{{% tab title="index.css" color="blue" %}}
```css
* {
    box-sizing: border-box;
}

body {
    margin: 0;
    font-family: 'Inter', sans-serif;
    background-color: #262626;
    color: #D9D9D9;
    padding: 20px;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
}

main {
    display: flex;
    flex-direction: column;
    align-items: center;
}

main > .title {
    text-align: center;
}

main > .value {
    background-color: white;
    border: none;
    border-radius: 50%;
    height: 100px;
    width: 100px;
    display: flex;
    justify-content: center;
    align-items: center;
    color: #262626;
    font-size: 2rem;
    font-weight: bold;
    cursor: pointer;
}
```
{{< /tab >}}
{{< /tabs >}}

Lorsqu'on appuie sur le bouton, une fonction `handleClick()` sensée modifier le texte du bouton est appelée. 

Copiez ce code et essayez de cliquer sur le bouton. Que remarquez-vous ?

Rien ne change sur la page ! Le simple fait de modifier une variable locale ne va pas inciter React à réexécuter notre composant. React ne va pas réagir au changement d'état et afficher la valeur mise à jour. Pour que cela puisse fonctionner, nous devons utiliser une fonction fournie par React : `React.useState()` : 

```jsx
import { useState } from "react"

export default function App() {
    const state = useState("Oui")
    
    return (
        <main>
            <h1 className="title">Est-il important de connaître les states?</h1>
            <button onClick={handleClick} className="value">{state[0]}</button>
        </main>
    )
}
```

Cette fonction prend en paramètre la valeur initiale de la variable et retourne un tableau avec deux éléments : 
+ Le premier élément est la valeur de la variable ;
+ Le deuxième est une fonction qui nous permettra de modifier la valeur de cette variable.

### Destructurer le retour de useState
Afin de mieux nommer les éléments du tableau que retourne `useState()` (et rendre notre code plus lisible), nous pouvons destructurer sa valeur de retour : 

```jsx
import React from "react"

export default function App() {
    const [isImportant, setIsImportant] = React.useState("Oui")
    
    return (
        <main>
            <h1 className="title">Est-il important de connaître les states?</h1>
            <button className="value">{isImportant}</button>
        </main>
    )
}
```
{{% notice style="info" title="Note"%}}
Par convention, on donne à la variable un nom qui décrit la valeur stockée, et on nomme la fonction `setNomDeLaVariable`
{{% /notice %}}

Le code du bouton peut donc être modifié de la façon suivante : 

```jsx
import { useState } from "react"

export default function App() {
    const [isImportant, setIsImportant] = useState("Oui")
    
    function handleClick() {
        setIsImportant("Bien sûr")
    }
    
    return (
        <main>
            <h1 className="title">Est-il important de connaître les states?</h1>
            <button onClick={handleClick} className="value">{isImportant}</button>
        </main>
    )
}
```

### Exercice
Pour le code ci-dessous :

1. Créez un *state* pour suivre la valeur de la variable `count` (valeur initiale à 0)
2. Créez une fonction `add` qui sera appelée lorsqu'on appuie sur le bouton `+`
3. Réfléchissez à un moyen d'ajouter 1 à `count` à chaque fois qu'on appuie sur le bouton `+`
4. Faites la même chose pour le bouton `-`

{{< tabs >}}
{{% tab title="App.jsx" color="blue" %}}
```jsx
import { useState } from "react"

export default function App() {
    
    return (
        <main className="container">
            
            <h1>
                Combien de fois mon enseignant va-t-il dire le mot state dans ce chapitre ?
            </h1>
            
            <div className="counter">
                <button 
                    className="minus" aria-label="Decrease count">–
                </button>
                <h2 className="count">0</h2>
                <button className="plus" aria-label="Increase count">+</button>
            </div>
        </main>
    )
}
```
{{< /tab >}}
{{% tab title="index.css" color="blue" %}}
```css
* {
    box-sizing: border-box;
}

body {
    margin: 0;
    font-family: 'Inter', sans-serif;
    background-color: #262626;
    color: #D9D9D9;
    padding: 20px;
    display: flex;
    justify-content: center;
    align-items: center;
}

.container {
    display: flex;
    flex-direction: column;
}

.container > h1 {
    font-size: 1.5rem;
    margin-top: 0;
}

.counter {
    display: flex;
    align-items: flex-end;
    align-self: center;
    margin-top: 40px;
}

.counter > button {
    height: 50px;
    width: 50px;
    border-radius: 50%;
    border: none;
    cursor: pointer;
    background-color: #737373;
    color: #D9D9D9;
    font-size: 1.5rem;
}

.counter > button:hover {
    background-color: #404040;
    color: #D9D9D9;
}

.count {
    background-color: white;
    height: 100px;
    width: 100px;
    border-radius: 50%;
    display: flex;
    justify-content: center;
    align-items: center;
    color: #262626;
    margin-block: 0 10px;
    font-size: 2rem;
}

.plus {
    margin-left: -20px;
}

.minus {
    margin-right: -20px;
    z-index: 1;
}
```
{{< /tab >}}
{{< /tabs >}}

### Mettre à jour le state avec une fonction callback
Si vous avez besoin de l'ancienne valeur du *state* pour déterminer la nouvelle, il est fortement conseillé d'utiliser une **fonction de rappel** (*callback function*) au lieu d'utiliser directement la valeur du *state*. Cette fonction callback recevra l'ancienne valeur en paramètre. Vous pourrez ensuite l'utiliser pour déterminer la nouvelle valeur :

```jsx
import { useState } from "react"

export default function App() {

    function add() {
        setCount(prevCount => prevCount + 1)
    }

    function subtract() {
        setCount(prevCount => prevCount - 1)    
    }

    return (
        <main className="container">
            
            <h1>
                Combien de fois mon enseignant va-t-il dire le mot state dans ce chapitre ?
            </h1>
            
            <div className="counter">
                <button className="minus" onClick={subtract} aria-label="Decrease count">–</button>
                <h2 className="count">0</h2>
                <button className="plus" onClick={add} aria-label="Increase count">+</button>
            </div>
        </main>
    )
}
```

### Exercice
En utilisant l'opérateur ternaire et les *states*, faites en sorte que lorsqu'on clique sur le bouton, la valeur change à "Non" si elle est à "Oui" et à "Oui" si elle est à "Non".

{{< tabs >}}
{{% tab title="App.jsx" color="blue" %}}
```jsx
export default function App() {

    return (
        <main>
            <h1 className="title">Est-ce que je sors ce soir?</h1>
            <button className="value">Oui</button>
        </main>
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
    font-family: 'Inter', sans-serif;
    background-color: #262626;
    color: #D9D9D9;
    padding: 20px;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
}

main {
    display: flex;
    flex-direction: column;
    align-items: center;
}

main > .title {
    text-align: center;
}

main > .value {
    background-color: white;
    border: none;
    border-radius: 50%;
    height: 100px;
    width: 100px;
    display: flex;
    justify-content: center;
    align-items: center;
    color: #262626;
    font-size: 2rem;
    font-weight: bold;
    cursor: pointer;
}
```
{{% /tab %}}

{{< /tabs >}}

### Manipulation de states complexes

#### Exercice 1 - Tableaux

1. Changez le code ci-dessous pour utiliser un tableau initialisé avec `useState()` à la place du tableau `thingsElements`. Initialisez le *state* avec un tableau vide (`[]`)
2. Modifiez la fonction `addFavoriteThing()` pour qu'à chaque fois qu'on appuie sur le bouton `Ajouter`, la fonction ajoute un nouvel élément "Test" à la page
+ Maintenant, faites en sorte qu'à chaque fois qu'on appuie sur le bouton, un nouvel élément du tableau `allFavoriteThings` est affiché.

{{< tabs >}}
{{% tab title="App.jsx" color="blue" %}}
```jsx
import { useState } from "react"

export default function App() {

  const myFavoriteThings = []
  const allFavoriteThings = ["💦🌹", "😺", "💡🫖", "🔥🧤", "🟤🎁", 
  "🐴", "🍎🥧", "🚪🔔", "🛷🔔", "🥩🍝"]
  const thingsElements = myFavoriteThings.map(thing => <p key={thing}>{thing}</p>)

  function addFavoriteThing() {
    myFavoriteThings.push("Test")
  }
  
  return (
    <main>
      <button onClick={addFavoriteThing}>Ajouter</button>
      <section aria-live="polite">
        {thingsElements}
      </section>
    </main>
  )
}
```
{{< /tab >}}
{{% tab title="index.css" color="blue" %}}
```css
* {
    box-sizing: border-box;
}

body {
    background-color: #70B85D;
    color: white;
    padding: 20px;
    font-size: 1.3rem;
}

main {
    display: flex;
    flex-direction: column; 
    align-items: center;
}

button {
    width: 100%;
    max-width: 300px;
    background-color: transparent;
    padding: 1rem;
    color: white;
    border: 2px solid white;
    border-radius: 50px;
    cursor: pointer;
    font-family: 'Karla', sans-serif;
    margin-bottom: 20px;
}

button:hover {
    background-color: #FFFEF1;
    color: #2C5E2E;
}

button:focus {
    outline: 0;
}

p {
    margin-block: 10px;
    font-size: 2rem;
}
```
{{< /tab >}}
{{< /tabs >}}

{{% expand title="Solution" %}}
```jsx
import { useState } from "react"

export default function App() {
    const [myFavoriteThings, setMyFavoriteThings] = useState([])

    const allFavoriteThings = ["💦🌹", "😺", "💡🫖", "🔥🧤", "🟤🎁",
        "🐴", "🍎🥧", "🚪🔔", "🛷🔔", "🥩🍝"]
    const thingsElements = myFavoriteThings.map(thing => <p key={thing}>{thing}</p>)

    function addFavoriteThing() {
        setMyFavoriteThings(
            prevFavThings => [
                ...prevFavThings,
                allFavoriteThings[prevFavThings.length]
            ]
        )
    }

    return (
        <main>
            <button onClick={addFavoriteThing}>Add item</button>
            <section aria-live="polite">
                {thingsElements}
            </section>
        </main>
    )
}
```
{{% /expand %}}

#### Exercice 2 - Objets

Pour les questions suivantes, vous pouvez utiliser les images [user.png](./images/user.png), [star-empty.png](./images/star-empty.png) et [star-filled.png](./images/star-filled.png)

1. Remplissez les valeurs du markup avec les propriétés de l'objet/state `contact`.
2. Utilisez l'opérateur ternaire pour déterminer quelle image de l'étoile (remplie ou vide) devrait être utilisée, basé sur la valeur de `contact.isFavorite`.
3. Modifiez les choses suivantes : 
    + `aria-pressed` doit être égale à la valeur de `contact.isFavorite`
    + `aria-label` devrait changer de valeur à "Supprimer des favoris" si `contact.isFavorite` est à `true`.
    + `alt` devrait être égal à `icône étoile remplie` quand elle est remplie, et `icône étoile vide` quand elle est vide

4. Modifiez la valeur de `contact.isFavorite` lorsqu'on appuie sur l'étoile. Sa valeur doit passer à `true` si elle était à `false` et `false` si elle était à `true`.

{{< tabs >}}
{{% tab title="App.jsx" color="blue" %}}

```jsx
import { useState } from "react"
import avatar from "./images/user.png"
import starFilled from "./images/star-filled.png"
import starEmpty from "./images/star-empty.png"

export default function App() {
    const [contact, setContact] = useState({
        firstName: "John",
        lastName: "Doe",
        phone: "+1 (514) 555-1212",
        email: "itsmyrealname@example.com",
        isFavorite: false
    })

    function toggleFavorite() {
        console.log("Toggle Favorite")
    }

    return (
        <main>
            <article className="card">
                <img
                    src={avatar}
                    className="avatar"
                    alt="Photo de profil de John Doe"
                />
                <div className="info">
                    <button
                        onClick={toggleFavorite}
                        aria-pressed={false}
                        className="favorite-button"
                    >
                        <img
                            src={starEmpty}
                            alt="icône étoile vide"
                            className="favorite"
                        />
                    </button>
                    <h2 className="name">
                        John Doe
                    </h2>
                    <p className="contact">+1 (212) 555-1212</p>
                    <p className="contact">itsmyrealname@example.com</p>
                </div>

            </article>
        </main>
    )
}
```
{{< /tab >}}
{{% tab title="index.css" color="blue" %}}
```css
* {
    box-sizing: border-box;
}

body {
    background-color: #0C4A6E;
    margin: 0;
    font-family: "Inter", sans-serif;
}

main {
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
}

.card {
    background-color: white;
    width: 200px;
    border: 1px solid lightgray;
    border-radius: 10px;
    height: 350px;
}

.card .avatar {
    width: 100%;
    padding: 10%;
    padding-bottom: 0;
}

.card .name {
    margin-block: 13px;
    color: #333333;
}

.card .info {
    padding: 10px;
}

.card .favorite {
    width: 25px;
    cursor: pointer;
}

.card .contact {
    font-size: 0.75rem;
    color: gray;
    margin-block: 7px;
}

.card .favorite-button {
    border: none;
    background: transparent;
}

.card .favorite-button:active {
    transform: none;
    box-shadow: none;
}
```
{{< /tab >}}
{{< /tabs >}}


{{% expand title="Solution" %}}
```jsx
import { useState } from "react"
import avatar from "./images/user.png"
import starFilled from "./images/star-filled.png"
import starEmpty from "./images/star-empty.png"

export default function App() {
    const [contact, setContact] = useState({
        firstName: "John",
        lastName: "Doe",
        phone: "+1 (212) 555-1212",
        email: "itsmyrealname@example.com",
        isFavorite: true
    })
    
    let starIcon = contact.isFavorite ? starFilled : starEmpty
    
    function toggleFavorite() {
        setContact(prevContact => ({
            ...prevContact,
            isFavorite: !prevContact.isFavorite
        }))
    }


    return (
        <main>
            <article className="card">
                <img
                    src={avatar}
                    className="avatar"
                    alt="Photo de profil de John Doe"
                />
                <div className="info">
                    <button
                        onClick={toggleFavorite}
                        aria-pressed={contact.isFavorite}
                        aria-label={contact.isFavorite ? "Supprimer des favoris" : "Ajouter aux favoris"}
                        className="favorite-button"
                    >
                        <img
                            src={starIcon}
                            alt={contact.isFavorite ? "icône étoile remplie" : "icône étoile vide"}
                            className="favorite"
                        />
                    </button>
                    <h2 className="name">
                        {contact.firstName} {contact.lastName}
                    </h2>
                    <p className="contact">{contact.phone}</p>
                    <p className="contact">{contact.email}</p>
                </div>

            </article>
        </main>
    )
}
```
{{% /expand %}}