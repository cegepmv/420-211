+++
pre = '<b>7. </b>'
title = 'Git/GitHub'
weight = '17'
draft = true
+++

### Contrôle de version
Le contrôle de version (*Version Control*), également appelé contrôle de source (*Source Control*), permet de suivre et de gérer toutes les modifications apportées à un code.

#### Utilité
+ Plusieurs personnes peuvent travailler simultanément sur le même projet.
+ Il sert à la fois de référentiel, de récit de projet, de moyen de communication et d'outil de gestion d'équipe.
+ Enregistre toutes les modifications d'un code source dans un journal (ou historique).
+ Permet aux membres d'une équipe de travailler simultanément et offre la possibilité de fusionner leur travaux.
+ Trace chaque modification apportée au logiciel/code source.

#### Système de contrôle de version (VCS)

Également connu sous le nom de gestionnaire de code source (*Source Code Manager* ou *SCM*). Il s'agit d'un système qui conserve la trace des modifications apportées à un fichier ou à un ensemble de fichiers et qui, en cas de problème, vous permet de remonter dans l'histoirique des modification, de comparer les modifications au fil du temps et de revenir facilement à un état fonctionnel de votre code source. Le très populaire **Git** est un système de contrôle de version très appréciés des développeurs. Il est gratuit et libre (*open-source*).

### Configuration de `git`

La première fois que vous installez `git` sur votre machine, vous devez faire la configuration initiale.

Quelques éléments principaux que vous devez configurer :
+ Vos coordonnées : comme votre nom et votre adresse courriel 
+ Votre éditeur Git par défaut (nano, vim ou emacs)
+ Le nom de la branche par défaut (nous verrons les branches un peu plus tard).

Nous pouvons changer toutes ces choses en utilisant la commande `git config` :

+ Configurer le nom : 
```bash
git config --global user.name "Votre Nom"
```
+ Configurer l'adresse courriel : 
```bash
git config --global user.email "votre-adresse@exemple.com"
```
+ Configurer l'éditeur git par défaut :
```bash
git config --global core.editor nano
```
+ Configurer la branche principal par défaut : 
```bash
git config --global init.defaultBranch main
```
+ Vérifier la configuration `git` :
```bash
git config --list
```

{{% notice style="info" title="Conseil"%}}
Il est préférable d'avoir le même nom d'utilisateur et adresse courriel que celle de votre profil GitHub (plus de détails dans les prochaines sections).
{{% /notice %}}

+ Configurer l'éditeur par défaut : 
```bash
git config --global core.editor nano
```

### Introduction à GitHub
Avant de nous plonger dans les différentes commandes `git`, familiarisons-nous rapidement avec **GitHub**.

**Git** est l'outil qui permet suivre les modifications apportées à un code (c'est comme un historique/journal des changements). 

**GitHub** est un site web sur lequel vous pouvez **téléverser (*push*) vos projets locaux sur internet** pour que vos coéquipiers (ou d'autres personnes qui travaillent sur le même projet) puissent aussi avoir accès au code et le modifier. 

**GitHub est comme un "hub" où vous pouvez entreposer vos projets/codes sur internet**.

#### Inscription à GitHub
Allez sur le site de GitHub et inscrivez-vous (utilisez l'adresse courriel du Cégep !).

#### Profil GitHub
Une fois inscrit, vous pouvez vous rendre sur le site https://github.com/VOTRE_USERNAME. Vous pourrez voir votre profil public où vous pourrez ajouter quelques informations vous concernant (photo de profil, description, etc...). Voici un exemple de profil sur lequel vous pouvez vous inspirer : [Profil GitHub](https://github.com/bobbyiliev).

#### Créer un nouveau dépôt
Si vous n'êtes pas familier avec le terme "dépôt", vous pouvez le considérer comme **un projet** : Il contient tous les fichiers de l'application ou du site web que vous êtes en train de développer. 

On appelle généralement un dépot une "repo" (pour *repository* en anglais).

Pour créer un nouveau dépôt sur GitHub, cliquez sur le bouton vert `NEW` en haut à gauche où les dépôts sont listés puis cliquer sur le bouton `New Repository` :

(SCREEN)

Après cela, vous arriverez à une page où vous pourrez spécifier les informations pour votre nouveau dépôt, comme par exemple :
+ Le nom du projet (utilisez quelque chose de descriptif)
+ Une description générale du projet et de son objet.
+ Choisissez si vous voulez que le dépôt soit public ou privé.

Une fois que vous avez ajouté les informations et crée votre "repo", vous arriverez sur une page avec des instructions sur la façon de pousser votre projet local sur GitHub (nous verrons ces étapes plus en détail dans les prochains sections) :

##### Dépôt publique vs dépôt privé
En fonction de la nature du projet (qu'il soit ou non *open-source* par exemple), vous pouvez définir votre dépôt comme **public** ou **privé** :

+ **Dépôt public :** n'importe qui sur internet peut le voir. Attention! Même s'il est possible de voir le dépôt et de lire le code, vous serez le mainteneur du projet : C'est vous qui choisirez les personnes autorisées à modifier le code.
+ **Dépôt privé :** n'est accessible qu'à vous et aux personnes que vous invitez.

##### Le fichier `README.md`

+ Le fichier `README.md` est une présentation/description de votre projet. 
+ **Avantage :** Lorsque vous regardez le dépôt de quelqu'un sur GitHub, lire son fichier `README` vous permettra de comprendre ce que fait son code, quelles sont les dépendances à installer pour faire fonctionner son logiciel, etc...
+ **Il est très important qu'projet/dépôt soit correctement décrit et documenté** (si ce n'est pas le cas, personne ne voudra l'utiliser, l'améliorer ou le développer).

### Commandes git

#### Initialiser un projet git

Si vous démarrez un nouveau projet ou si vous avez un projet existant que vous souhaitez ajouter à `Git` et ensuite le mettre sur GitHub, vous devez d'abord initialiser le projet avec la commande `git init`.
Pour simplifier les choses, disons que nous voulons commencer à construire un nouveau projet. La première chose que je ferais habituellement est de créer un nouveau dossier dans lequel je stockerai les fichiers de mon projet.

```bash
mkdir nouveau-projet
cd nouveau-projet
git init
```

Chaque fois que vous initialisez un nouveau projet Git crée un répertoire `.git` dans lequel tous la configuration de votre "repo" est stockée.


#### Git Status

Chaque fois que vous apportez des modifications à votre projet Git et que vous souhaitez vérifier ce qui a changé, vous pouvez utiliser la commande `git status`

*Exemple de sortie avec le nouveau projet crée précédemment :*

    On branch main

    No commits yet
    
    nothing to commit (create/copy files and use "git add" to track)

Ajoutez un fichier `README.md` "générique" : 
```bash
echo "# Projet Démo" >> README.md
``` 

Si vous lancez `git status` encore une fois : 
    
    Untracked files:
      (use "git add <file>..." to include in what will be committed)
        README.md
    nothing added to commit but untracked files present (use "git add" to track)

Git détecte qu'il y a un nouveau fichier qui n'est pas "suivi", appelé *README.md*, (que nous venons de créer) et nous invite à utiliser la commande `git add` pour commencer à "suivre" le fichier.

#### git add

Par défaut, lorsque vous créez un nouveau fichier dans votre projet Git, il n'est pas "suivi". Pour indiquer à Git qu'il doit commencer à suivre le fichier, vous devez utiliser la commande `git add`.

```bash
git add NOM_DU_FICHIER
```
Dans l'exemple précédent :
```bash
git add README.md
```

Si vous lancez `git status`:

    Changes to be committed:
      (use "git rm --cached <file>..." to unstage)
        new file: README.md

Git nous indique que le fichier `README.md` est un nouveau fichier qui vient d'être mis à disposition, qui n'a pas été suivi auparavant et qui est prêt à être "commit"

Pour "suivre" plusieurs fichiers : 
```bash
git add NOM_DU_FICHIER1 NOM_DU_FICHIER2 NOM_DU_FICHIER3 
```

Pour "suivre" la totalité des fichiers non suivis dans le répertoire : 
```bash
git add .
```

{{% notice style="warning" title="Attention"%}}
Soyez prudents! Dans certains cas, il peut y avoir des fichiers que vous ne voulez pas ajouter à Git.
{{% /notice %}}

#### git commit
Une fois que vous avez ajouté vos fichiers, l'étape suivante est de valider ces modifications. Si vous exécutez à nouveau `git status`, vous pourrez voir que Git nous indique qu'il y a des modifications à valider :

    Changes to be committed:
      (use "git rm --cached <file>..." to unstage)
        new file: README.md

Dans ce cas, seul le fichier `README.md` sera validé. Pour ce faire, nous pouvons exécuter la commande suivante :

```bash
git commit -m "Commit initial"
```

+ `git commit` : pour indiquer à git que nous voulons livrer les changements que nous avons mis en place avec la commande git add
`-m `: indique que nous allons spécifier notre message qui va accompagner notre *commit*.
+ Entre les guillemets : notre message de livraison (**il est important d'écrire des messages de livraison courts et descriptifs de vos changements**).

#### git log

Afin de lister l'historique des commits, vous pouvez utiliser la commande suivante :

```bash
git log
```

### Clé SSH
Il existe plusieurs façons de s'authentifier auprès de GitHub. Essentiellement, vous en avez besoin pour pousser vos modifications locales depuis votre ordinateur portable vers votre dépôt GitHub.
Vous pouvez utiliser l'une des méthodes suivantes :
+ HTTPS : cette méthode requiert votre nom d'utilisateur et votre mot de passe GitHub à chaque fois que vous essayez d'envoyer vos modifications.
+ SSH (recommandé) : Avec SSH, vous pouvez générer une paire de clés SSH et ajouter votre clé publique à GitHub. De cette manière, votre nom d'utilisateur et votre mot de passe ne vous seront pas demandés à chaque fois que vous enverrez vos modifications sur GitHub.

#### Étapes pour se connecter à GitHub via SSH
+ Générer une nouvelle paire de clé 
```bash
ssh-keygen
```
+ Une fois crée, vous devez téléverser la clé publique sur votre compte GitHub. Copiez le résultat de la commande suivante : 
```bash
cat ~/.ssh/id_rsa.pub
```

+ Allez sur GitHub, cliquez sur votre photo de profil (en haut à droit) -> *Settings*-> *SSH and GPG Keys* -> *New SSH Key*
+ Spécifiez un titre pour votre clé (par exemple Laptop de travail), puis dans la section *Key*, collez votre clé publique et enfin cliquez sur *Add SSH Key*

#### git push

Enfin, une fois que vous avez effectué toutes vos modifications, que vous les avez mises en scène avec la commande git add . et que vous avez validé les modifications avec la commande git commit, vous devez pousser les modifications validées de votre dépôt local vers votre dépôt GitHub distant. Cela permet de s'assurer que le dépôt distant est mis à jour avec votre dépôt local.

```bash
git remote add origin https://github.com/VOTRE_USERNAME/NOM_REPO.git
git branch -M main
git push -u origin main
```
Après avoir exécuté la commande git push, vous pouvez vous rendre sur votre projet GitHub et vous pourrez voir les *commits* que vous avez apportées localement dans le dépôt distant sur GitHub. Si vous cliquez sur le lien *commits*, vous pourrez voir tous les *commits* comme si vous lanciez la commande `git log`.

#### git pull


Si vous travaillez sur un projet avec plusieurs personnes, il y a de fortes chances que le code change. Il vous faut donc un moyen de récupérer les dernières modifications du dépôt GitHub sur votre machine.

Vous savez déjà que vous pouvez utiliser la commande `git push` pour pousser vos derniers commits, donc pour faire l'inverse et télécharger les derniers *commits* de GitHub vous devez utiliser la commande `git pull`.

Pour tester cela, faisons un changement directement sur GitHub. Une fois sur GitHub, cliquez sur le fichier *README.md* et cliquez sur l'icône du crayon pour éditer le fichier :

(SCREEN)

Apportez une modification mineure au fichier, ajoutez un message et cliquez sur le bouton `Commit Changes` :

(SCREEN)

Si on essaie de push du nouveau code à partir de notre ordinateur, nous aurons une erreur : 

     ! [rejected] main -> main (fetch first)
    error: failed to push some refs to
    'git@github.com:bobbyiliev/demo-repo.git'
    hint: Updates were rejected because the remote contains work
    that you do
    hint: not have locally. This is usually caused by another repository pushing
    hint: to the same ref. You may want to first integrate the remote changes
    hint: (e.g., 'git pull ...') before pushing again.
    hint: See the 'Note about fast-forwards' in 'git push --help' for details.

Comme indiqué , le dépôt distant est en avance sur votre dépôt local, vous devez donc exécuter la commande git pull pour obtenir les dernières modifications :

```bash
git pull origin main
```

Résultat de la commande : 

    remote: Enumerating objects: 5, done.
    remote: Counting objects: 100% (5/5), done.
    remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
    Unpacking objects: 100% (3/3), 646 bytes | 646.00 KiB/s, done.
    From github.com:bobbyiliev/demo-repo
      * branch main -> FETCH_HEAD
        da46ce3..442afa5 main -> origin/main
    
      README.md | 3 ++-
      1 file changed, 2 insertions(+), 1 deletion(-)

Comme indiqué, le dépôt distant est en avance sur votre dépôt local, vous devez donc exécuter la commande `git pull` pour obtenir les dernières modifications :

```bash
git pull origin main
```

    remote: Enumerating objects: 5, done.
    remote: Counting objects: 100% (5/5), done.
    remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
    Unpacking objects: 100% (3/3), 646 bytes | 646.00 KiB/s, done.
    From github.com:bobbyiliev/demo-repo
      * branch main -> FETCH_HEAD
        da46ce3..442afa5 main -> origin/main
      README.md | 3 ++-
      1 file changed, 2 insertions(+), 1 deletion(-)

Nous pouvons voir que le fichier README.md a été modifié et qu'il y a eu 2 nouvelles lignes ajoutées et 1 ligne supprimée.
Maintenant, si vous lancez `git log`, vous verrez que le *commit* que vous avez fait sur GitHub est disponible localement.

Remarque 
Bien entendu, il s'agit d'un scénario simplifié. Dans le monde réel, vous ne feriez pas de modifications directement sur GitHub, mais vous travailleriez très probablement avec d'autres personnes sur le même projet, et vous devriez pull leurs dernières modifications régulièrement. Vous devez vous assurer que vous récupérez les dernières modifications à chaque fois avant d'essayer de push les votres.

#### Branches git
Jusqu'à présent, nous n'avons travaillé que sur la branche Main, qui est créée par défaut lors de la création d'un nouveau dépôt GitHub. Dans ce chapitre, vous en apprendrez plus sur les branches Git. Pourquoi en avoir besoin et comment les utiliser.

Les branches sont un moyen de travailler sur votre projet en ajoutant une nouvelle fonctionnalité ou en corrigeant des bogues sans affecter la branche principale.

De cette façon, chaque nouvelle fonctionnalité ou correction de bogue que vous développez peut vivre sur une branche séparée, et plus tard, une fois que vous êtes prêt et que vous avez entièrement testé les changements, vous pouvez fusionner la nouvelle branche à votre branche principale. Vous en apprendrez plus sur la fusion dans le prochain chapitre !

(ARBRE DE BRANCHES)

Grâce aux branches multiples, vous pouvez avoir plusieurs personnes travaillant sur différentes fonctionnalités ou corrections en même temps, chacune travaillant sur sa propre branche.

L'image montre 3 branches :
+ branche main (défaut)
+ branche 1
+ branche 2

La branche main est la branche par défaut. Nous pouvons considérer les deux autres branches comme deux nouvelles fonctionnalités en cours de développement. Par exemple, un développeur peut travailler sur un nouveau formulaire de contact pour votre application web sur la branche 1, et un autre développeur peut travailler sur une fonctionnalité de formulaire d'enregistrement d'utilisateur sur la branche 2. Grâce aux branches séparées, les deux développeurs peuvent travailler sur le même projet sans se gêner l'un l'autre.

+ Créer une branche :
```bash
git branch nouvelleFonctionnalite
```
+ Passer à la nouvelle branche :
```bash
git checkout nouvelleFonctionnalite
```
+ Pour exécuter les deux commandes en une :
```bash
git branch -b nouvelleFonctionnalite
```
+ Pour vérifier dans quelle branche on est :
```bash
git branch
```

Maintenant que notre branche est crée, ajoutez du contenu :
```bash
echo "<h1>Ma Première Fonctionnalité</h1>" > fonctionnalite1.html
git add fonctionnalite1.html
git commit -m "Ajout fonctionnalite1.html"
git push
```
#### git merge
Une fois que les développeurs ont terminé leurs modifications, ils peuvent fusionner leurs branches avec la branche *main* pour mettre les nouvelles fonctionnalités en ligne.

(ARBRE DES BRANCHES)

Si vous avez suivi les étapes précédentes, votre branche *nouvelleFonctionnalite* est maintenant en avance sur la branche *main* de 1 commit. Pour transférer ces nouveaux changements dans la branche principale, il faut fusionner la branche *nouvelleFonctionnalite*  dans notre branche *main*. 
```bash
# Passer à la branche main
git checkout main

# Fusionner la branche nouvelleFonctionnalite
git merge nouvelleFonctionnalite
```
Comme vous étiez sur la branche *main* lorsque vous avez lancé la commande `git merge`, Git va prendre tous les commits de la branche *nouvelleFonctionnalite* et les fusionner avec la branche *main*.

Dans notre cas, la fusion s'est déroulée sans problème car il n'y a pas eu de conflits. Toutefois, si vous travaillez sur un projet et que plusieurs personnes apportent des modifications, il peut y avoir des **conflits de fusion** (*Merge Conflicts*).
Cela se produit lorsque des modifications sont apportées à la même ligne d'un fichier, ou lorsqu'un développeur modifie un fichier sur une branche et qu'un autre développeur supprime le même fichier.

##### Laboratoire : résoudre des conflits

Simulons un conflit
+ Créez une nouvelle branche
```bash
git checkout -b demoConflit
```
+ Éditez le fichier `fonctionnalite1.html`
```bash
echo "<p>Démo conflit</p>" >> fonctionnalite1.html
```
+ Ajoutez et commit les changements :
```bash
git add fonctionnalite1.html
git commit -m "Démo conflit 1"
```
+ Retournez sur la branche *main* :
```bash
git checkout main
```
+ Faites un changement sur la même ligne que sur la branche `demoConflit` :
```bash
echo "<p>Conflit: changement sur la branche main</p>" >> fonctionnalite1.html
```
+ Ajoutez et commit les changements :
```bash
git add fonctionnalite1.html
git commit -m "Conflit sur main"
```

Maintenant votre branche principale et la branche demoConflit ont des changements dans le même fichier, sur la même ligne. 

+ Lançons la commande `git merge` :
```bash
git merge demoConflit
```
+ Sortie : 

    Auto-merging fonctionnalite1.html
    CONFLICT (content): Merge conflict in fonctionnalite1.html
    Automatic merge failed; fix conflicts and then commit the result.

Dans la sortie, on voit que la fusion échoue car il y a eu des modifications au même fichier sur la même ligne, donc Git n'est pas sûr de savoir quelle est la bonne modification.

Si vous vérifiez le contenu du fichier `fonctionnalite1.html`, vous verrez la sortie suivante :
```html
<h1>Ma Première Fonctionnalité</h1>
<p>Conflit: changement sur la branche main</p>
```
+ `<<<<<<< HEAD` : Indique le début des modifications sur votre branche actuelle. Dans notre cas, la ligne `<p>Conflit: changement sur la branche main</p>` est présente sur la branche main, qui est également la branche sur laquelle nous sommes.

+ `=======` : Indique où se terminent les changements de la branche actuelle et d'où proviennent les changements de la nouvelle branche. Dans notre cas, la modification de la nouvelle branche est la ligne `<p>Démo conflit</p>`.

+ `>>>>>>> demoConflit` : Indique le nom de la branche d'où proviennent les modifications.