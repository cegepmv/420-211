+++
pre = '<b>3. </b>'
title = "Gestion des actifs statiques"
weight = '330'
draft = false 
+++

Dans une application React, les images et autres fichiers statiques sont généralement placés dans le dossier public ou src/assets.

**Exemple d'image importée depuis `public`**
```jsx
function Logo() {
  return <img src="/logo.png" alt="Logo" />;
}
```
**Exemple d'image importée depuis `src/assets`**
```jsx
import logo from "./assets/logo.png";

function Logo() {
  return <img src={logo} alt="Logo" />;
}
```
L'importation permet d'assurer que l'image est bien prise en compte lors de la compilation.