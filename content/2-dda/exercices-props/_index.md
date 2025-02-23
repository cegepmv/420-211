+++
pre = '<b>1. </b>'
title = 'JSX et les props - exercices'
weight = '310'
draft = false
+++

La section suivante présente une série d'exercices visant à renforcer votre compréhension de la transmission des données entre composants et la réutilisabilité de ceux-ci.

---

### **Exercice 1 : Affichage dynamique d'un message d'accueil**
**Objectif** : Créez un composant `WelcomeBanner` qui affiche un message de bienvenue basé sur la prop `username`.

**Instructions**
1. Créez un composant `WelcomeBanner` qui prend une prop `username` (string) et affiche :
   `"Bienvenue sur notre site, [username] !"`.
2. Dans le composant `App`, utilisez `WelcomeBanner` avec trois utilisateurs différents (par exemple, "Alice", "Bob", "Charlie").

**Vérification**
- Vérifiez que le message s'affiche correctement pour chaque utilisateur.
- Changez la valeur de `username` dans `App` et assurez-vous que le message se met à jour dynamiquement.

**Exemple d'affichage attendu**
```
Bienvenue sur notre site, Alice !
Bienvenue sur notre site, Bob !
Bienvenue sur notre site, Charlie !
```
---

### **Exercice 2 : Afficher l'état d'un capteur**
**Objectif** : Afficher dynamiquement l'état d'un capteur (actif ou inactif) selon une prop.

**Instructions**
1. Créez un composant `SensorStatus` qui prend une prop `isActive` (booléen).
2. Si `isActive` est `true`, affichez `"Le capteur est actif."`, sinon affichez `"Le capteur est inactif."`.
3. Testez plusieurs valeurs de `isActive` dans `App` (par exemple, `true` et `false`).

**Vérification**
- Vérifiez que le texte change correctement en fonction de la valeur de `isActive`.
- Testez avec des valeurs différentes pour vous assurer que le composant réagit bien.

**Exemple d'affichage attendu**
```
Le capteur est actif.
Le capteur est inactif.
```

---

### **Exercice 3 : Vérifier la disponibilité d'une salle**
**Objectif** : Utiliser une condition avec props pour indiquer si une salle est disponible ou occupée.

**Instructions**
1. Créez un composant `RoomAvailability` qui prend une prop `isAvailable` (booléen).
2. Affichez `"Salle disponible"` si `isAvailable` est `true`, sinon `"Salle occupée"`.
3. Dans `App`, affichez `RoomAvailability` avec différentes valeurs (par exemple, `true` et `false`).

**Vérification**
- Vérifiez que le texte change en fonction de la disponibilité de la salle.
- Testez avec plusieurs valeurs pour vous assurer que le composant fonctionne correctement.

**Exemple d'affichage attendu**
```
Salle disponible
Salle occupée
```
---

### **Exercice 4 : Liste des cours disponibles**
**Objectif** : Afficher une liste de cours en utilisant un tableau passé en prop.

**Instructions**
1. Créez un composant `CourseList` qui prend une prop `courses` (tableau de strings).
2. Affichez chaque cours sous forme de `<li>`.
3. Dans `App`, testez `CourseList` avec au moins deux listes différentes (par exemple, `["Mathématiques", "Informatique", "Histoire"]` et `["Biologie", "Physique", "Philosophie"]`).

**Vérification**
- Vérifiez que chaque élément du tableau est bien affiché dans une liste.
- Testez avec des tableaux de différentes tailles pour vous assurer que le composant s'adapte.

**Exemple d'affichage attendu**
```
Cours disponibles :
- Mathématiques
- Informatique
- Histoire

Autres cours :
- Biologie
- Physique
- Philosophie
```
---

---

### **Exercice 5 : Profil d'un véhicule**
**Objectif** : Passer un objet en prop et afficher dynamiquement les informations d'un véhicule.

**Instructions**
1. Créez un composant `VehicleProfile` qui prend une prop `vehicle` (objet `{ brand, model, year }`).
2. Affichez les informations sous forme de paragraphe (par exemple, `"Toyota Corolla (2020)"`).
3. Dans `App`, affichez `VehicleProfile` pour plusieurs véhicules (par exemple, `{ brand: "Toyota", model: "Corolla", year: 2020 }`).

**Vérification**
- Vérifiez que les informations du véhicule sont correctement affichées.
- Testez avec plusieurs objets pour vous assurer que le composant fonctionne avec différentes données.

**Exemple d'affichage attendu**
```
Toyota Corolla (2020)
Ford Mustang (2022)
Tesla Model 3 (2023)
```

---

### **Exercice 6 : Bouton interactif pour activer un mode**
**Objectif** : Transmettre une fonction en prop et l'exécuter dans un composant enfant.

**Instructions**
1. Créez un composant `ModeButton` qui prend une prop `onActivate` (fonction).
2. Lorsque l'utilisateur clique sur le bouton, la fonction doit être exécutée.
3. Dans `App`, définissez une fonction `activateMode` qui affiche une alerte (par exemple, `"Mode activé !"`).

**Vérification**
- Vérifiez que l'alerte s'affiche bien lorsque vous cliquez sur le bouton.
- Testez avec différentes fonctions pour vous assurer que le composant est réutilisable.

---

### **Exercice 7 : Liste de tâches avec état d'achèvement**
**Objectif** : Générer dynamiquement des tâches avec un statut.

**Instructions**
1. Définissez un tableau `tasks` contenant `{ id, title, completed }`.
2. Créez un composant `TaskList` qui génère dynamiquement des tâches en utilisant `map()`.
3. Affichez `TaskList` dans `App`.

**Vérification**
- Vérifiez que chaque tâche est affichée avec son statut (✅ ou ❌).
- Testez avec plusieurs tableaux de tâches pour vous assurer que le composant s'adapte.

**Exemple d'affichage attendu**
```
- Faire les courses ✅
- Nettoyer la voiture ❌
- Étudier React ✅
```

---

### **Exercice 8 : Carte météo**
**Objectif** : Afficher des informations météo en utilisant des props.

**Instructions**
1. Créez un composant `WeatherCard` qui prend en props `{ temperature, condition }`.
2. Affichez `"Température : X°C - Condition : [condition]"`.
3. Testez différentes valeurs dans `App` (par exemple, `{ temperature: 22, condition: "Ensoleillé" }`).

**Vérification**
- Vérifiez que les informations météo sont correctement affichées.
- Testez avec plusieurs jeux de données pour vous assurer que le composant fonctionne correctement.

**Exemple d'affichage attendu**
```
Température : 22°C - Condition : Ensoleillé
Température : 15°C - Condition : Nuageux
Température : -5°C - Condition : Neigeux
```
---

---

### 🚀 **Challenge Bonus : Gestion des places de parking**
**Objectif** : Indiquer dynamiquement si une place est disponible et permettre la réservation.

**Instructions**
1. Créez un composant `ParkingSpot` qui prend `isAvailable` et `onReserve` en props.
2. Si `isAvailable` est `true`, affichez `"Place disponible"` avec un bouton `"Réserver"`.
3. Lorsqu'on clique sur `"Réserver"`, exécutez `onReserve`.
4. Testez différentes valeurs de `isAvailable` et de `onReserve` dans `App`.

**Vérification**
- Vérifiez que le texte et le bouton s'affichent correctement en fonction de `isAvailable`.
- Testez la fonction `onReserve` pour vous assurer qu'elle est bien exécutée.

**Exemple d'affichage attendu**
```
Place disponible [Réserver]
Place occupée
```
