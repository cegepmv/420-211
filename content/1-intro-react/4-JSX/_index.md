+++
pre = '<b>4. </b>'
title = "JSX"
weight = '240'
draft = false
+++
------------

React a introduit la syntaxe **JSX**, une extension de JavaScript qui permet d’écrire du HTML directement dans le code JS. Cette combinaison rend le développement plus intuitif et favorise une meilleure organisation de l’interface.

### ReactElement et createElement()
JSX peut donner l’impression que React écrit du HTML, mais ce n’est **pas vraiment le cas**.

##### Sans JSX
```jsx
import { createElement } from "react"

const reactElement = createElement("h1", null, "Hello de createElement!")
```

Ce code ne crée pas un élément HTML mais un **objet JavaScript** appelé *ReactElement* qui possède toutes les propriétés nécessaires à *React* pour *render* l'élément. Vous pouvez faire un `console.log(reactElement)` afin d'explorer les différentes ropriétés de cet objet.

##### Équivalence JSX / createElement
```jsx
const reactElement = <h1><span>Je suis dans un span</span></h1>
```

est équivalent (conceptuellement) à :
```jsx
const reactElement = createElement(
  "h1",
  null,
  createElement("span", null, "Je suis dans un span")
)
```

👉 JSX est simplement une syntaxe plus lisible pour créer des objets React.