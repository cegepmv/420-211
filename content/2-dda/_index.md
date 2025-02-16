+++
pre = '<b>2. </b>'
title = "DDA"
weight = '300'
draft = false 
+++

# Application basées sur des données (data-driven applications)

L'une des grandes forces de React est la réutilisabilité des composants. Un composant bien conçu peut être utilisé plusieurs fois dans une application, avec des données différentes, permettant ainsi de réduire la duplication du code et de rendre le développement plus efficace.

**Ce que nous allons allons explorer dans ce module:**
1. L'insertion de JavaScript dans JSX
2. L'utilisation des props pour transmettre des données aux composants
3. La gestion des actifs statiques
4. La mise en correspondance des données avec les composants

### Insérer du JavaScript dans JSX
React permet d'intégrer du JavaScript directement dans le JSX à l'aide des accolades {}. 
Cela nous permet d'afficher des variables, d'effectuer des calculs ou d'utiliser des expressions JavaScript dans notre interface.

**Exemple simple :**
On peut afficher une variable directement dans du JSX :
```jsx
function Greeting() {
  const name = "Alice";
  return <h1>Bonjour, {name} !</h1>;
}
```
Dans cet exemple, la variable name est insérée dynamiquement à l'intérieur du `<h1>`.

**Exemple avec un calcul :**
On peut aussi exécuter des calculs dans JSX :
```jsx
function TotalPrice() {
  const price = 50;
  const tax = 10;
  return <p>Total : {price + tax} €</p>;
}
```
```jsx
function App() {
  return (
    <h1>Il est actuellement environ {new Date().getHours() % 12} heures</h1>
  );
}
```
Dans cet exemple, nous utilisons `new Date().getHours() % 12` pour afficher l'heure actuelle en format 12 heures.

#### Exercice dirigé : insérer du JavaScript dans JSX
Voici un exemple où nous définissons une variable timeOfDay en fonction de l'heure actuelle à l'aide d'une structure if...else :
```jsx
function App() {
  const hours = new Date().getHours();
  let timeOfDay;

  if (hours < 12) {
    timeOfDay = "morning";
  } else if (hours >= 12 && hours < 17) {
    timeOfDay = "afternoon";
  } else if (hours < 21) {
    timeOfDay = "evening";
  } else {
    timeOfDay = "night";
  }

  return (
    <h1>Good night</h1>
  );
}
```
🎯 Actuellement, le texte affiché est toujours "Good night", modifiez le `return` du composant pour que le message s'affiche dynamiquement en fonction de `timeOfDay`.

🔹 Exemple de résultat attendu :
- À 10h, l’affichage devrait être "Good morning".
- À 15h, l’affichage devrait être "Good afternoon".
- Etc.

🚀 Au travail !! 

### Les props : partager des données entre composants 
Les **props (propriétés)** permettent à un composant parent de transmettre des informations à un composant enfant. Elles sont accessibles en tant qu'attributs dans le JSX et en tant qu'objet dans le composant enfant.

**Exemple de composant avec props**
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

Voici comment nous pouvons créer ce composant qui reçoit un nom en **prop** et y accède via `props.name` :
```jsx
function WelcomeMessage(props) {
  return <h1>Bienvenue, {props.name} !</h1>;
}
```
> **Important :** Les `props` sont **en lecture seule** et ne doivent pas être modifiées à l'intérieur du composant enfant.


#### Utiliser les props pour afficher des informations dynamiques

On peut aussi passer plusieurs valeurs et y accéder avec `props.nomDeLaProp` :
**Exemple d'utilisation**
```jsx
function UserInfo(props) {
  return (
    <p>{props.name} a {props.age} ans.</p>
  );
}

function App() {
  return (
    <div>
      <UserInfo name="Alice" age={25} />
      <UserInfo name="Bob" age={30} />
    </div>
  );
}
```
Ici, `UserInfo` reçoit les props `name` et `age` et y accède dynamiquement via `props.name` et `props.age`.

#### Utiliser les props pour effectuer des calculs
On peut aussi effectuer des opérations logiques ou mathématiques dans JSX avec les props.

Voici un exemple où l’on affiche si un produit est cher ou abordable en fonction de son prix, en utilisant un opérateur ternaire :
```jsx
function PriceTag(props) {
  return <p>Prix : {props.price > 100 ? 'Cher' : 'Abordable'}</p>;
}

function App() {
  return (
    <div>
      <PriceTag price={120} />
      <PriceTag price={80} />
    </div>
  );
}
```
Dans cet exemple, nous utilisons une **expression conditionnelle** pour afficher un texte différent en fonction de la valeur de `price`:
- si le prix est supérieur à 100, l'affichage sera "Cher".
- sinon, l'affichage sera "Abordable".

#### Passer des props qui ne sont pas des chaînes de caractères 
Les props en React ne sont pas limitées aux chaînes de caractères (string) et aux nombres. On peut aussi passer des tableaux, des objets, des fonctions, et même des composants !

**Exemple : passer un tableau en prop**
On peut aussi envoyer un tableau et l'afficher sous forme de liste.
```jsx
function ShoppingList(props) {
  return (
    <ul>
      {props.items.map((item, index) => (
        <li key={index}>{item}</li>
      ))}
    </ul>
  );
}

function App() {
  return (
    <div>
      <ShoppingList items={["Pommes", "Bananes", "Oranges"]} />
    </div>
  );
}
```
`props.items` est un tableau et on l'affiche en utilisant `.map()`.

**Exemple : passer un objet en prop**

Les objets peuvent aussi être passés en **prop**, et on y accède avec `props.nomDeLaProp.nomDeLaValeur`ß.

```jsx
function UserProfile(props) {
  return (
    <p>
      {props.user.name} a {props.user.age} ans et habite à {props.user.city}.
    </p>
  );
}

function App() {
  return (
    <div>
      <UserProfile user={{ name: "Alice", age: 25, city: "Paris" }} />
      <UserProfile user={{ name: "Bob", age: 30, city: "Lyon" }} />
    </div>
  );
}
```
Ici, `props.user` est un **objet**, et on récupère ses valeurs avec `props.user.name`, `props.user.age`, etc.

**Exemple : passer une fonction en prop**

On peut aussi transmettre une **fonction** en prop pour que le composant enfant l’appelle.

```jsx
function Button(props) {
  return <button onClick={props.onClick}>Cliquez-moi</button>;
}

function App() {
  function handleClick() {
    alert("Bouton cliqué !");
  }

  return (
    <div>
      <Button onClick={handleClick} />
    </div>
  );
}

```
Ici, `props.onClick` est une **fonction**, et elle est exécutée quand le bouton est cliqué.


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
