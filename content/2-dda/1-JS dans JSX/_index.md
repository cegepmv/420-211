+++
pre = '<b>1. </b>'
title = "Insérer du JS dans JSX"
weight = '310'
draft = false 
+++

React permet d'intégrer du JavaScript directement dans le JSX à l'aide des accolades `{}`. 
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