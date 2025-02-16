+++
pre = '<b>2. </b>'
title = "DDA"
weight = '300'
draft = false 
+++

# Application basées sur des données (data-driven applications)

L'une des grandes forces de React est la réutilisabilité des composants. Un composant bien conçu peut être utilisé plusieurs fois dans une application, avec des données différentes, permettant ainsi de réduire la duplication du code et de rendre le développement plus efficace.

**Ce que nous allons allons explorer dans ce module:**
1. L'utilisation des props pour transmettre des données aux composants
2. L'insertion de JavaScript dans JSX
3. La gestion des actifs statiques
4. La mise en correspondance des données avec les composants

### Les props : partager des données entre composants 
Les **props (propriétés)** permettent à un composant parent de transmettre des informations à un composant enfant. Elles sont accessibles en tant qu'attributs dans le JSX et en tant qu'objet dans le composant enfant.

**Exemple de composant avec props**
function WelcomeMessage({ name }) {
  return <h1>Bienvenue, {name} !</h1>;
}
```jsx
function App() {
  return (
    <div>
      <WelcomeMessage name="Alice" />
      <WelcomeMessage name="Bob" />
    </div>
  );
}
```
Ici, le composant `WelcomeMessage` est réutilisé avec des valeurs différentes passées via les `props`.
> **Important :** Les `props` sont **en lecture seule** et ne doivent pas être modifiées à l'intérieur du composant enfant.


### Insérer du JavaScript dans JSX
React permet d'intégrer du JavaScript directement dans le JSX à l'aide des {}.

**Exemple d'utilisation**
```jsx
function UserInfo({ name, age }) {
  return (
    <p>{name} a {age} ans.</p>
  );
}
```
On peut également utiliser des expressions plus complexes :
```jsx
function PriceTag({ price }) {
  return <p>Prix : {price > 100 ? 'Cher' : 'Abordable'}</p>;
}
```
Dans cet exemple, nous utilisons une **expression conditionnelle (opérateur ternaire)** pour afficher un texte différent en fonction de la valeur de `price`.

### Gestion des actifs statiques
Dans une application React, les images et autres fichiers statiques sont généralement placés dans le dossier public ou src/assets.

**Exemple d'image importée depuis `public`**
```jsx
function Logo() {
  return <img src="/logo.png" alt="Logo" />;
}
```
**Exemple d'image importée depuis `src/assets`**
```jsx
import logo from "./assets/logo.png";

function Logo() {
  return <img src={logo} alt="Logo" />;
}
```
L'importation permet d'assurer que l'image est bien prise en compte lors de la compilation.

### Mise en correspondance des données avec des composants
Il est courant de générer dynamiquement des composants à partir d'un tableau de données. Cela se fait généralement avec la méthode map().

**Exemple de liste d'éléments dynamiques**
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

---
### Exercice dirigé : réutilisabilité des composants
L'objectif de cet exercice est de **refactoriser** la page web précédemment développée afin d'**améliorer la réutilisabilité** des composants. Vous devrez optimiser votre implémentation en appliquant les bonnes pratiques de développement avec React, notamment en structurant le code de manière **modulaire** et en favorisant la transmission efficace des données entre les composants.

**🎯 Objectifs :**
- Identifier et extraire les éléments communs dans des **composants réutilisables**.
- Utiliser **les props** pour transmettre les données nécessaires aux composants.
- Simplifier et structurer votre code en évitant les répétitions.

**Points clés à améliorer :**
1. **Refactoriser le composant `ListItem`**
Plutôt que d'avoir plusieurs éléments statiques pour les différentes raisons d’aimer l’informatique, vous devez transformer ListItem en un composant réutilisable prenant **image, titre et description** en props.

2. **Organiser les données de manière dynamique**
Créez un tableau d’objets contenant les différentes raisons, puis affichez les éléments dynamiquement en **mappant** ce tableau pour générer les composants `ListItem`.

3. **Simplifier l’architecture des fichiers**
Si ce n'est pas encore fait, organisez les composants dans des fichiers séparés (`Header.js`, `ListItem.js`, `Footer.js`, etc.) pour améliorer la clarté et la maintenabilité de votre code.

En appliquant ces principes, vous écrirez un code **plus modulaire, maintenable et évolutif**. Cela vous permettra d’ajouter de nouvelles raisons sans modifier directement le JSX, rendant votre application plus flexible.

**🚀 À vous de jouer !** Reprenez votre implémentation précédente et appliquez ces améliorations.
