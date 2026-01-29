+++
pre = '<b>5. </b>'
title = "Règles et bonnes pratiques"
weight = '250'
draft = false
+++
--------

## Composants
Un composant React doit obligatoirement: 
+ être une fonction JS ;
+ commencer par une majuscule (*PascalCase*) ;
+ retourner **un seul élément parent**. Si plusieurs éléments sont nécessaires, on utilise un élément qui les englobe (`<div>`, `<main>` ou autre) ou un **Fragment** :
```jsx
<>
    <Header />
    <MainContent />
    <Footer />
</>

ou 

<Fragment>
    <Header />
    <MainContent />
    <Footer />
</Fragment>
```

Un composant peut contenir d’autres composants (c'est même encouragé). Chaque composant doit avoir une responsabilité claire :
```jsx
function Page() {
    return (
        <>
            <Header />
            <MainContent />
            <Footer />
        </>
    )
}
```

## Styles et className
En JSX :
+ `class` ❌
+ `className` ✅
```jsx
<ul className="nav-list">
```
Les styles sont ensuite définis dans un fichier CSS et importés au début du code.

## Organisation du projet React

À mesure que l’application grandit, les composants doivent être séparés dans des fichiers dédiés.

Exemple :
```md
src/
├─ components/
│  ├─ Header.jsx
│  ├─ Header.css
│  ├─ MainContent.jsx
│  ├─ MainContent.css
│  └─ Footer.jsx
│  └─ Footer.css
└─ App.jsx
```

Chaque composant est **exporté** puis **importé là où il est utilisé**.