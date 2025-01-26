+++
pre = '<b>7.1 </b>'
title = 'Guide Git Bash'
weight = '01'
draft = true
+++


---
### Git Bash : Guide pratique
Git Bash est un terminal puissant qui permet d'utiliser Git via des commandes en ligne. Contrairement à GitHub Desktop, il offre un contrôle précis et détaillé des opérations Git, idéal pour les utilisateurs qui souhaitent maîtriser les bases et les fonctionnalités avancées de Git. Avec Git Bash, vous pouvez gérer vos dépôts, créer des branches, et effectuer des opérations complexes directement depuis la ligne de commande. 
Voici un guide étape par étape pour tirer le meilleur parti de Git Bash.

##### 1. Configuration de votre nom d’utilisateur et de votre email

Avant d'utiliser Git, configurez votre identité pour associer vos modifications à votre profil.

**Commande :**
```bash
git config --global user.name "Votre Nom"
git config --global user.email votre.email@example.com
```

##### 2. Cloner un dépôt existant

Pour travailler sur un projet déjà hébergé sur GitHub :

1. Copiez l'URL du dépôt GitHub.
2. Exécutez la commande suivante dans Git Bash pour cloner le dépôt sur votre machine :

```bash
git clone <lien_du_dépôt>
```

**Exemple :**
```bash
git clone https://github.com/votre-utilisateur/votre-projet.git
```

##### 3. Initialiser un dépôt (pour un nouveau projet)

Si vous commencez un nouveau projet, vous devez initialiser un dépôt Git dans le dossier correspondant.

**Commande :**
```bash
git init
```

##### 4. Ajouter des fichiers au dépôt

Une fois que vous avez des fichiers à suivre, ajoutez-les à la gestion de versions avec Git.

**Commande pour ajouter un fichier spécifique :**
```bash
git add <nom_du_fichier>
```

**Commande pour ajouter tous les fichiers :**
```bash
git add *
```

##### 5. Créer un commit

Un commit permet d'enregistrer vos modifications dans l'historique de Git avec un message descriptif.

**Commande :**
```bash
git commit -m "Description de vos modifications"
```

##### 6. Envoyer vos modifications sur GitHub

Si le dépôt est déjà connecté à GitHub, envoyez vos modifications :

**Commande :**
```bash
git push origin <nom_de_la_branche>
```

**Exemple :**
```bash
git push origin main
```

##### 7. Créer une nouvelle branche

Pour travailler sur une fonctionnalité ou corriger un bug, créez une nouvelle branche.

**Commande :**
```bash
git branch <nom_de_la_branche>
```

**Exemple :**
```bash
git branch feature-nouvelle-fonctionnalité
```

##### 8. Changer de branche

Pour passer d'une branche à une autre.

**Commande :**
```bash
git checkout <nom_de_la_branche>
```

**Exemple :**
```bash
git checkout feature-nouvelle-fonctionnalité
```

---

Pour plus de détails sur les commandes Git, vous pouvez consulter le Cheat Sheet officiel : [https://training.github.com/downloads/fr/github-git-cheat-sheet.pdf](https://training.github.com/downloads/fr/github-git-cheat-sheet.pdf)