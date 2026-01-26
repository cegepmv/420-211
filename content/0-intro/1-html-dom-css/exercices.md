+++
title = 'Exercices'
weight = '111'
draft = false
+++

#### Exercice 1 - Structure DOM
À partir du DOM suivant, faites le fichier HTML correspondant (nommez votre fichier *exercice-dom-1.html*) :

![DOM](/420-211/images/0-intro/011-ex1.png)

#### Exercice 2 - Manipulation par `id`
Dans le document [exercice-dom-2.html](/420-211/ressources/exercice-dom-2.html), remplacez les mots 
+ *apple* → *pomme*
+ *pear* → *poire*
+ *banana* → *banane*

En utilisant des appels à la fonction `getElementById()` (vous devez créer le fichier *exercice-dom-2.js*).

#### Exercice 3 - Manipulaiton par `class`
Dans le document [exercice-dom-3.html](/420-211/ressources/exercice-dom-3.html), utilisez `getElementsByClass()` pour:
+ appliquer la police **Arial**
+ changer la couleur du texte en **bleu**

Vous devez créer le fichier *exercice-dom-3.js*

#### Exercice 4 - Mode sombre
À partir du fichier [exercice-dom-4.html](/420-211/ressources/exercice-dom-4.html), implémentez la fonction associée au bouton pour basculer en **mode sombre** en modifiant les styles des éléments HTML. 

Vous pouvez utiliser le site suivant pour les références aux couleurs : https://htmlcolorcodes.com/. 

Le résultat devrait ressembler à ceci (les titres sont en vert pâle et le texte en gris) :

![DOM](/420-211/images/0-intro/012-ex4.jpg)

#### Exercice 5 - Mise en forme CSS
En utilisant un fichier CSS, définissez des classes de style pour obtenir la page suivante à partir du fichier [exercice-css.html](/420-211/ressources/exercice-css.html) : 

![Exercice 5](/420-211/images/0-intro/013-ex5.png)

#### Exercice 6 – Refactorisation sémantique HTML

Le fichier [exercice-semantique.html](/420-211/ressources/exercice-semantique.html) contient un code fonctionnel, mais qui **n’utilise pas les balises HTML sémantiques appropriées**. On vous demande de:

+ Remplacer les `<div>` par des balises sémantiques appropriées
+ Conserve la même structure visuelle
+ Ne pas modifier le contenu textuel
+ Le fichier final doit être plus lisible et mieux structuré


{{%notice style="tip" title="Astuces"%}}
+ Le menu devrait être contenu dans une balise <nav>
+ Le contenu principal devrait être contenu dans <main>
+ Chaque publication devrait être un <article>
{{% /notice %}}


