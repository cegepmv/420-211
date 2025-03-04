+++
pre = '<b>4. </b>'
title = "Données et composants"
weight = '340'
draft = false 
+++

# Mise en correspondance
Il est courant de générer dynamiquement des composants à partir d'un tableau de données. Cela se fait généralement avec la méthode map().

### Exemple de liste d'éléments dynamiques
```jsx
const users = [
  { id: 1, name: "Alice", age: 30 },
  { id: 2, name: "Bob", age: 25 },
  { id: 3, name: "Charlie", age: 35 }
];

function UserList() {
  return (
    <ul>
      {users.map(user => (
        <li key={user.id}>{user.name} - {user.age} ans</li>
      ))}
    </ul>
  );
}
```
Dans cet exemple, chaque élément de la liste est généré dynamiquement en utilisant `map()`, et un `key` unique est attribué à chaque élément pour améliorer les performances de React.

### Exemple de liste d'objets dynamiques : Voitures

```jsx
import './App.css';
import voitures from './assets/voitures';
import Voiture from './components/Voiture';

function App() {

  const voituresElements = voitures.map(voiture => {
    return <Voiture
              marque={voiture.marque}
              model={voiture.model}
              couleur={voiture.couleur}
              annee={voiture.annee}
      />
  })

  return (
    <>
      <div className="app">
        <h1>Liste des voitures</h1>
        <div className="voiture-list">
          {voituresElements}
        </div>
      </div>
    </>
  )
}

export default App
```

### Composant Voiture
```jsx
import React from 'react';
import './Voiture.css';

function Voiture(props) {
  return (
    <div className="voiture-card">
      <h2>{props.marque} {props.model}</h2>
      <p><strong>Couleur :</strong> {props.couleur}</p>
      <p><strong>Année :</strong> {props.annee}</p>
    </div>
  );
}

export default Voiture;
```

### Données des voitures
```jsx
const voitures = [
  { id: 1, marque: "Toyota", model: "Corolla", couleur: "Bleu", annee: 2020 },
  { id: 2, marque: "Honda", model: "Civic", couleur: "Rouge", annee: 2019 },
  { id: 3, marque: "Ford", model: "Mustang", couleur: "Noir", annee: 2021 },
  { id: 4, marque: "Tesla", model: "Model 3", couleur: "Blanc", annee: 2022 },
  { id: 5, marque: "BMW", model: "X5", couleur: "Gris", annee: 2018 }
];

export default voitures;
```

### Conclusion 
La réutilisabilité des composants est un principe fondamental de React. En utilisant les **props**, en intégrant du **JavaScript dans JSX**, en gérant correctement les **actifs statiques**, et en **mappant des données à des composants**, vous pouvez créer des interfaces dynamiques et maintenables.

Dans la prochaine section, nous explorerons la **gestion de l'état avec useState et useEffect**.
