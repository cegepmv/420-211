+++
pre = '<b>4. </b>'
title = "Rendus conditionnels"
weight = '440'
draft = true 
+++

Il est possible d'afficher quelque chose sur la page en fonction de la valeur d'un state, en utilisant la technique du rendu conditionnel (*conditionnal rendering*).


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
                setup={joke.setup} 
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

solution : 
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

#### Exercice 2
Continuez l'exercice 1 en faisant en sorte que lorsqu'il y a 0 messages non lus, le composant affiche "Vous n'avez aucun message à lire"

solution : 
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

### Rendu conditionnel : opération ternaire
Dans le cas où nous avons besoin d'une logique if...else, nous pouvons aussi utiliser l'opération ternaire.

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
            {props.setup && <h3>{props.setup}</h3>}
            {isShown ? <p>{props.punchline}</p> : null}
            <button onClick={toggleShown}>{isShown ? "Hide" : "Show"} punchline</button>
            <hr />
        </div>
    )
}
```

#### Exercice

Reprenons l'exercice de l'opération &&. Maintenant, modifiez le composant `App()` pour satisfaire les requis suivants :

+ S'il n'y a pas de messages non-lus, afficher "Vous êtes à jour !"
+ S'il y a exactement 1 message non-lu, afficher "Vous avez 1 message non-lu" (singulier)
+ S'il y a plus d'1 message non lu, afficher "Vous avez <nombre de messages non lus> messages non-lus" (pluriel).

```jsx
import {useState} from "react"

export default function App() {
    const [messages, setMessages] = useState(["a", "b"])

    return (
        <div>
            <h1></h1>
        </div>
    )
}

```

solution :
```jsx
import {useState} from "react"

export default function App() {
    const [messages, setMessages] = useState(["a", "b"])


    function determineText() {
        if (messages.length === 0) {
            return "You're all caught up!"
        } else if (messages.length === 1) {
            return "You have 1 unread message"
        } else {
            return `You have ${messages.length} unread messages`
        }
    }

    return (
        <div>
            <h1>{determineText()}</h1>
        </div>
    )
}
```