+++
pre = '<b>4. </b>'
title = "Rendus conditionnels"
weight = "450"
draft = false
+++

Dans une application dynamique React, il est possible d'afficher du contenu sur la page en fonction de la valeur d'un *state*, en utilisant la technique du rendu conditionnel (*conditionnal rendering*).


### Rendu conditionnel avec &&

{{< tabs >}}
{{% tab title="App.jsx" color="blue" %}}
```jsx
import Joke from "./components/Joke"
import jokesData from "/src/assets/jokesData"

export default function App() {
    const jokeElements = jokesData.map(joke => {
        return (
            <Joke 
                key={joke.id}
                setup={joke.question} 
                punchline={joke.punchline} 
            />
        )
    })
    return (
        <div>
            {jokeElements}
        </div>
    )
}
```
{{< /tab >}}
{{% tab title="Joke.jsx" color="blue" %}}
```jsx
import  {useState} from "react"

export default function Joke(props) {
    const [isShown, setIsShown] = useState(false)
    
    function toggleShown() {
        setIsShown(prevShown => !prevShown)
    }
    
    return (
        <div>
            {props.setup && <h3>{props.setup}</h3>}
            {isShown && <p>{props.punchline}</p>}
            <button onClick={toggleShown}>Show punchline</button>
            <hr />
        </div>
    )
}
```
{{< /tab >}}
{{% tab title="jokesData.js" color="blue" %}}
```js
export default [
    {
        id: 1,
        question: "Que demande un zéro à un huit ?",
        punchline: "T'as mis une ceinture ?"
    },
    {
        id: 2,
        question: "Pourquoi les souris n'aiment pas jouer aux devinettes ?",
        punchline: "Parce qu'elles ont peur de donner leur langue au chat !"
    },
    {
        id: 3,
        question: "Pourquoi est-ce que les éléphants ne peuvent pas utiliser d'ordinateurs ?",
        punchline: "Parce qu'ils ont peur de la souris !"
    },
    {
        id: 4,
        question: "Quel est le légume le plus explosif ?",
        punchline: "La grenade !"
    },
    {
        id: 5,
        question: "Quel est le comble pour un électricien ?",
        punchline: "D'avoir les idées noires !"
    },
    {
        id: 6,
        question: "Quel est le comble pour un vélo ?",
        punchline: "C’est de perdre les pédales !"
    },
]
```
{{< /tab >}}
{{< /tabs >}}

#### Exercice 1
Modifiez le composant `App()` ci-dessous pour afficher le `<h1>` uniquement si le state `unreadMessages` n'est pas vide :

```jsx
import {useState} from "react"

export default function App() {
    const [unreadMessages, setUnreadMessages] = useState(["a", "b"])
    
    return (
        <div>
            <h1>Vous avez _ messages non lus!</h1>
        </div>
    )
}
```
{{% expand title="Solution" %}}
```jsx
import {useState} from "react"

export default function App() {
    const [unreadMessages, setUnreadMessages] = useState(["a", "b"])
    
    return (
        <div>
            {
                unreadMessages.length > 0 && 
                <h1>Vous avez {unreadMessages.length} messages non lus!</h1>
            }
        </div>
    )
}
```
{{% /expand %}}

#### Exercice 2
Continuez l'exercice 1 en faisant en sorte que lorsqu'il y a 0 messages non lus, le composant affiche "Vous n'avez aucun message à lire"
{{% expand title="Solution" %}}
```jsx
import {useState} from "react"

export default function App() {
    const [unreadMessages, setUnreadMessages] = useState(["a", "b"])
    
    return (
        <div>
            {
                unreadMessages.length > 0 && 
                <h1>Vous avez {unreadMessages.length} messages non lus !</h1>
            }
            {
                unreadMessages.length === 0 && 
                <h1>Vous n'avez aucun message à lire !</h1>
            }
        </div>
    )
}
```
{{% /expand %}}
### Rendu conditionnel : opération ternaire
Dans le cas où nous avons besoin d'une logique *if...else*, nous pouvons aussi utiliser l'opération ternaire.

Avec l'exemple des blagues :

```jsx
import  {useState} from "react"

export default function Joke(props) {
    const [isShown, setIsShown] = useState(false)
    
    function toggleShown() {
        setIsShown(prevShown => !prevShown)
    }
    
    
    return (
        <div>
            {props.question && <h3>{props.question}</h3>}
            {isShown ? <p>{props.punchline}</p> : null}
            <button onClick={toggleShown}>{isShown ? "Cacher" : "Montrer"} punchline</button>
            <hr />
        </div>
    )
}
```

#### Exercice 1

Reprenons l'exercice de l'opération &&. Maintenant, modifiez le composant `App()` pour satisfaire les requis suivants :

+ S'il n'y a pas de messages non-lus, afficher "Vous êtes à jour !"
+ S'il y a exactement 1 message non-lu, afficher "Vous avez 1 message non-lu" (singulier)
+ S'il y a plus d'1 message non lu, afficher "Vous avez <nombre de messages non lus> messages non-lus" (pluriel).

```jsx
import {useState} from "react"

export default function App() {
    const [messages, setMessages] = useState(["Salut!", "Ça va ?"])

    return (
        <div>
            <h1></h1>
        </div>
    )
}

```
{{% expand title="Solution" %}}
```jsx
import {useState} from "react"

export default function App() {
    const [messages, setMessages] = useState(["a", "b"])


    function determineText() {
        if (messages.length === 0) {
            return "Vous êtes à jour!"
        } else if (messages.length === 1) {
            return "Vous avez 1 message non lu"
        } else {
            return `Vous avez ${messages.length} messages non lus`
        }
    }

    return (
        <div>
            <h1>{determineText()}</h1>
        </div>
    )
}
```
{{% /expand %}}

#### Exercice 2
Reprenez l'exercice du compteur du chapitre `useState()`. Créez un nouveau composant appelé `< Count />`, qui reçoit en *props* un `number` dont la valeur est celle du state `count`. Ce composant doit *render* l'élément `h2.count`. Remplacez le `h2` du composant `<App />` par une instance du composant `< Count />` nouvellement crée (en lui passant la valeur du *state* `count` avec un *props*).

#### Exercice 3
Reprenez l'exercice avec le *Card* profile (chapitre `useState()`). 

1. Déplacez le bouton/l'image de l'étoile dans son propre composant `<Star />`. Le composant devrait recevoir une propriété appelée `isFilled` qu'il utilise pour déterminer quelle icône il va afficher. (Vous devrez d'abord importer les 2 icônes d'étoiles dans ce nouveau composant).

2. Importez `<Star />` dans `<App />` puis remplacez le bouton de l'étoile par ce composant (en lui passant la valeur de `isFavorite` à son *props* `isFilled`.)

3. Essayez de trouver un moyen de modifier la valeur `isFavorite` du state `profile` dans le composant `< Star />`  


### Faire passer des données dans React
Avec React, les données sont passées d'un composant parent à un (ou des) composant(s) enfants.
Dans le cas où nos composants n'ont pas de relation parent -> enfant, ils ne peuvent pas s'échanger de données.
Pour remédier à cela, il faut **déclarer la donnée au premier composant parent commun puis faire passer cette données aux composants enfant par des *props***.

**Exemple :** 

{{< tabs >}}
{{% tab title="App.jsx" color="blue" %}}
```jsx
import { useState } from "react"
import Header from "./components/Header"
import Body from "./components/Body"

export default function App() {
    return (
        <main>
            <Header />
            <Body />
        </main>
    )
}
```
{{< /tab >}}
{{% tab title="Body.jsx" color="blue" %}}
```jsx
import React from "react"

export default function Body() {
    return (
        <section>
            <h1>Heureux de vous revoir, ___!</h1>
        </section>
    )
}
```
{{< /tab >}}
{{% tab title="Header.jsx" color="blue" %}}
```jsx
import { useState } from "react"
import avatar from "./icons/user.png"

export default function Header() {
    const [userName, setUserName] = useState("Joe")

    return (
        <header>
            <img src={avatar} />
            <p>{userName}</p>
        </header>
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
    background-color: whitesmoke;
}

header {
    height: 65px;
    box-shadow: 0px 2.98256px 7.4564px rgba(0, 0, 0, 0.1);
    display: flex;
    justify-content: flex-end;
    align-items: center;
    padding-inline: 20px;
    background-color: #dce6fd
}

header > img, header > p {
    cursor: pointer;
}

section {
    padding: 20px;
}
```
{{< /tab >}}
{{< /tabs >}}

Dans cet exemple :
+ Le composant `<Header />` déclare le *state* `userName`. 
+ **Problème :** le composant `<Body />` a aussi besoin de ce state.
+ **Solution :** déclarer le *state* au premier parent commun de `<Body />` et `<Header />` (`<App />`), puis faire passer le *state* avec des *props* :

{{< tabs >}}
{{% tab title="App.jsx" color="blue" %}}
```jsx
import { useState } from "react"
import Header from "./components/Header"
import Body from "./components/Body"

export default function App() {
    const [userName, setUsername] = useState("Joe") 
    return (
        <main>
            <Header name={userName}/>
            <Body name={userName}/>
        </main>
    )
}
```
{{< /tab >}}
{{% tab title="Body.jsx" color="blue" %}}
```jsx
import React from "react"

export default function Body(props) {
    return (
        <section>
            <h1>Heureux de vous revoir, {props.name}!</h1>
        </section>
    )
}
```
{{< /tab >}}
{{% tab title="Header.jsx" color="blue" %}}
```jsx
import React from "react"
import avatar from "./icons/user.png"

export default function Header(props) {
    const [userName, setUserName] = React.useState("Joe")

    return (
        <header>
            <img src={avatar} />
            <p>{props.name}</p>
        </header>
    )
}
```
{{< /tab >}}
{{< /tabs >}}


#### Style dynamique

Avec React, il est possible de dynamiquement changer le style d'un élément à partir d'un state. Déclarer un style à un élément est similaire à du pure HTML : en fournissant une propriété `style=` à l'élément. La seule différence, c'est que cette propriété ne reçoit pas une chaine de caractère mais un objet JavaScript.

+ HTML :
```html
<html>
    <head>
        <link rel="stylesheet" href="/index.css">
    </head>
    <body style="background-color: red">
        <div id="root"></div>
        <script src="/index.jsx" type="module"></script>
    </body>
</html>
```
+ React : 

{{< tabs >}}
{{% tab title="App.jsx" color="blue" %}}
```jsx
export default function App() {
    const [pads, setPads] = React.useState(padsData)
    const styles = {
        backgroundColor: "red"
    }
    const buttonElements = pads.map(pad => (
        <button style={styles} key={pad.id}></button>
    ))
    
    return (
        <main>
            <div className="pad-container">
                {buttonElements}
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
    background-color: #1C1917;
}

main {
    display: flex;
    justify-content: center;
    align-items: center;
}

.pad-container {
    display: grid;
    grid-template-columns: repeat(4, 100px);
    grid-template-rows: repeat(2, 100px);
    gap: 10px;
}

button {
    height: 100px;
    width: 100px;
    border: 3px solid white;
    border-radius: 5px;
    cursor: pointer;
    
}
```
{{< /tab >}}
{{< /tabs >}}


#### Exercice (Sound Pad)
{{< tabs >}}
{{% tab title="App.jsx" color="blue" %}}
```jsx
import pads from "./pads"

export default function App() {
    const [pads, setPads] = useState(padsData)
    const styles = {
        backgroundColor: "red"
    }
    const buttonElements = pads.map(pad => (
        <button style={styles} key={pad.id}></button>
    ))
    
    return (
        <main>
            <div className="pad-container">
                {buttonElements}
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
    background-color: #1C1917;
}

main {
    display: flex;
    justify-content: center;
    align-items: center;
}

.pad-container {
    display: grid;
    grid-template-columns: repeat(4, 100px);
    grid-template-rows: repeat(2, 100px);
    gap: 10px;
}

button {
    height: 100px;
    width: 100px;
    border: 3px solid white;
    border-radius: 5px;
    cursor: pointer;
    
}
```
{{< /tab >}}
{{% tab title="pads.js" color="blue" %}}
```js
export default [
    {
        id: 1,
        color: "#F18D8B",
        on: true
    },   
    {
        id: 2,
        color: "#F5C280",
        on: false
    },   
    {
        id: 3,
        color: "#EEEC79",
        on: true
    },   
    {
        id: 4,
        color: "#64ED98",
        on: true
    },   
    {
        id: 5,
        color: "#63DEED",
        on: false
    },   
    {
        id: 6,
        color: "#877FED",
        on: false
    },   
    {
        id: 7,
        color: "#A57FE9",
        on: false
    },   
    {
        id: 8,
        color: "#F289C1",
        on: true
    },   
]
```
{{< /tab >}}
{{< /tabs >}}
1. Créez un composant `<Pad />` et remplacez le `button` par `<Pad />`
2. Passez au composant `<Pad />` un *props* `color` avec la valeur du même nom provenant des objets de `padsData`.
3. Dans le composant `<Pad />`, appliquez un style *inline* au `<button>` pour définir la couleur de fond du bouton (`backgroundColor`).
4. Modifiez la classe `button` du CSS et ajoutez la classe `button.on `suivante :
```css
button {
    height: 100px;
    width: 100px;
    border: 3px solid white;
    border-radius: 5px;
    cursor: pointer;   
    opacity: 0.1;
}

button.on {
    opacity: 1;
}
```
La classe `button` donne maintenant une opacité au bouton. La classe `button.on` change la valeur de l'opacité à 1. Modifiez le code du bouton de `<Pad />` : si le bouton est activé, son `className` doit être égal à `on` (le composant devrait recevoir la propriété `on` de l'objet de `padsData.js` pour savoir si le bouton est actif ou non).

{{% expand title="Solution" %}}

App.jsx :
```jsx
export default function App() {
    const [pads, setPads] = useState(padsData)

    const buttonElements = pads.map(pad => (
        <Pad key={pad.id} color={pad.color} on={pad.on}/>
    ))
    
    return (
        <main>
            <div className="pad-container">
                {buttonElements}
            </div>
        </main>
    )
}
```

Pad.jsx :
```jsx
export default function Pad(props) {
    
    return (
        <button 
            style={{backgroundColor: props.color}}
            className={props.on ? "on" : ""}
        ></button>
    )
}
```
{{% /expand %}}

### State local vs state partagé
#### Exercice
+ Reprenez l'exercice précédent. Créez un `state` dans le composant `< Pad />` qui controle si celui-ci est actif ou non. Utilisez le props `on` pour déterminer la valeur initiale du state.

+ Créez un écouteur d'évènement pour que lorsqu'on clique sur un *Pad*, le state change de "on" à "off" et vice-versa.

{{% expand title="Solution" %}}
```jsx
export default function Pad(props) {
    const [on, setOn] = useState(props.on)
    
    function toggle() {
        setOn(prevOn => !prevOn)
    }

    return (
        <button 
            style={{backgroundColor: props.color}}
            className={on ? "on" : undefined}
            onClick={toggle}
        ></button>
    )
}
```
{{% /expand %}}

On appelle cette méthode de déclaration d'un *state* un **state dérivé** (*derived state*) car sa valeur est dérivée de la donnée initiale du composant parent (passée en *props*). Chaque composant `<Pad />` généré à partir du tableau d'objet `padsData` gère son propre state. 

+ **Problème :** Les données du composant parent peuvent différer des données des composants enfant, ce qui crée 2 sources de vérité dans notre application.

Dans notre cas, ceci ne cause pas de problème, mais imaginons que nous souhaiterions ajouter une nouvelle fonctionnalité à notre application : un bouton qui désactive/réinitialise tous les *Pads*. Nous sommes maintenant obligés de créer un *state* partagé entre tous les *Pads* : 

```jsx
export default function App() {
    const [pads, setPads] = useState(padsData)
    
    function turnAllPadsOff() {
        setPads(prevPads => prevPads.map(pad => ({
            ...pad,
            on: false
        })))
    }
    
    const buttonElements = pads.map(pad => (
        <Pad key={pad.id} color={pad.color} on={pad.on}/>
    ))
    
    return (
        <main>
            <div className="pad-container">
                {buttonElements}
            </div>
            <button className="all-off" onClick={turnAllPadsOff}>Réinitialiser</button>
        </main>
    )
}
```

#### Exercice
+ Remplissez la fonction `toggle()` ci-dessous. Celle-ci doit recevoir l'`id` du *Pad* à activer/désactiver. Elle doit utiliser la méthode `.map()` sur le tableau `pads`. Si le `pad` courant possède le même `id` que celui passé en paramètre, sa propriété `on` est inversée (de `true` à `false` ou de `false` à `true`).

+ Faites passer la fonction `toggle()` à chaque composant `<Pad />` à l'aide de *props*. Cette fonction doit être invoquée lorsqu'on clique sur le *Pad* (écouteur d'évènement).

```jsx
export default function App() {
    const [pads, setPads] = useState(padsData)
    
    function toggle(id) {
        // VOTRE CODE ICI
    }
    
    const buttonElements = pads.map(pad => (
        <Pad key={pad.id} color={pad.color} on={pad.on}/>
    ))
    
    return (
        <main>
            <div className="pad-container">
                {buttonElements}
            </div>
        </main>
    )
}
```

{{% expand title="Solution" %}}

App.jsx :
```jsx
export default function App() {
    const [pads, setPads] = useState(padsData)
    
    function toggle(id) {
        setPads(prevPads => prevPads.map(item => {
            return item.id === id ? {...item, on: !item.on} : item
        }))
    }
    
    const buttonElements = pads.map(pad => (
        <Pad toggle={toggle} id={pad.id} key={pad.id} color={pad.color} on={pad.on}/>
    ))
    
    return (
        <main>
            <div className="pad-container">
                {buttonElements}
            </div>
        </main>
    )
}
```

Pad.jsx :
```jsx
export default function Pad(props) {
    return (
        <button 
            style={{backgroundColor: props.color}}
            className={props.on ? "on" : undefined}
            onClick={() => props.toggle(props.id)}
        ></button>
    )
}
```
{{% /expand %}}