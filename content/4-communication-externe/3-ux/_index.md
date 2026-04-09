+++
pre = '<b>3. </b>'
title = "Gérer l'expérience utilisateur"
weight = '530'
draft = false 
+++

## useEffect et le chargement des données
Comme vu précédemment, un appel API est un **effet de bord**. La bonne pratique serait donc d'utiliser le *hook* `useEffect()` dans cette situation. 

Cependant, on ne peut pas mettre `async` directement sur la fonction de `useEffect`. On crée donc une fonction asynchrone à l'**intérieur de l'effet**.

## Gérer l'expérience utilisateur (UX) : état *loading*
Une API peut prendre 100ms ou 3 secondes pour répondre. Il est crucial d'informer l'utilisateur que quelque chose se passe.

```js
import React, { useState, useEffect } from "react";

export default function ListePokemons() {
  const [pokemon, setPokemon] = useState(null);
  const [loading, setLoading] = useState(true); // 1. État de chargement par défaut à true
  const [error, setError] = useState(null);

  useEffect(() => {
    async function fetchData() {
      try {
        setLoading(true); // On s'assure d'être en chargement au début
        const response = await fetch("https://pokeapi.co/api/v2/pokemon/1");
        
        if (!response.ok) throw new Error("Erreur lors de la récupération");

        const data = await response.json();
        setPokemon(data);
      } catch (err) {
        console.error(err.message);
      } finally {
        setLoading(false); // 2. Le chargement est terminé, peu importe le résultat
      }
    }

    fetchData();
  }, []); // [] signifie : exécuter uniquement au premier affichage

  // 3. Rendu conditionnel selon l'état
  if (loading) return <p>Chargement des données... ⏳</p>;

  return (
    { pokemon && (
      <div>
        <h1>{pokemon.name}</h1>
        <img src={pokemon.sprites.front_default} alt={pokemon.name} />
      </div>
    )}
  );
}
```

## Résumé : "Recette" React pour les API
Pour transformer votre composant en une interface dynamique connectée au monde réel, suivez ces étapes :

1. Déclarer un State pour stocker vos données (ex: [] ou null).
2. Déclarer un State Loading (true par défaut) pour gérer l'attente.
3. Utiliser useEffect avec un tableau de dépendances vide [] pour ne lancer l'appel qu'une fois.
4. Écrire une fonction async interne qui fetch, await la réponse, puis met à jour le state.
5. Utiliser le rendu conditionnel dans votre return pour afficher soit un spinner, soit vos données.

### Exercice — Défi "Explorateur de Star Wars"
En utilisant l'API `https://swapi.dev/api/people/`, créez un composant qui :

1. Affiche un message "Recherche de la force..." pendant le chargement.
2. Affiche le nom et la couleur des yeux du personnage récupéré.
3. Bonus : Ajoutez un bouton "Personnage Suivant" qui incrémente un ID dans le useEffect (souvenez-vous des dépendances !).

## Gestion des erreurs
Faire un appel réseau, c'est comme envoyer une lettre : elle peut se perdre, l'adresse peut être fausse, ou le destinataire peut refuser de l'ouvrir. En JavaScript, nous utilisons le bloc try...catch...finally.

### Pourquoi fetch est un peu "piégeux" ?
Il y a une subtilité importante avec la fonction `fetch()` : elle ne considère pas les erreurs HTTP (comme l'erreur 404 "Non trouvé" ou 500 "Erreur serveur") comme des exceptions.

+ fetch ne "crash" (ne va dans le catch) que si la requête n'a pas pu partir (ex: coupure internet totale).
+ Si le serveur répond "404 Not Found", fetch considère que la communication a réussi.
+ C'est à nous de vérifier manuellement si la réponse est "OK".

### La structure robuste (standard de l'industrie)
Voici comment structurer votre code pour qu'il soit professionnel et résistant :

```js
useEffect(() => {
  const fetchData = async () => {
    try {
      setLoading(true);
      setError(null); // On réinitialise l'erreur au début de chaque tentative

      const response = await fetch("https://api.exemple.com/data");

      // ÉTAPE 1 : Vérifier si le serveur a répondu avec un code d'erreur (404, 500, etc.)
      if (!response.ok) {
        throw new Error(`Erreur serveur : ${response.status}`); 
        // Envoyer une erreur manuellement force le passage immédiat dans le bloc catch
      }

      // ÉTAPE 2 : Tenter de lire le JSON
      const data = await response.json();
      setData(data);

    } catch (err) {
      // ÉTAPE 3 : Attraper n'est-ce que ce soit (panne réseau, erreur 404 forcée, JSON corrompu)
      console.error("Détails de l'erreur:", err);
      setError("Désolé, nous ne parvenons pas à récupérer les données.");
      
    } finally {
      // ÉTAPE 4 : Arrêter le chargement, que ce soit un succès ou un échec
      setLoading(false);
    }
  };

  fetchData();
}, []);
```
<!-- Les 3 types d'erreurs à prévoir
Il est formateur pour vos étudiants de comprendre qu'il existe différentes "pannes" :

L'erreur réseau (Client-side) : L'étudiant a mal écrit l'URL ou n'a plus de Wi-Fi. Le fetch échoue immédiatement.

L'erreur de ressource (Server-side 404) : L'URL est bonne, le serveur répond, mais le Pokémon ou l'utilisateur demandé n'existe pas.

L'erreur de format (Data-side) : Le serveur répond, mais ce n'est pas du JSON (parfois une page d'erreur HTML). Le await response.json() va alors faire planter le code. -->

<!-- Exercice de réflexion : L'expérience utilisateur (UX)
Demandez à vos étudiants : "Si une erreur survient, vaut-il mieux ne rien afficher ou afficher un bouton 'Réessayer' ?"
Défi Code : Modifiez votre composant pour ajouter un bouton "Réessayer".

Indice : Ce bouton doit simplement rappeler la fonction qui contient le fetch. -->

{{%notice style="tip" title="À retenir"%}}
+ `try` : "Essaie de faire ça".
+ `throw` : "Lance une alerte si le serveur dit que ça ne va pas".
+ `catch` : "Attrape l'alerte et décide quoi afficher à l'utilisateur (un message d'erreur)".
+ `finally` : "Quoi qu'il arrive, éteins le spinner de chargement".
{{%/notice%}}
<!-- 
Note: Cette approche permet de leur montrer que la programmation, c'est aussi de la communication. On communique avec le serveur, et on communique l'état de cette relation à l'utilisateur final. 
-->