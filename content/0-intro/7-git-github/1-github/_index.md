+++
pre = '<b>1. </b>'
title = 'Intro à Github'
weight = '171'
draft = false
+++
-------------
<!-- ### Contrôle de version
Le contrôle de version (*Version Control*), également appelé contrôle de source (*Source Control*), permet de suivre et de gérer toutes les modifications apportées à un code.

#### Utilité
+ Plusieurs personnes peuvent travailler simultanément sur le même projet.
+ Il sert à la fois de référentiel, de récit de projet, de moyen de communication et d'outil de gestion d'équipe.
+ Enregistre toutes les modifications d'un code source dans un journal (ou historique).
+ Permet aux membres d'une équipe de travailler simultanément et offre la possibilité de fusionner leur travaux.

#### Système de contrôle de version (VCS)

Également connu sous le nom de gestionnaire de code source (*Source Code Manager* ou *SCM*). Il s'agit d'un système qui conserve la trace des modifications apportées à un fichier ou à un ensemble de fichiers et qui, en cas de problème, vous permet de remonter dans l'histoirique des modification, de comparer les modifications au fil du temps et de revenir facilement à un état fonctionnel de votre code source. Le très populaire **Git** est un système de contrôle de version très appréciés des développeurs. Il est gratuit et libre (*open-source*).

### Introduction à GitHub -->

Avant de nous plonger dans les différentes commandes `git`, familiarisons-nous rapidement avec **GitHub**.

+ **Git** est l'outil qui permet suivre les modifications apportées à un code (c'est comme un historique/journal des changements). 

+ **GitHub** est un site web sur lequel vous pouvez **téléverser (*push*) vos projets locaux sur internet** pour que vos coéquipiers (ou d'autres personnes qui travaillent sur le même projet) puissent aussi avoir accès au code et le modifier. 

{{% notice style=info title=Analogie %}}
GitHub est comme un "hub" où vous pouvez entreposer et partager vos projets/codes sur internet.
{{% /notice %}}

## Inscription à GitHub
Allez sur le site de GitHub et inscrivez-vous (utilisez l'adresse courriel du Cégep !).

## Profil GitHub
Une fois inscrit, vous pouvez vous rendre sur le site : 

https://github.com/VOTRE_USERNAME. 

Vous pourrez voir votre profil public où vous pourrez ajouter quelques informations vous concernant (photo de profil, description, etc...). Voici un exemple de profil sur lequel vous pouvez vous inspirer : [Profil GitHub](https://github.com/bobbyiliev).

## Créer un nouveau dépôt
Si vous n'êtes pas familier avec le terme "dépôt", vous pouvez le considérer comme **un projet** : Il contient tous les fichiers de l'application ou du site web que vous êtes en train de développer. 

On appelle généralement un dépot une "repo" (pour *repository* en anglais).

Pour créer un nouveau dépôt sur GitHub, cliquez sur le bouton vert `NEW` en haut à gauche où les dépôts sont listés puis cliquer sur le bouton `New Repository` :

(SCREEN)

Après cela, vous arriverez à une page où vous pourrez spécifier les informations pour votre nouveau dépôt, comme par exemple :
+ Le nom du projet (utilisez quelque chose de descriptif)
+ Une description générale du projet et de son objet.
+ Choisissez si vous voulez que le dépôt soit public ou privé.

Une fois que vous avez ajouté les informations et crée votre "repo", vous arriverez sur une page avec des instructions sur la façon de pousser votre projet local sur GitHub (nous verrons ces étapes plus en détail dans les prochains sections).

### Dépôt publique vs dépôt privé
En fonction de la nature du projet (qu'il soit ou non *open-source* par exemple), vous pouvez définir votre dépôt comme **public** ou **privé** :

+ **Dépôt public :** n'importe qui sur internet peut le voir. Attention! Même s'il est possible de voir le dépôt et de lire le code, vous serez le mainteneur du projet : C'est vous qui choisirez les personnes autorisées à modifier le code.
+ **Dépôt privé :** n'est accessible qu'à vous et aux personnes que vous invitez. Attention, il vous faudra être membre du projet pour push et il faut aussi s'authentifier soit par SSH, soit par HTTPS. 

### Authentification avec un jeton (*PAT*)

Depuis 2021, GitHub n'accepte plus votre mot de passe habituel pour les opérations Git en ligne de commande. Pour vous identifier, vous devez créer et utiliser un **Personal Access Token (PAT)**.

#### 1. Générer votre jeton (PAT) sur GitHub
1. Cliquez sur votre photo de profil (en haut à droite), puis sur **Settings**.
2. Dans le menu de gauche, tout en bas, cliquez sur **<> Developer settings**.
3. Sélectionnez **Personal access tokens** > **Tokens (classic)**.
4. Cliquez sur le bouton **Generate new token** (choisissez *Generate new token (classic)*).
5. Remplissez les informations suivantes :
    * **Note :** Donnez-lui un nom clair (ex: "Session Automne - Portable").
    * **Expiration :** Par défaut 30 jours (vous pouvez choisir une durée plus longue pour la session).
    * **Select scopes :** Cochez impérativement la case **`repo`** (cela permet de gérer vos projets privés et publics).
6. Cliquez sur **Generate token** en bas de page.

{{%notice style="warning" title="Attention"%}}
**Copiez votre jeton immédiatement !** Vous ne pourrez plus le revoir après avoir quitté la page. Conservez-le dans un endroit sûr.
{{%/notice%}}




#### 2. Utiliser le jeton dans le terminal
Lorsque vous ferez votre premier `git push`, le terminal vous demandera vos identifiants :

* **Username :** Votre nom d'utilisateur GitHub.
* **Password :** **Collez ici votre jeton (PAT)** au lieu de votre mot de passe de compte. 

*Note : Sous Linux ou macOS, il est normal que le curseur ne bouge pas et qu'aucun caractère ne s'affiche pendant que vous collez le jeton.*

#### 3. Mémoriser les identifiants
Pour éviter de copier-coller ce jeton à chaque interaction, utilisez la commande suivante pour que Git enregistre vos accès de façon permanente sur votre poste :

```bash
git config --global credential.helper store
```

### Le fichier README.md

+ Le fichier `README.md` est une présentation/description de votre projet. 
+ **Avantage :** Lorsque vous regardez le dépôt de quelqu'un sur GitHub, lire son fichier `README` vous permettra de comprendre ce que fait son code, quelles sont les dépendances à installer pour faire fonctionner son logiciel, etc...

{{%notice style="note" title="Important"%}}
**Il est très important qu'projet/dépôt soit correctement décrit et documenté**. Si ce n'est pas le cas, personne ne voudra l'utiliser, l'améliorer ou le développer.
{{%/notice%}}


