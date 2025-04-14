+++
pre = '<b>4. </b>'
title = "Introduction aux “hooks” "
weight = '500'
draft = false 
+++

Nous avons découvert, dans le module précédent, comment React gère l'état avec `useState` et comment afficher dynamiquement du contenu avec le rendu conditionnel. Ces concepts nous ont certes permis de créer des composants plus interactifs et réactifs, mais `useState` n’est en réalité qu’un premier aperçu d’un ensemble d’outils très puissants fournis par React ; les *hooks*.

### Qu'est-ce qu'un *hook* ?

Un *hook* est une **fonction spéciale** fournie par React qui permet à un **composant fonctionnel** de gérer des fonctionnalités avancées, comme :
- l'état (`useState`),
- les effets de bord (`useEffect`),
- l'accès au DOM (`useRef`),
- la gestion de contexte (`useContext`),
- la mémorisation de valeurs (`useMemo`, `useCallback`), etc.

Avant leur introduction, il fallait utiliser des **composants de classe** pour accéder à ces fonctionnalités.  
Depuis React 16.8, les *hooks* permettent d’écrire des composants **fonctionnels** tout en leur donnant accès à **l’état, au cycle de vie, et plus encore** — de façon plus simple et modulaire. Les *hooks* ont été introduits pour permettre aux composants fonctionnels de devenir aussi puissants que les composants basés sur les classes, voire plus !

---

À travers ce module, nous allons explorer ces aspects un à un, en particulier :
- L’approche fonctionnelle en React
- Les composants contrôlés pour gérer les formulaires
- La récupération de données depuis une API 
- La gestion des *side effects* et de leur dépendances
- L'utilisation des *refs* (accéder au DOM / stocker des valeurs persistantes)

### Focus sur `useEffect` 
Avec React, les composants sont conçus pour être **purs** : cela signifie qu’ils doivent simplement **recevoir des données (*props*, *state*)** et **retourner une interface utilisateur (UI)**.
Cependant, dans le monde réel, un composant a souvent besoin de faire des actions dites **impures**, comme :

- Récupérer des données d’un serveur
- Écouter un événement du navigateur
- Modifier le `document.title`
- Attacher un écouteur d’événement (ex. : scroll, resize)
- Lancer une animation ou un minuteur...

Ces actions sont appelées **effets de bord** (*side effects*), car elles vont au-delà du simple affichage ; elles affectent le monde extérieur au composant.

C’est exactement pour ce genre de situations que React nous fournit le hook `useEffect`.

> `useEffect` permet d’exécuter du code **après** que le composant a été affiché à l’écran, et de contrôler **à quelle fréquence** cet effet est déclenché.

Nous allons l’explorer en détail dans les sections suivantes.
