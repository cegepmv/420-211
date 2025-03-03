+++
pre = '<b>3. </b>'
title = 'Objets JS'
weight = '130'
draft = false
+++

Avec JavaScript, on utilise souvent **des objets**.

Un objet est une manière de regrouper sous un même nom une structure de données qui contient plusieurs valeurs. Par exemple, une variable nommée `car` peut contenir différentes informations reliées à une voiture, comme le nom de la marque, le modèle et l’année:

```js
const car = {
    brand: "Hyundai",
    model: "Ioniq 5",
    year: 2022
}
```
Chacune de ces informations est une **propriété** de l’objet.

Pour référer aux valeurs des propriétés d’un objet, on utilise un point (par exemple `car.model`):

```js
const car = {
    brand: "Hyundai",
    model: "Ioniq 5",
    year: 2022
}

console.log(car.brand) // Affiche Hyundai
console.log(car.model) // Affiche Ioniq 5
console.log(car.year) // Affiche 2022
```
Les objets peuvent contenir d’autres objets (et même des fonctions !); par exemple un objet `person` peut avoir les propriétés `lastName`, `firstName` et `address`, et `address` peut elle-même être un objet qui contient les propriétés `number`, `street` et `city`:

```js
const person = { 
    lastName: "Chicoine", 
    firstName: "Louis", 
    address: { 
        number: "2222", 
        street:"Des Prés", 
        city:"Sherbrooke" 
    } 
}
    
console.log(person.lastName, person.firstName) // Affiche Chicoine Louis
console.log(person.address.number, person.address.street) // Affiche 2222 Des Prés
console.log(person.address.city) // Affiche Sherbrooke
```

Enfin, il est possible d’organiser les objets dans des tableaux. Dans ce cas-ci, on devra utiliser un indice entre crochets (par exemple `maListe[0]`) pour référer à un des objets du tableau. Dans l’exemple suivant, `car` est un tableau d’objets; selon la valeur de `i`, les informations affichés seront différentes :

```js
const car = [
    { brand: "Hyundai", model: "Ioniq 5", year: 2022 },
    { brand: "Audi", model: "R8", year: 2019 }
]
    
const i=0;
    
console.log(car[i].brand)
console.log(car[i].model)
console.log(car[i].year)
```