+++
pre = '<b>2. </b>'
title = "Props"
weight = '320'
draft = false 
+++

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


### Utiliser les props pour afficher des informations dynamiques

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

### Utiliser les props pour effectuer des calculs
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

### Passer des props qui ne sont pas des chaînes de caractères 
Les props en React ne sont pas limitées aux chaînes de caractères (string) et aux nombres. On peut aussi passer des tableaux, des objets, des fonctions, et même des composants !

#### Exemples

##### Passer un tableau en props
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

##### Passer un objet en prop

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

##### Passer une fonction en prop

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
