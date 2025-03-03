+++
pre = '<b>5. </b>'
title = "Exercice dirigé"
weight = '340'
draft = false 
+++

# Réutilisabilité des composants
L'objectif de cet exercice est de **refactoriser** la page web précédemment développée afin d'**améliorer la réutilisabilité** des composants. Vous devrez optimiser votre implémentation en appliquant les bonnes pratiques de développement avec React, notamment en structurant le code de manière **modulaire** et en favorisant la transmission efficace des données entre les composants.

**🎯 Objectifs :**
- Identifier et extraire les éléments communs dans des **composants réutilisables**.
- Utiliser **les props** pour transmettre les données nécessaires aux composants.
- Simplifier et structurer votre code en évitant les répétitions.

**Points clés à améliorer :**
1. **Refactoriser le composant `ListItem`**
Plutôt que d'avoir plusieurs éléments statiques pour les différentes raisons d’aimer l’informatique, vous devez transformer ListItem en un composant réutilisable prenant **image, titre et description** en props.

2. **Organiser les données de manière dynamique**
Créez un tableau d’objets contenant les différentes raisons, puis affichez les éléments dynamiquement en **mappant** ce tableau pour générer les composants `ListItem`.

3. **Simplifier l’architecture des fichiers**
Si ce n'est pas encore fait, organisez les composants dans des fichiers séparés (`Header.js`, `ListItem.js`, `Footer.js`, etc.) pour améliorer la clarté et la maintenabilité de votre code.

En appliquant ces principes, vous écrirez un code **plus modulaire, maintenable et évolutif**. Cela vous permettra d’ajouter de nouvelles raisons sans modifier directement le JSX, rendant votre application plus flexible.

**🚀 À vous de jouer !** Reprenez votre implémentation précédente et appliquez ces améliorations.
