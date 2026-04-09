+++
pre = '<b>2. </b>'
title = "useEffect()"
weight = '520'
draft = false 
+++


Dans React, lorsqu'on souhaite **récupérer des données externes** (par exemple depuis une API), on ne doit pas le faire directement dans le corps du `component`, car celui-ci peut être réexécuté plusieurs fois.

La bonne pratique consiste à utiliser le hook `useEffect`, qui permet d’exécuter une action **après** le rendu initial du composant (et à chaque mise à jour si on le souhaite).

### Exemple inadéquat : appel direct dans le *component*

```jsx
fetch("https://pokeapi.co/api/v2/pokemon/pikachu")
  .then(res => res.json())
  .then(data => console.log(data)) // déclenché à chaque render !
```
Le *hook* `useEffect` permet d’exécuter une fonction après le rendu du composant, et d’en contrôler la fréquence d’exécution.

Voici comment faire le même appel de manière propre, avec `useEffect` :

```jsx
import { useState, useEffect } from "react"

export default function App() {
  const [pokemonData, setPokemonData] = useState(null)

  useEffect(() => {
    fetch("https://pokeapi.co/api/v2/pokemon/pikachu")
      .then(res => res.json())
      .then(data => setPokemonData(data))
  }, [])

  return (
    <div>
      <pre>{JSON.stringify(pokemonData, null, 2)}</pre>
    </div>
  )
}
```

<!-- Link la doc officiel de useeffects pr syntaxe  -->

### La syntaxe de `useEffect`
```jsx
React.useEffect(() => {
  // code exécuté après le rendu
}, [/* dépendances */])
```
- Le premier argument est une fonction *callback* appelée après le rendu.
- Le deuxième argument est un tableau de dépendances :
  - `[]` → l’effet est exécuté une seule fois (au montage du composant)
  - `[count]` → l’effet s’exécute à chaque fois que count change

### Exemple : démonstration avec un compteur
Ce composant affiche un bouton pour incrémenter un compteur. Un appel API est placé dans `useEffect` sans tableau de dépendances, ce qui provoque un appel à chaque *re-render* :

```jsx
import React from "react"

export default function App() {
  const [starWarsData, setStarWarsData] = React.useState({})
  const [count, setCount] = React.useState(0)

  console.log("Rendered!")

  React.useEffect(() => {
    console.log("Effect ran")
    fetch("https://swapi.dev/api/people/1")
      .then(res => res.json())
    // .then(data => setStarWarsData(data))
  })

  return (
    <div>
      <h2>The count is {count}</h2>
      <button onClick={() => setCount(prev => prev + 1)}>Add</button>
      <pre>{JSON.stringify(starWarsData, null, 2)}</pre>
    </div>
  )
}
```
<!-- 💡 Ici, comme le tableau de dépendances est absent, l’effet est exécuté à chaque re-render. -->

### Comprendre les dépendances
React compare le tableau de dépendances entre deux rendus.
Si une valeur a changé, l’effet est relancé.
- `[]` → effet exécuté une seule fois
- `[count]` → effet exécuté à chaque changement de count

Dans l’exemple précédent, comme count n’est pas utilisé dans l’effet, on peut le retirer du tableau (ou même ne pas en mettre).

### Exercice — afficher les pokémon un à un
Voici un composant qui utilise count pour charger dynamiquement un Pokémon différent depuis l’API :

```jsx
import React from "react"

export default function App() {
  const [pokemonData, setPokemonData] = React.useState({})
  const [count, setCount] = React.useState(1)

  React.useEffect(() => {
    fetch(`https://pokeapi.co/api/v2/pokemon/${count}`)
      .then(res => res.json())
      .then(data => setPokemonData(data))
  }, [count])

  return (
    <div>
      <h2>Le numéro est {count}</h2>
      <button onClick={() => setCount(prev => prev + 1)}>Afficher le prochain Pokémon</button>
      <pre>{JSON.stringify(pokemonData, null, 2)}</pre>
    </div>
  )
}
```
**Objectif** : comprendre comment `useEffect` se réexécute à chaque changement de `count`, ce qui permet d’afficher un pokémon différent à chaque clic.

Il est possible d'aller plus loin en :
- affichant le nom (`pokemonData.name`) et l’image (`pokemonData.sprites.front_default`),
- ajoutant un champ de saisie pour chercher un pokémon par son nom.


