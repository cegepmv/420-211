<!-- +++
pre = '<b>2. </b>'
title = 'Javascript depuis ES5'
date = 2025-01-09T11:51:55+01:00
weight = '02'
draft = true
+++


## Variables

### Mot clé `const`

Une constante est une variable dont la valeur est fixe. Une fois déclarée sa valeur ne peut pas être modifiée.

Pour déclarer une constante en JS, on utilise le mot clé `const`.

Il n'est pas possible de réinitialiser la valeur d'une constante. Si on essaie :

```js
const pizza = true ;
pizza = false ;
```
Nous aurons une erreur : 


### Mot clé `let`

Depuis Juin 2015 et l’arrivée de la mise-à-jour ES6 de Javascript, on utilise donc le mot clé `let` pour définir une variable.


### *Template strings*

Les *Template strings* (ou littéraux de gabarit) sont une alternative à la concaténation "traditionnelle" de *strings* (chaînes de caractères). 

Concaténation traditionnelle : 

```js
console.log(lastName + ", " + firstName + " " + middleName);
```

Avec des *template strings* :

```js
console.log(`${lastName}, ${firstName} ${middleName}`);
```

On peut aussi créer créer une chaîne et insérer des variables ou expression JavaScript en les entourant de `${ }` : 

```js
const email = `
Hello ${firstName},
Thanks for ordering ${qty} tickets to ${event}.

Order Details
${firstName} ${middleName} ${lastName}
    ${qty} x $${price} = $${qty*price} to ${event}

You can pick your tickets up 30 minutes before
the show.

Thanks,

${ticketAgent}
```

Avec des *template strings*, il est plus facile et lisible d'insérer du HTML dans une variable :   

```js
document.body.innerHTML = `
<section>
    <header>
        <h1>The React Blog</h1>
    </header>
    <article>
        <h2>${article.title}</h2>
        ${article.body}
    </article>
    <footer>
        <p>copyright ${new Date().getYear()} | The React Blog</p>
    </footer>
</section>
`;
```

## Fonctions

Chaque fois que l'on souhaite effectuer une tâche répétitive, on utilise des fonctions. En Javascript, il existe plusieurs types de syntaxes pour déclarer une fonction.

### Fonctions nommées

Une déclaration de fonction commence par le mot-clé `function`, suivi du nom de la fonction (dans l'exemple, `logCompliment`. Le corps de la fonction et ses instructions (i.e. son bloc d'instruction) sont définis entredes accolades :

```js
function logCompliment() {
    console.log("You're doing great !") ;
}
```
Une fois la fonction déclarée, vous l'invoquez ou l'appelez pour la voir s'exécuter :

```js
function logCompliment() {
    console.log("Vous vous débrouillez très bien !") ;
}

logCompliment() ;
```
Une fois la fonction invoquée, le compliment est affiché dans la console.

### Fonctions anonymes 

Une autre option serait d'utiliser une fonction anonyme, ce qui revient à déclarer la fonction comme une variable :

```js
const logCompliment = function() {
    console.log("You're doing great!");
};

logCompliment();
```

Le resultat est le même. La seule différence, c'est qu'il n'est pas possible d'invoquer une fonction anonyme avant de la déclarer.

```js
// Invoking the function before it's declared
hey();
// Function Declaration
function hey() {
    alert("hey!");
}
```

```js
// Invoking the function before it's declared
hey();
// Function Expression
const hey = function() {
    alert("hey!");
    };

TypeError: hey is not a function
```

#### Passage d'arguments

Une fonction peut prendre un ou plusieurs arguments en entrée : 

```js
const logCompliment = function(firstName) {
    console.log(`You're doing great, ${firstName}`);
};

logCompliment("Molly");
```

```js
const logCompliment = function(firstName, message) {
    console.log(`${firstName}: ${message}`);
};

logCompliment("Molly", "You're so cool");
```

#### Retour de fonctions

La fonction `logCompliment` enregistre actuellement le compliment dans la console, mais plus souvent, nous utiliserons une fonction pour **retourner** une valeur.
Pour cela, on utilise le mot clé **return** à cette fonction.

```js
const createCompliment = function(firstName, message) {
    return `${prénom} : ${message}` ;
} ;

createCompliment("Molly", "You're so cool") ;
```
Si vous souhaitez vérifier que la fonction s'exécute comme prévu, il vous suffit d'insérer l'appel de la fonction dans un `console.log()` :

```js
console.log(createCompliment("You're so cool", "Molly")) ;
```

#### Arguments par défaut

Il est possible d'avoir des valeurs par défaut pour les arguments, dans le cas ou la valeur n'est pas fournie, la valeur par défaut est utilisée : 

```js
function logActivity(name = "Shane McConkey", activity = "skiing") {
    console.log(`${name} loves ${activity}`);
}
```
```js
const defaultPerson = {
    name: {
        first: "Shane",
        last: "McConkey"
    },
    favActivity: "skiing"
};

function logActivity(person = defaultPerson) {
    console.log(`${person.name.first} loves ${person.favActivity}`);
}
```

### Fonctions fléchées

Une façon plus "moderne" de déclarer une fonction est d'utiliser la syntaxe des fonctions fléchées. Avec les fonctions fléchées, il est possible de créer des fonctions sans utiliser le mot-clé `function`. Souvent, il n'est pas non plus nécessaire d'utiliser le mot-clé `return`.

Fonction anonyme : 
```js
const lordify = function(firstName) {
    return `${firstName} of Canterbury`;
};

console.log(lordify("Dale")); // Dale of Canterbury
console.log(lordify("Gail")); // Gail of Canterbury
```

Fonction fléchées (syntaxe plus simple et épurée) :

```js
const lordify = firstName => `${firstName} of Canterbury`;
```

Avec la flèche, nous avons maintenant une déclaration de fonction complète sur une seule ligne. Le mot-clé `function` est supprimé. Nous supprimons également `return` car la flèche pointe vers ce qui doit être retourné. Un autre avantage est que si la fonction ne prend qu'un seul argument, nous pouvons supprimer les parenthèses autour des arguments.

Plus d'un argument doit être entouré de parenthèses :

```js
// Typical function
const lordify = function(firstName, land) {
    return `${firstName} of ${land}`;
};
// Arrow Function
const lordify = (firstName, land) => `${firstName} of ${land}`;

console.log(lordify("Don", "Piscataway")); // Don of Piscataway
console.log(lordify("Todd", "Schenectady")); // Todd of Schenectady
```

cette fonction peut tenir sur une seule ligne car il n'y a qu'une seule déclaration à renvoyer. S'il y a plusieurs lignes, il faut utiliser des accolades :

```js
const lordify = (firstName, land) => {
    if (!firstName) {
        throw new Error("A firstName is required to lordify");
    }
    
    if (!land) {
        throw new Error("A lord must have a land");
    }
    
    return `${firstName} of ${land}`;
};
console.log(lordify("Kelly", "Sonoma")); // Kelly of Sonoma
console.log(lordify("Dave")); // ! JAVASCRIPT ERROR
```

## Objets et tableaux (*Arrays*)

Depuis ES2016, la syntaxe JavaScript a pris en charge des façons créatives de scoping de variables au sein d'objets et de tableaux. Ces techniques créatives sont largement utilisées par la communauté React. Jetons un coup d'œil à quelques-unes d'entre elles, notamment la déstructuration, l'amélioration du littéral objet et l'opérateur spread.

### Décomposer un objet

L'affectation de déstructuration vous permet de délimiter localement les champs d'un objet et de déclarer les valeurs qui seront utilisées. Prenons l'objet sandwich. Il possède quatre clés, mais nous ne voulons utiliser que les valeurs de deux d'entre elles. Nous pouvons délimiter le pain et la viande pour qu'ils soient utilisés localement

```js
const sandwich = {
    bread: "dutch crunch",
    meat: "tuna",
    cheese: "swiss",
    toppings: ["lettuce", "tomato", "mustard"]
};

const { bread, meat } = sandwich;

console.log(bread, meat); // dutch crunch tuna
```

Il est aussi possible de décomposer les arguments d'une fonction.


```js
const lordify = regularPerson => {
    console.log(`${regularPerson.firstname} of Canterbury`);
};

const regularPerson = {
    firstname: "Bill",
    lastname: "Wilson"
};

lordify(regularPerson); // Bill of Canterbury
```

```js
const lordify = ({ firstname }) => {
    console.log(`${firstname} of Canterbury`);
};
const regularPerson = {
    firstname: "Bill",
    lastname: "Wilson"
};

lordify(regularPerson); // Bill of Canterbury
```

Exemple plus complexe avec des objets imbriqués (objet dans un objet) :

```js
const regularPerson = {
    firstname: "Bill",
    lastname: "Wilson",
    spouse: {
        firstname: "Phil",
        lastname: "Wilson"
    }
};

const lordify = ({ spouse: { firstname } }) => {
    console.log(`${firstname} of Canterbury`);
};

lordify(regularPerson); // Phil of Canterbury
```

### Décomposer un tableau

Il est aussi possible de décomposer les valeurs d'un tableau : 

```js
const [firstAnimal] = ["Horse", "Mouse", "Cat"];

console.log(firstAnimal); // Horse
```

```js
const [, , thirdAnimal] = ["Horse", "Mouse", "Cat"];

console.log(thirdAnimal); // Cat
```

### *Object Literal Enhancement*

Il est aussi possible de faire l'opération inverse de la décomposition, soit "recomposer" un objet : 

```js
const name = "Tallac";
const elevation = 9738;

const funHike = { name, elevation };

console.log(funHike); // {name: "Tallac", elevation: 9738}
```

### Opérateur Spread

L'opérateur *spread* est constitué de trois points `...`. Il peut permettre de "fusionner" le contenu de plusieur tableaux. Par exemple, si nous avons deux tableaux, nous pouvons créer un troisième tableau qui combine les deux tableaux en un seul :

```js
const peaks = ["Tallac", "Ralston", "Rose"];
const canyons = ["Ward", "Blackwood"];
const tahoe = [...peaks, ...canyons];

console.log(tahoe.join(", ")); // Tallac, Ralston, Rose, Ward, Blackwood
```

Tous les éléments des pics et des canyons sont placés dans un nouveau tableau appelé tahoe.

Voyons comment l'opérateur *spread* peut nous aider dans certaines situations. En utilisant le tableau `peaks` de l'exemple précédent, imaginons que nous voulions récupérer le dernier élément du tableau plutôt que le premier. Nous pourrions utiliser la méthode `Array.reverse` pour inverser le tableau en combinaison avec la décomposition du tableau :

```js
const peaks = ["Tallac", "Ralston", "Rose"];
const [last] = peaks.reverse();

console.log(last); // Rose
console.log(peaks.join(", ")); // Rose, Ralston, Tallac
```

Vous voyez ce qui s'est passé ? La fonction `reverse` a en fait modifié le tableau de base.
Avec l'opérateur *spread*, il n'est pas nécessaire de modifier le tableau d'origine. Au lieu de cela, nous pouvons créer une copie du tableau et l'inverser :

```js
const peaks = ["Tallac", "Ralston", "Rose"];
const [last] = [...peaks].reverse();

console.log(last); // Rose
console.log(peaks.join(", ")); // Tallac, Ralston, Rose
```

Comme nous avons utilisé l'opérateur *spread* pour copier le tableau, le tableau `peaks` est toujours intact et peut être utilisé ultérieurement dans sa forme originale.

L'opérateur *spread* peut également être utilisé pour obtenir les éléments restants du tableau :

```js
const lakes = ["Donner", "Marlette", "Fallen Leaf", "Cascade"];

const [first, ...others] = lakes;

console.log(others.join(", ")); // Marlette, Fallen Leaf, Cascade
```

L'opérateur *spread* peut aussi être utilisé pour des objets (de la même façon que pour les tableaux) :

```js
const morning = {
    breakfast: "oatmeal",
    lunch: "peanut butter and jelly"
};

const dinner = "mac and cheese";

const backpackingMeals = {
    ...morning,
    dinner
};

console.log(backpackingMeals);

// {
//  breakfast: "oatmeal",
//  lunch: "peanut butter and jelly",
//  dinner: "mac and cheese"
// }
``` -->