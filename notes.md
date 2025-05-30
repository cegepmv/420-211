## Expliquer statique vs dynamique

## Montrer le projet qu'on va faire

## Faire le header

Header.css : 
```css
* {
    box-sizing: border-box;
}

body {
    margin: 0;
    font-family: Inter, sans-serif;
    background-color: #FAFAF8;
}

header {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 11px;
    height: 80px;
    background-color: white;
    box-shadow: 0px 1px 3px 0px rgba(0, 0, 0, 0.10), 0px 1px 2px 0px rgba(0, 0, 0, 0.06);
}

header > img {
    width: 50px;
}

header > h1 {
    font-weight: 400;
}
```

```jsx
import chefClaudeLogo from "./images/chef-claude-icon.png"

export default function Header() {
    return (
        <header>
            <img src={chefClaudeLogo}/>
            <h1>Chef Claude</h1>
        </header>
    )
}
```

## Faire le form 

Main.css :
```css
.add-ingredient-form {
    display: flex;
    justify-content: center;
    gap: 12px;
    height: 38px;
}

.add-ingredient-form > input {
    border-radius: 6px;
    border: 1px solid #D1D5DB;
    padding: 9px 13px;
    box-shadow: 0px 1px 2px 0px rgba(0, 0, 0, 0.05);
    flex-grow: 1;
    min-width: 150px;
    max-width: 400px;
}

.add-ingredient-form > button {
    font-family: Inter, sans-serif;
    border-radius: 6px;
    border: none;
    background-color: #141413;
    color: #FAFAF8;
    width: 150px;
    font-size: 0.875rem;
    font-weight: 500;
}

.add-ingredient-form > button::before {
    content: "+";
    margin-right: 5px;
}
```
Main.jsx : 
```jsx
export default function Main() {
    return (
        <main>
            <form className="add-ingredient-form">
                <input 
                    type="text"
                    placeholder="e.g. oregano"
                    aria-label="Add ingredient"
                />
                <button>Add ingredient</button>
            </form>
        </main>
    )
}
```


