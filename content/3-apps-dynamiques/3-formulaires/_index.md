+++
pre = '<b>3. </b>'
title = "Formulaires"
weight = '430'
draft = false 
+++

Un des outils permettant à une application dynamique de récupérer des données entrées par un utilisateur sont les formulaires. Ces données sont le plus souvent envoyées à un serveur (API) pour y être traitées.

Exemple de cas d'utilisation de formulaires : 
+ Inscription à une application
+ Connexion à un site



### Les bases

{{< tabs >}}
{{% tab title="App.jsx" color="blue" %}}
```jsx
function App() {

    return (
        <section className="container">
            
            <h2>Inscription</h2>
            <form className="form">
                <label htmlFor="email">Email :</label>
                <input 
                    type="email" 
                    id="email" 
                    name="email" 
                    placeholder="john-doe@exemple.com"
                />

                <label htmlFor="password">Mot de passe :</label>
                <input 
                    type="password" 
                    id="password" 
                    name="password"
                />
                
                <button className="submit-btn">Inscription</button>
            </form>
        </section>
    )
}

export default App
```
{{< /tab >}}
{{% tab title="index.css" color="blue" %}}
```css
* {
  margin: 0;
  padding: 0;
}

body{ 
  background-color: #2CA1CC;
  font-family: 'Roboto', sans-serif;
}

.container{
  width: 400px;
  margin: auto;
  margin-top: 50px;
  padding-bottom: 30px;
  background-color: #fff;
  border-radius:5px;
  color: #1F1F1F;
}

.container h2 {
  padding: 20px; 
  text-align: center;
}

.form {
  display: flex;
  flex-direction: column;
  margin: 10px 40px 0;
}

.form input {
  margin: 10px 0 20px;
  padding: 10px;
  width:90%;
  background-color: #EAEDF2;
  border: none;
  border-radius:3px;
  color:#A0A0A0;
}

.form textarea {
  resize: none;
  margin: 10px 0 20px;
  padding: 10px;
  width:90%;
  height: 15vh;
  background-color: #EAEDF2;
  border: none;
  border-radius:3px;
  color:#A0A0A0;
}

.form fieldset {
  display: flex;
  flex-direction: column;
  border: none;
  margin: 10px 0;
}

.form fieldset legend {
  margin-bottom: 5px;
}

.form fieldset input {
  width:fit-content;
  margin: 10px 10px 7px 2px;
}
.form fieldset label {
  width:fit-content;
}


.form .submit-btn {
  border:none;
  padding: 10px;
  border-radius:5px;
  color:#F7F6FF;
  cursor: pointer;
  width: 96%;
  margin-bottom:10px;
  margin-top: 20px;
  background-color: #19B8D6;
  height: 37px;
}
```
{{< /tab >}}
{{< /tabs >}}

+ Toutes les entrées d'un formulaire doivent être à l'intérieur d'une balise `<form>`


+ Pour une entrée texte, on utilise l'élément HTML `<input>`. Cet élément possède plusieurs propriétés :
    + `type` : le type d'entrée. Peut être `email`, `password`, `checkbox`, etc...
    + `name` : Le nom de l'élément. C'est ce qui va nous permettre de récupérer sa valeur par la suite.
    + `placeholder`: un exemple qui va être affiché pour guider l'utilisateur sur la forme attendue de l'entrée.

+ Un élément `<label>` doit être fourni pour donner un label à une entrée. Cet élément possède une propriété `htmlFor` dont la valeur est égale à la propriété `id` de l'entrée qu'elle décrit. Dans un code HTML, on remplacerait le `htmlFor=` par `for=`. 

### Balise form

Toutes les entrées d'un formulaire doivent être à l'intérieur d'une balise `<form>`. Cette balise possède les propriétés suivantes : 
+ `action=` : La fonction (ou le fichier) déclenchée lorsqu'on soumet le formulaire.
+ `method=` : Le type d'appel API effectué lors de la soumission du formulaire. Peut être de type `POST`, `GET`, `PUT` ou `DELETE`. Par défaut, sa valeur est `GET`.

Lorsque vous soumettez un formulaire, la page est redirigée vers un URL qui contient les données entrées dans le formulaire. Si nous changeons la propriété `method=` à `"POST"`, le formulaire crée une requête `POST` et met les entrées du formulaire dans le corps (*body*) de la requête.

Pour faire en sorte d'éviter la redirection (ne pas afficher les données du formulaire dans l'URL) et traiter les données du formulaire dans notre propre code JavaScript, nous pouvons utiliser la propriété `onSubmit` et lui donner une fonction qui va gérer la soumission. Nous pouvons empêcher le rafraîchissement de la page en utilisant `event.preventDefault()` comme suit :

```jsx
function App() {

  function handleSubmit(event) {
    event.preventDefault()
  }

  return (
    <section className="container">
      <h2>Inscription</h2>
      
      <form className="form" onSubmit={handleSubmit} >

          <label htmlFor="password">Mot de passe :</label>
          <input type="password" id="password" name="password"/>
        
          <label htmlFor="email">Email :</label>
          <input type="email" id="email" name="email" placeholder = "john-doe@exemple.com"/>
        
          <button className="submit-btn">Inscription</button>
      </form>
    </section>
  )
}
```

L'argument `event` passé à la fonction `handleSubmit()` possède beaucoup d'informations utiles pour traiter le formulaire : 

```jsx
function handleSubmit(event) {
    event.preventDefault()
    const formEl = event.currentTarget
    const formData = new FormData(formEl)
    const email = formData.get("email")
    formEl.reset()
}
```
+ Pour récupérer l'élément `<form>`, on utilise `event.target` ou `event.currentTarget` (conseillé). 
+ À partir de `event.currentTarget`, nous pouvons créer un objet JavaScript `FormData`. En lui passant `event.currentTarget` en argument, nous pouvons récupérer chaque donnée du formulaire en utilisant ensuite la méthode `formData.get("nom_de_l'entrée")`.
+ Pour réinitialiser le formulaire après avoir traîté les données, on utilise la méthode `.reset()`



#### Propriété action
À partir de la version 19, React a introduit une meilleure façon (plus déclarative) de gérer les formulaires, en utilisant la propriété `action={fonction}` de l'élément `<form>`. 

```jsx
function App() {

    function signUp(formData) {
        const email = formData.get("email")
        console.log(email)
    }
    
    return (
        <section className="container">
            
            <h2>Inscription</h2>
        
            <form action={signUp} className="form">
                
                <label htmlFor="email">Email :</label>
                
                <input 
                    type="email" 
                    id="email" 
                    name="email" 
                    placeholder="john-doe@exemple.com"
                />

                <label htmlFor="password">Mot de passe :</label>
                
                <input 
                    type="password" 
                    id="password" 
                    name="password"
                />
                
                <button className="submit-btn">Inscription</button>
            </form>
        </section>
    )
}
```

Cette façon de faire simplifie grandement la gestion du formulaire : 
+ Nous n'avons plus besoin d'utiliser `event.preventDefault()` et `form.reset()` (c'est fait automatiquement).
+ La fonction appelée prend maintenant en argument un objet de type `FormData` : Plus besoin d'en créer un manuellement à partir de `event.currentTarget` ! 
+ Cette façon, plus déclarative, simplifie beaucoup le code (il ne tient plus que sur une ligne !)

#### Exercice 
Dans la méthode `signUp()` de l'exemple précédent, récupérez le mot de passe puis affichez-le dans la console.

### Types d'entrées d'un formulaire

#### Bouton

Lorsqu'un bouton est à l'intérieur d'une balise `<form>`, celui-ci déclenche par défaut la fonction donnée à la propriété `action=` ou `onSubmit=` lorsqu'on clique dessus.


#### textarea

```html
<label htmlFor="description">Description:</label>
<textarea id="description" name="description"></textarea>
```


#### Boutons radio 
Les boutons radio permettent de sélectionner un choix unique parmis plusieurs choix de réponse :

```js
function signUp(formData) {
    const employmentStatus = formData.get("employmentStatus")
}
```

```jsx
<fieldset>
    
    <legend>Situation professionnelle :</legend>
    
    <label>
        <input 
            type="radio" 
            name="employmentStatus" 
            value="unemployed" 
        />
        Sans emploi
    </label>
    
    <label>
        <input 
            type="radio" 
            name="employmentStatus" 
            value="part-time" 
        />
        Temps partiel
    </label>
    
    <label>
        <input 
            type="radio" 
            name="employmentStatus" 
            defaultChecked={true} 
            value="full-time" 
        />
        Temps plein
    </label>

</fieldset>
```

+ Pour avoir une valeur spécifique pour chaque bouton radio, nous devons leur donner à chacun une propriété `value="une-valeur"`
+ Si nous souhaitons avoir un bouton radio sélectionné par défaut, il faut lui rajouter la propriété `defaultChecked={true}`

#### Checkbox

Les *checkbox* fonctionnent comme les boutons radio, sauf que l'on peut en sélectionner plusieurs : 

```jsx
<fieldset>
    <legend>Restrictions alimentaires :</legend>
    
    <label>
        <input 
            type="checkbox"
            name="dietaryRestrictions" 
            value="kosher" 
        />
        Cachère
    </label>
        
    <label>
        <input 
            type="checkbox"
            name="dietaryRestrictions" 
            value="vegan"
        />
        Vegan
    </label>

    <label>
        <input 
            type="checkbox" 
            name="dietaryRestrictions" 
            defaultChecked={true} 
            value="gluten-free" 
        />
        Sans gluten
    </label>

</fieldset>

```

+ Les *checkbox* fonctionnent comme les boutons radio, et possèdent les mêmes propriétés (`name`, `value`, `defaultChecked` etc...)
+ Pour recevoir toutes les valeurs sélectionnées, il faut utiliser la méthode `formData.getAll()` au lieu de `formData.get()`. Cette méthode retourne un tableau ayant toutes les options sélectionnées : 

```js
function signUp(formData) {
    const dietaryRestrictions = formData.getAll("dietaryRestrictions")
}
```

#### select et option

Les éléments `<select>` et `<option>` nous permettent de créer une liste déroulante : 

```js
function signUp(formData) {
    const favColor = formData.get("favColor")
}
```

```jsx

<label htmlFor="favColor">Quelle est ta couleur préférée?</label>
<select id="favColor" name="favColor" defaultValue="" required>
    <option value="" disabled>-- Choisis une couleur --</option>
    <option value="red">Rouge</option>
    <option value="orange">Orange</option>
    <option value="yellow">Jaune</option>
    <option value="green">Vert</option>
    <option value="blue">Bleu</option>
    <option value="indigo">Indigo</option>
    <option value="violet">Violet</option>
</select>
```
+ Il est possible de donner une valeur par défaut avec la propriété `defaultValue=` en lui donnant la valeur de la propriété `value=` d'une des options.
+ Il est possible d'interdire la selection d'une des options en lui ajoutant la propriété `disabled`.
+ Il est aussi possible de rendre le champ `<select>` (ainsi que tout autre champ) obligatoire pour soumettre le formulaire en ajoutant la propriété `required`.

### Utiliser Object.fromEntries

Pour obtenir toutes les entrées d'un formulaire en une ligne de code, nous pouvons utiliser l'utilitaire JavaScript `Object.fromEntries()`. En lui passant l'objet `formData` en argument, nous pouvons créer un objet contenant les noms et les valeurs de toutes les entrées du formulaire : 

```jsx
function signUp(formData) {
    const data = Object.fromEntries(formData)
}
```

Exemple de valeur que peux avoir `data` : 
```js
{
    email: "dd@exemple.com"
    password: "pass-123"
    description: "Une petite description de moi.",
    employmentStatus: "unemployed",
    dietaryRestrictions: "gluten-free",
}
```

**Problème :** Dans le cas où nous avons une section *checkbox* dans notre formulaire, il ne sera pas possible de récupérer toutes les options sélectionnées. Un moyen (parmis d'autres) pour récupérer toutes les options : 

```jsx
function signUp(formData) {
    const data = Object.fromEntries(formData)
    const dietaryRestrictions = formData.getAll("dietaryRestrictions")
    const allData = {
        ...data,
        dietaryRestrictions
    }
}
```

### Exemple Complet 

```jsx

function App() {

    function signUp(formData) { 
        const data = Object.fromEntries(formData)
        const dietaryRestrictions = formData.getAll("dietaryRestrictions")
        const allData = {
            ...data,
            dietaryRestrictions
        }
    }

    return (
        <section className="container">
            <h2>Inscription</h2>
            
            <form action={signUp} className="form">
                
                <label htmlFor="email">Email :</label>
                <input 
                    type="email" 
                    id="email" 
                    name="email" 
                    placeholder="john-doe@exemple.com"
                />

                <label htmlFor="password">Mot de passe :</label>
                <input 
                    type="password" 
                    id="password" 
                    name="password"
                />
                
                
                <label htmlFor="description">Description :</label>
                <textarea id="description" name="description"></textarea>
                
                <fieldset>
                
                    <legend>Statut professionnel :</legend>
                    
                    <label>
                        <input 
                            type="radio" 
                            name="employmentStatus" 
                            value="unemployed" 
                        />
                        Sans emploi
                    </label>
                    
                    <label>
                        <input 
                            type="radio" 
                            name="employmentStatus" 
                            value="part-time" 
                        />
                        Temps partiel
                    </label>
                    
                    <label>
                        <input 
                            type="radio" 
                            name="employmentStatus" 
                            defaultChecked={true} 
                            value="full-time" 
                        />
                        Temps plein
                    </label>
                
                </fieldset>

                <fieldset>
                    
                    <legend>Restrictions alimentaires :</legend>
                    
                    <label>
                        <input 
                            type="checkbox" 
                            name="dietaryRestrictions" 
                            value="kosher" 
                        />
                        Cachère
                    </label>
                    
                    <label>
                        <input 
                            type="checkbox" 
                            name="dietaryRestrictions" 
                            value="vegan" 
                        />
                        Vegan
                    </label>
                    
                    <label>
                        <input 
                            type="checkbox" 
                            name="dietaryRestrictions" 
                            defaultChecked={true} 
                            value="gluten-free" 
                        />
                        Sans Gluten
                    </label>
                
                </fieldset>

                <button className="submit-btn">Inscription</button>
            </form>
        </section>
    )
}

export default App
```