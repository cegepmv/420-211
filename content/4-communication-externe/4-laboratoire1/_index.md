+++
pre = '<b>4. </b>'
title = "Laboratoire Harry Potter"
weight = '531'
draft = false 
+++

L'objectif de cet atelier est de transformer une application statique en une plateforme dynamique connectée à une API. Vous allez mettre en pratique la récupération de données asynchrones, la gestion des effets de bord avec useEffect, et l'optimisation de l'expérience utilisateur (UX).

L'API utilisée : `https://potterapi-fedeperin.vercel.app/fr/books`


Nous allons commencer par cette base : 
{{< tabs >}}
{{% tab title="App.jsx" color="blue" %}}
```jsx
import { useState } from 'react'
import './App.css'

function App() {
  const [book, setBook] = useState({
    number: 1,
    title: "Harry Potter à l'école des sorciers",
    originalTitle: "Harry Potter and the Sorcerer's Stone",
    releaseDate: "Jun 26, 1997",
    description: "Le jour de son anniversaire, Harry Potter découvre qu'il est le fils de deux sorciers célèbres, dont il a hérité de pouvoirs magiques. Il doit fréquenter une célèbre école de magie et de sorcellerie, où il se lie d'amitié avec deux jeunes qui deviendront ses compagnons d'aventure. Lors de sa première année à Poudlard, il découvre qu'un sorcier malveillant et puissant nommé Voldemort est à la recherche d'une pierre philosophale qui prolonge la vie de celui qui la possède.",
    pages: 223,
    cover: "https://raw.githubusercontent.com/fedeperin/potterapi/main/public/images/covers/1.png",
    index: 0
  })
  return (
    <main className="app-shell">
      <section className="book-browser">

        <div className="controls" aria-label="Book navigation">
          <button
            type="button"
            className="nav-button"
          >
            Left
          </button>
          <button
            type="button"
            className="nav-button"
          >
            Right
          </button>
        </div>

        <section className="card">
          <article className="book-details">
            <img
              className="book-cover"
              src={book.cover}
              alt={`Cover of ${book.title}`}
            />

            <div className="book-copy">
              <p className="book-tagline">
                Tome {book.number} • {book.releaseDate}
              </p>
              <h2>{book.title}</h2>
              <p className="description">{book.description}</p>

              <dl className="detail-grid">
                <div>
                  <dt>Titre original</dt>
                  <dd>{book.originalTitle}</dd>
                </div>
                <div>
                  <dt>Pages</dt>
                  <dd>{book.pages}</dd>
                </div>
                <div>
                  <dt>Collection</dt>
                  <dd>Harry Potter</dd>
                </div>
              </dl>
            </div>
          </article>
        </section>
      </section>
    </main>
  )
}

export default App
```
{{< /tab >}}
{{% tab title="App.css" color="blue" %}}
```css
.app-shell {
  min-height: 100vh;
  display: grid;
  place-items: center;
  padding: 32px 20px;
}

.book-browser {
  width: min(100%, 980px);
  padding: 32px;
  border-radius: 28px;
  background:
    radial-gradient(circle at top left, rgba(255, 220, 134, 0.18), transparent 28%),
    radial-gradient(circle at right bottom, rgba(127, 100, 255, 0.16), transparent 24%),
    rgba(25, 16, 34, 0.92);
  border: 1px solid rgba(255, 232, 176, 0.16);
  box-shadow: 0 24px 80px rgba(10, 5, 18, 0.46);
  backdrop-filter: blur(14px);
}

.heading-group {
  max-width: 720px;
}

.eyebrow {
  margin: 0 0 12px;
  color: #ffd36e;
  font-size: 0.85rem;
  font-weight: 700;
  letter-spacing: 0.2em;
  text-transform: uppercase;
}

.lede {
  margin: 0;
  color: rgba(247, 236, 222, 0.78);
}

.controls {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 16px;
  margin: 28px 0 24px;
}

.nav-button {
  min-width: 110px;
  padding: 12px 18px;
  border: none;
  border-radius: 999px;
  background: linear-gradient(135deg, #ffd36e, #ff9f68);
  color: #261428;
  font: inherit;
  font-weight: 800;
  cursor: pointer;
  transition:
    transform 160ms ease,
    box-shadow 160ms ease,
    opacity 160ms ease;
  box-shadow: 0 16px 34px rgba(255, 159, 104, 0.24);
}

.card {
  min-height: 460px;
  border-radius: 24px;
  padding: 24px;
  background: rgba(8, 5, 14, 0.6);
  border: 1px solid rgba(255, 255, 255, 0.08);
}

.status-view {
  min-height: 412px;
  display: grid;
  place-content: center;
  justify-items: center;
  gap: 14px;
  text-align: center;
  color: #fff5e9;
}

.spinner {
  width: 58px;
  height: 58px;
  border-radius: 50%;
  border: 5px solid rgba(255, 255, 255, 0.16);
  border-top-color: #ffd36e;
  animation: spin 0.85s linear infinite;
}

.error-message h2 {
  color: #ffbeb2;
}

.error-message p {
  max-width: 36ch;
  color: #ffe2dc;
}

.book-details {
  display: grid;
  grid-template-columns: minmax(220px, 300px) 1fr;
  gap: 28px;
  align-items: center;
}

.book-cover {
  width: 100%;
  display: block;
  border-radius: 22px;
  border: 1px solid rgba(255, 255, 255, 0.1);
  box-shadow: 0 20px 48px rgba(0, 0, 0, 0.38);
}

.book-copy h2 {
  margin: 10px 0 18px;
  font-size: clamp(2rem, 4vw, 3.4rem);
}

.book-tagline {
  margin: 0;
  color: #ffd36e;
  font-weight: 700;
  letter-spacing: 0.04em;
  text-transform: uppercase;
}

.description {
  margin-bottom: 22px;
  color: rgba(255, 245, 233, 0.82);
}

.detail-grid {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 18px;
  margin: 0;
}

.detail-grid div {
  padding: 16px;
  border-radius: 18px;
  background: rgba(255, 255, 255, 0.04);
  border: 1px solid rgba(255, 255, 255, 0.08);
}

.detail-grid dt {
  margin-bottom: 6px;
  color: #ffd36e;
  font-size: 0.8rem;
  font-weight: 700;
  letter-spacing: 0.14em;
  text-transform: uppercase;
}

.detail-grid dd {
  margin: 0;
  color: #fff5e9;
}
```
{{< /tab >}}
{{% tab title="index.css" color="blue" %}}
```css
:root {
  font-family: Georgia, 'Times New Roman', serif;
  line-height: 1.5;
  font-weight: 400;
  color: #fff5e9;
  background:
    radial-gradient(circle at top, #4b3557 0%, #24172f 32%, #120b17 72%);
  font-synthesis: none;
  text-rendering: optimizeLegibility;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

* {
  box-sizing: border-box;
}

html {
  min-height: 100%;
}

body {
  min-height: 100vh;
  margin: 0;
}

button,
input,
textarea,
select {
  font: inherit;
}

img {
  max-width: 100%;
}

#root {
  min-height: 100vh;
}

h1,
h2,
p,
dl {
  margin-top: 0;
}

h1,
h2 {
  line-height: 1.05;
  color: #fff8ef;
}

h1 {
  margin-bottom: 14px;
  font-size: clamp(2.5rem, 6vw, 4.8rem);
}

```
{{< /tab >}}
{{< /tabs >}}

## 1 - Architecture et composants
Pour rendre le code plus maintenable, commencez par créer un composant `<BookCard />`. Celui-ci reçoit l'objet `book` en *prop* et gère l'affichage (image, titre, description, détails).

## 2 - Connexion à l'API
Actuellement, les données sont "en dur" dans le `useState`. Nous voulons récupérer le livre dont l'index est 0 en utilisant `useEffect()` 

1. Initialisez le state `book` à `null`.
2. Implémentez un `useEffect`. À l'intérieur de cet effet :
    + Utilisez `fetch` pour récupérer le livre dont l'index est 0 : `https://potterapi-fedeperin.vercel.app/fr/books?index=0`
    + Utilisez `async/await` et un bloc `try/catch/finally`.
    + Mettez à jour le state `book` avec le résultat.

  <!-- + Activez l'état isLoading. -->
## 3 - Gestion de l'état et navigation
Dans `App.jsx`, nous avons besoin de suivre la position de l'utilisateur lorsqu'il veut afficher le livre précédent/suivant.

1. Initialisez un state `currentIndex` à `0` (le premier livre).
2. Créez deux fonctions pour gérer la navigation :
    + `nextBook()` : Incrémente l'index mais **ne doit pas dépasser 6**.
    + `prevBook()` : Décrémente l'index mais **ne doit pas descendre sous 0**.
3. Créez un écouteur d'évènement sur les deux boutons pour exécuter ces fonction lorsque l'utilisateur clique dessus.

## 4 - Navigation dynamique
Nous voulons pouvoir passer d'un livre à un autre à l'aide des boutons "Précédent" et "Suivant" et récupérer ses données.

1. Modifiez le `useEffect()` pour maintenant inclure une dépendance pour le state `currentIndex`
2. Utilisez `fetch` en insérant l'index dans l'URL : `https://potterapi-fedeperin.vercel.app/fr/books?index=${currentIndex}`

## 4 - Gestion de l'expérience utilisateur (loading & erreurs)

1. Créez un composant `<Spinner />` 
  ```jsx
    <div className="status-view">
      <div className="spinner" />
      <p>Loading book data...</p>
    </div>
  ```
2. État de chargement : Ajoutez un state `isLoading` (par défaut à `false`).
    + Affichez le spinner tant que les données ne sont pas arrivées.
    + Cachez-le une fois le `fetch` terminé (utilisez le bloc `finally`).
3. Gestion des erreurs : 
    + Créez un composant `<Error>` qui recoit un message d'erreur en *props* : 
      ```jsx
        <div className="status-view error-message" role="alert">
          <h2>Unable to load book</h2>
          <p>{error}</p>
        </div>
      ```
    + Ajoutez un state `error` (initialisé à `null`). Si le fetch échoue ou si la réponse n'est pas "ok", capturez l'erreur dans le `catch` et stockez le message.
    + Affichez ce message à l'utilisateur via le composant `<Error>`.

## Défis supplémentaires (Pour les mages confirmés)
+ **Boucle de navigation :** Faites en sorte que si l'on clique sur "Suivant" au dernier livre, on revienne au premier (et vice-versa).
+ **Désactivation des boutons :** Désactivez les boutons (`disabled`) pendant que `isLoading` est à vrai.
