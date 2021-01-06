# TP Git Flow

Version :0.0.1

note: https://dillinger.io/ pour visualiser page markdown
[comment]: <> (note: https://dillinger.io/ pour visualiser page markdown)

## Ajouter, commiter puis pusher sur le serveur distant :
    git add README.md
    git commit -m "add README"
    git push -u origin master
    
## Lister vos branches :
    git branch

## Installer Git flow si besoin (Linux) :
    sudo apt get install git-flow # (debian et dérivées)
    sudo yay -S --needed gitflow-avh gitflow-bashcomletion-avh # (AUR archlinux)

## Initialiser et paramétrer vos branches avec la commande suivante :
    git flow init
        Branch name for production releases: [master]
        Branch name for "next release" development: [develop]
        How to name your supporting branch prefixes?
        Feature branches? [feature/]
        Bugfix branches? [bugfix/]
        Release branches? [release/]
        Hotfix branches? [hotfix/]
        Support branches? [support/]
        Version tag prefix? []
        Hooks and filters directory? [C:/Users/Dell/Desktop/RepoGitFlow/.git/hooks]

## Appuyer sur “Enter” à chaque nouvelle entrée, il s’agit du paramétrage de notre Workflow.

Comme vous pouvez le constater, plusieurs branches et sous branches vont être créés.

## Lister vos branches :
    git branch
        * develop
        master

Nous constatons la création de la banche **develop**

## Commençons le développement d'une nouvelle fonctionnalité avec :
    git flow feature start homepage

        Basculement sur la nouvelle branche 'feature/homepage'

        Summary of actions:
        * A new branch 'feature/homepage' was created, based on 'develop'
        * You are now on branch 'feature/homepage'

        Now, start committing on your feature. When done, use:

            git flow feature finish homepage

## Lister vos branches :

    git branch
        develop
        * feature/homepage
        master

## Créer un nouveau fichier index.html :
    vi index.html

## Ajouter, commiter puis pusher sur le serveur distant :
    git add index.html
    git commit -m "add index.html"
    git push origin feature/homepage

## Publiez une fonctionnalité sur le serveur distant pour qu'elle puisse être utilisée par d'autres utilisateurs.
    git flow feature publish homepage

        La branche 'feature/homepage' est paramétrée pour suivre la branche distante 'feature/homepage' depuis 'origin'.
        Everything up-to-date
        Déjà sur 'feature/homepage'
        Votre branche est à jour avec 'origin/feature/homepage'.

        Summary of actions:
        - The remote branch 'feature/homepage' was created or updated
        - The local branch 'feature/homepage' was configured to track the remote branch
        - You are now on branch 'feature/homepage'

## Récupérer une fonctionnalité publiée par un autre utilisateur
    git pull origin feature/homepage

        warning: Tirer sans spécifier comment réconcilier les branches divergentes
        est découragé. Vous pouvez éliminer ce message en lançant une des
        commandes suivantes avant votre prochain tirage :

        git config pull.rebase false  # fusion (stratégie par défaut)
        git config pull.rebase true   # rebasage
        git config pull.ff only       # avance rapide seulement

        Vous pouvez remplacer "git config" par "git config --global" pour que
        ce soit l'option par défaut pour tous les dépôts. Vous pouvez aussi
        passer --rebase, --no-rebase ou --ff-only sur la ligne de commande pour
        remplacer à l'invocation la valeur par défaut configurée.

        Depuis https://github.com/MFranckFR/td_gitflow
        * branch            feature/homepage -> FETCH_HEAD
        Déjà à jour.

## Terminer la fonctionnalité
    git flow feature finish homepage

        Branches 'feature/homepage' and 'origin/feature/homepage' have diverged.
        And local branch 'feature/homepage' is ahead of 'origin/feature/homepage'.
        Basculement sur la branche 'develop'
        Merge made by the 'recursive' strategy.
        README.md  | 65 ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++-
        index.html | 16 ++++++++++++++++
        2 files changed, 80 insertions(+), 1 deletion(-)
        create mode 100644 index.html
        To https://github.com/MFranckFR/td_gitflow
        - [deleted]         feature/homepage
        Branche feature/homepage supprimée (précédemment 163cd59).

        Summary of actions:
        - The feature branch 'feature/homepage' was merged into 'develop'
        - Feature branch 'feature/homepage' has been locally deleted; it has been remotely deleted from 'origin'
        - You are now on branch 'develop'

## Cette action effectue les opérations suivantes:
* Fusionne Feature/homepage dans 'develop'
* Supprime la branche de fonctionnalité
* Passe sur la branche 'develop'

## Affichons notre historique :
    git log --oneline --graph --color --all --decorate

        * 94534fb (HEAD -> develop) add index.html
        * 328b454 (origin/master, master) init commit

## Commencer une livraison
    git flow release start v0.0.1

        Switched to a new branch 'release/v0.0.1'
        Summary of actions:
        - A new branch 'release/v0.0.1' was created, based on 'develop'
        - You are now on branch 'release/v0.0.1'
        Follow-up actions:
        - Bump the version number now!
        - Start committing last-minute fixes in preparing your release
        - When done, run:
        git flow release finish 'v0.0.1'

## Modifiez le fichier README.md en y insérant le texte 
Version :0.0.1

## Ajouter, commiter

    git add README.md
    git commit -m "add bump version"

## Terminer la livraison
    git flow release finish v0.0.1

## Une fenêtre s’ouvrira et vous demandera de rentre un message correspondant à un tag, insérer v0.0.1

## Taper esc , puis :wq

    Switched to branch 'master'
    Your branch is up to date with 'origin/master'.
    Merge made by the 'recursive' strategy.
    README.md | 1 +
    index.html | 0
    2 files changed, 1 insertion(+)
    create mode 100644 index.html
    Already on 'master'
    Your branch is ahead of 'origin/master' by 3 commits.
    (use "git push" to publish your local commits)
    Switched to branch 'develop'
    Merge made by the 'recursive' strategy.
    README.md | 1 +
    1 file changed, 1 insertion(+)
    Deleted branch release/v0.0.1 (was 625e7d9).
    Summary of actions:
    - Release branch 'release/v0.0.1' has been merged into 'master'
    - The release was tagged 'v0.0.1'
    - Release tag 'v0.0.1' has been back-merged into 'develop'
    - Release branch 'release/v0.0.1' has been locally deleted
    - You are now on branch 'develop'

## Envoyons sur le repository distant le tag que nous venons de créer
    git push –tags

        Enumerating objects: 9, done.
        Counting objects: 100% (9/9), done.
        Delta compression using up to 4 threads
        Compressing objects: 100% (6/6), done.
        Writing objects: 100% (7/7), 724 bytes | 241.00 KiB/s, done.
        Total 7 (delta 2), reused 0 (delta 0)
        To gitlab.com:DamienMonchaty/repogitflow.git
        * [new tag]
        v0.0.1 -> v0.0.1

## Mettez à jour vos remotes
    git push origin master
    git push origin develop

## Commencer un hotfix

Imaginons nous nous étions trompés dans le titre de notre page index, nous aurons mis en place un branche de correctif comme ceci :

    git flow hotfix start title

        Branches 'master' and 'origin/master' have diverged.
        And local branch 'master' is ahead of 'origin/master'.
        Switched to a new branch 'hotfix/title'
        Summary of actions:
        - A new branch 'hotfix/title' was created, based on 'master'
        - You are now on branch 'hotfix/title'
        Follow-up actions:
        - Start committing your hot fixes
        - Bump the version number now!
        - When done, run:
    
    git flow hotfix finish 'title'

## Modifiez le fichier index.html en y insérant le titre

    <title>Premier Git Flow</title>

## Ajouter, commiter :
    git add index.html
    git commit -m "changement du titre"

## Terminer un hotfix
    git flow hotfix finish title

## Une fenêtre s’ouvrira et vous demandera de rentre un message correspondant à cet Hotfix, insérer le texte suivant puis Puis taper esc , puis ":wq" pour enregistrer + terminer
    Hotfix title

## Lister vos branches :
    git branch
        * develop
        master

Taper **gitk** pour voir votre historique !!! Pour pouvoir continuer, veuillez fermer la fenêtre

## Affichons notre historique :
    git log --oneline --graph --color --all –decorate

## Pour afficher l’historique d’une seule branche, veuillez taper la commande suivante :
    git log --oneline --graph --color –decorate –first-parent develop

## Commençons le développement d'une nouvelle fonctionnalité avec :
    git flow feature start demo

## Modifier trois fois le fichier "index.html" avec votre éditeur

## et faire trois commits correspondants :
    git commit -a -m "a1"
    git commit -a -m "a2"
    git commit -a -m "a3"

## Terminer la fonctionnalité
    git flow feature finish demo

        Switched to branch 'develop'
        Merge made by the 'recursive' strategy.
        index.html | 2 +-
        1 file changed, 1 insertion(+), 1 deletion(-)
        Deleted branch feature/demo (was b84dd83).
        Summary of actions:
        - The feature branch 'feature/demo' was merged into 'develop'
        - Feature branch 'feature/demo' has been locally deleted
        - You are now on branch 'develop'

## Affichons notre historique :
    git log --oneline --graph --color --all –decorate

## Finir par :
    git push origin develop

## FIN du TP

# Exercices

Selon le TP, veuillez dans le meme projet à la suite :

## Créer une nouvelle release v0.0.2

* Créer un nouvelle hotfix, imaginons aue nous nous somme encore trompé dans le titre de la page index par exemple.
* Créer une nouvelle fonctionnalité appelé « contactpage ».
* Créer une nouvelle release v0.0.3.

## FIN 2