+++
pre = '<b>2. </b>'
title = "Composants contrôlés"
weight = '520'
draft = false 
+++

Lorsqu’on crée un formulaire en HTML, les champs `<input>`, `<textarea>`, ou `<select>` gèrent généralement leur propre état (ce qu’on appelle des *composants non contrôlés*).

En React, la bonne pratique est d’utiliser des **composants contrôlés** :  
Cela signifie que c’est **React qui garde le contrôle sur la valeur du champ**, grâce au `state`.

---

### En quoi est-ce pertinent d'utiliser des composants contrôlés ?
- On peut **synchroniser l’interface utilisateur** (UI) avec des données internes.
- On peut valider, filtrer ou transformer les données au fur et à mesure que l’utilisateur tape.
- On garde le **plein contrôle sur la logique du formulaire**.

### Exemple simple

Voici un champ de texte contrôlé par React :

```jsx
import React from "react"

export default function App() {
  const [name, setName] = React.useState("")

  function handleChange(event) {
    setName(event.target.value)
  }

  return (
    <div>
      <label>Nom :
        <input 
          type="text"
          value={name}
          onChange={handleChange}
        />
      </label>
      <p>Bonjour, {name} !</p>
    </div>
  )
}
```
**Explication** : À chaque frappe de l’utilisateur, la valeur de l’*input* est mise à jour dans le *state*, puis l’interface se *re-render* automatiquement avec cette nouvelle valeur.

- Le *state* `name` contient la valeur du champ texte.
- L’attribut `value={name}` relie le champ à React : c’est un composant contrôlé.
- La fonction `handleChange` est appelée à chaque modification, ce qui met à jour le state avec la nouvelle valeur.

### Exercice 1 — crée ton propre champ contrôlé
En observant l'enxemple ci-haut, reproduis l’exercice suivant :
- Crée un champ de type text avec une *value* liée à un *state* nommé `email`.
- Gère le changement de valeur avec une fonction `handleChange`.
- Affiche dynamiquement le texte entré en dessous de l’*input*.

### Exercice 2 — champ mot de passe
Ajoute un deuxième champ contrôlé pour le mot de passe (*password*) et affiche-le en clair en dessous (à des fins de test uniquement).

En bonus : essaie de réutiliser une seule fonction handleChange pour gérer les deux champs.

