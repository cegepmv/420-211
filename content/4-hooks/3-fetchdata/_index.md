+++
pre = '<b>3. </b>'
title = "Données externes (fetch)"
weight = '530'
draft = false 
+++

<!-- ### ⏭️ Prochaine section :  
**"Récupération de données (Fetching Data) avec `useEffect`"**
introduire fetch data 
exemple avec api pokemon  -->

Dans la majorité des applications web modernes, il est rare que **toutes les données soient définies localement** dans le code. Souvent, une application a besoin de **communiquer avec des sources de données externes** pour fonctionner correctement. Cela peut inclure :
- des appels vers un **serveur backend** (ex. : Node, Django, etc.),
- des requêtes vers une **API tierce** (ex. : API météo, API Pokémon, etc.),
- ou encore l'accès à une base de données via une couche intermédiaire.


À travers cette section, nous allons explorer la **récupération de données depuis une API** à l’aide de la méthode `fetch()`, et voir comment intégrer ces données dans une application React.

### Exemple de base
Vous disposez du code suivant, qui récupère des données depuis l’API Star Wars. 
À vous de modifier le composant de manière à afficher les donnés sur la page web :

```jsx
import React from "react"

export default function App(props) {
  const [starWarsData, setStarWarsData] = React.useState(null)

  fetch("https://swapi.dev/api/people/1")
    .then(res => res.json())
    .then(data => console.log(data))

  return (
    <div>
      <pre>{JSON.stringify({ name: "Luke" }, null, 2)}</pre>
    </div>
  )
}
```

{{% expand title="Solution" %}}
```jsx
import React from "react"

export default function App(props) {
  const [starWarsData, setStarWarsData] = React.useState(null)

  fetch("https://swapi.dev/api/people/1")
    .then(res => res.json())
    .then(data => setStarWarsData(data))

  return (
    <div>
      <pre>{JSON.stringify(starWarsData, null, 2)}</pre>
    </div>
  )
}
```
{{% /expand %}}


Dans React, lorsqu'on souhaite **récupérer des données externes** (par exemple depuis une API), on ne doit pas le faire directement dans le corps du *component*, car celui-ci peut être réexécuté plusieurs fois.

La bonne pratique consiste à utiliser le hook `useEffect`, qui permet d’exécuter une action **après** le rendu initial du composant (et à chaque mise à jour si on le souhaite).

Dans la prochaine section, nous verrons comment structurer correctement ces appels dans une application React grâce à un outil essentiel : le hook `useEffect`.