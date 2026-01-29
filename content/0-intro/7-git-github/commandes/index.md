+++
pre = '<b>7.3 </b>'
title = 'Commandes'
weight = '175'
draft = false
+++


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


#### git status

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

Git détecte qu'il y a un nouveau fichier qui n'est pas "suivi" (*untracked*), appelé *README.md*, (que nous venons de créer) et nous invite à utiliser la commande `git add` pour commencer à "suivre" le fichier.

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
+ Entre les guillemets : notre message de livraison (**il est important d'écrire des messages de livraison courts et descriptifs de vos changements (Ex: Authentification des utilisateurs**)).

#### git log

Afin de lister l'historique des commits, vous pouvez utiliser la commande suivante :

```bash
git log
```



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

Pour tester cela, faisons un changement directement sur GitHub. Une fois sur GitHub, cliquez sur le fichier *README.md* et cliquez sur l'icône du crayon pour éditer le fichier.

Apportez une modification mineure au fichier, ajoutez un message et cliquez sur le bouton `Commit Changes`.


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