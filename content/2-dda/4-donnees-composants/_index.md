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

### Conclusion 
La réutilisabilité des composants est un principe fondamental de React. En utilisant les **props**, en intégrant du **JavaScript dans JSX**, en gérant correctement les **actifs statiques**, et en **mappant des données à des composants**, vous pouvez créer des interfaces dynamiques et maintenables.

Dans la prochaine section, nous explorerons la **gestion de l'état avec useState et useEffect**.
