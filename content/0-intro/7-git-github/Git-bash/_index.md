+++
pre = '<b>7.1 </b>'
title = 'Guide Git Bash'
weight = '173'
draft = false
+++

---
### Qu'est-ce que Git Bash et pourquoi est-il important ?
Git Bash est un terminal qui permet d’utiliser Git en ligne de commandes. Il offre un environnement Unix sur votre ordinateur, simplifiant l’exécution des commandes, particulièrement pour les utilisateurs de Windows.

Utiliser Git Bash est essentiel pour gérer efficacement vos projets grâce à un contrôle précis et rapide. Il permet d’approfondir votre compréhension des bases de Git et d’automatiser certaines tâches. De plus, maîtriser la ligne de commande est un atout majeur dans le développement logiciel professionnel. 

Avec Git Bash, vous pouvez gérer vos dépôts, créer des branches, et effectuer des opérations complexes directement depuis la ligne de commande. Voici un guide étape par étape pour tirer le meilleur parti de Git Bash.

##### Installation
1. Rendez-vous sur le site officiel de Git : [https://git-scm.com/](https://git-scm.com/)
2. Téléchargez et installez Git en suivant les instructions adaptées à votre système d’exploitation.
3. Pendant l’installation, laissez les options par défaut, sauf indication contraire.

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

##### Initialiser un dépôt (pour un nouveau projet)

Si vous commencez un nouveau projet, vous devez initialiser un dépôt Git dans le dossier correspondant.

**Commande :**
```bash
git init
```

##### 3. Ajouter des fichiers au dépôt

Une fois que vous avez des fichiers à suivre, ajoutez-les à la gestion de versions avec Git.

**Commande pour ajouter un fichier spécifique :**
```bash
git add <nom_du_fichier>
```

**Commande pour ajouter tous les fichiers :**
```bash
git add .
```

##### 4. Vérifier l'état des fichiers avec `git status`

Avant de créer un commit, il est utile de vérifier quels fichiers ont été modifiés, ajoutés ou supprimés. La commande `git status` affiche l'état actuel du répertoire de travail et de la zone de staging (préparation).

**Commande :**
```bash
git status
```
Ce que vous allez voir :  

Les fichiers **modifiés** mais non ajoutés à la zone de staging.  
Les fichiers **ajoutés** et prêts à être commités.  
Les fichiers **non suivis** (nouveaux fichiers que Git ne suit pas encore).  

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

##### 9. Fusionner des branches 
Lorsque vous avez terminé le travail sur une branche, vous pouvez la fusionner dans la branche principale (généralement main).

Étapes pour fusionner des branches :

Basculez sur la branche principale (main) :
```bash
git checkout main
```

Assurez-vous que main est à jour :
```bash
git pull origin main
```

Fusionnez la branche de travail (par exemple feature-nouvelle-fonctionnalité) dans main :
```bash
git merge feature-nouvelle-fonctionnalité
```

Résoudre les conflits s'il y en a :
- Ouvrez les fichiers en conflit.
- Recherchez les délimiteurs de conflit <<<<<<<, =======, >>>>>>>.
- Modifiez le fichier pour résoudre les conflits, puis sauvegardez.

Ajoutez les fichiers résolus :

```bash
git add <fichier_conflit>
```

Finalisez la fusion avec un commit :

git commit -m "Fusion de feature-nouvelle-fonctionnalité dans main"

Poussez les modifications fusionnées vers GitHub :
```bash
git push origin main
```

---

Pour plus de détails sur les commandes Git, vous pouvez consulter le Cheat Sheet officiel : [https://training.github.com/downloads/fr/github-git-cheat-sheet.pdf](https://training.github.com/downloads/fr/github-git-cheat-sheet.pdf)