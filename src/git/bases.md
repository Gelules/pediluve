# Commandes de bases

Tu vas effectuer quelques commandes de bases pour mieux appréhender Git. Rien de
spectaculaire mais tu sauras faire le minimum.

## init

Avant de jouer avec git, il faut initier le dépôt local.

### gitconfig

Avant d'initier un dépôt local, il faut configurer git avec au moins deux
informations : ton nom et ton mail.

Pour ça, tu vas créer un fichier **.gitconfig** dans ton **HOME** et le remplir
ainsi :

```text
$ cat ~/.gitconfig
[user]
    name = Gélules
    email = gelules@gelules.gelules
$
```

Evidemment, change les informations avec les tiennes.

Ces informations seront utiles pour savoir qui a créé quel commit.

```text
$ mkdir projet
$ cd projet
$ git init
```

Voilà, le répertoire **projet** est prêt à utiliser git.

Comment ça fonctionne ? Git crée en secret un répertoire caché qu'il utilise
pour suivre l'état du projet.

```text
$ ls -l .git
...
$
```

## status

**git status** est une commande fondamentale. Elle te permet de savoir où tu en
es dans ton travail.

Si tu le fais dans un répertoire vide, la commande te répondera qu'il n'y a rien
à commit, et qu'il faut utiliser **git add** pour commencer à suivre les
fichiers.

## add

Tu vas créer deux fichiers, **README** et **file_creator.sh**. Pour l'instant
ils seront vides.

```text
$ touch README file_creator.sh
$ git status
Untracked files:
  (use "git add <file>..." to include in what will be committed)
	README
	file_creator.sh
$ git add README file_creator.sh
$ git status
Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   README
	new file:   file_creator.sh
$
```

Tes fichiers sont prêts à être commités.

## commit

Pour créer un commit, il faut penser d'abord réfléchir à un message de commit
**intelligent**. Le tout premier est en *général* un simple **initial commit**.
Les prochains seront plus réfléchis selon le projet que tu effectues.

```text
$ git commit -m "initial commit"
[master (root-commit) 8a87f72] initial commit
 2 files changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 README
 create mode 100644 file_creator.sh
$
```

Tu as crées ton premier commit. Bravo !

Tu peux lire ici que c'est le *root-commit*, le tout premier du projet, et que
son changeset est *8a87f72*, et que 2 fichiers ont été créés avec les
permissions *644*.

Il est plus que probable que tu n'aies pas le même SHA-1. C'est normal.

A savoir : Git ne traque que la permission d'exécution. Si un fichier est
exécutable en local, il le sera aussi sur la remote.

## log

Maintenant que tu as crée ton premier commit, tu peux voir les logs du projet
évoluer avec la commande **git log**.

```text
$ git log
commit 8a87f728e30904f1cd837fd3ca2d4f17d11c0e58 (HEAD -> master)
Author: Gélules <gelules@gelules.gelules>
Date:   Sun Jul 21 22:15:07 2024 +0200

    initial commit
$
```

## On continue le projet sur Github

Dans la prochaine section, tu vas apprendre à créer un dépôt sur Github, à créer
des clés SSH pour garantir la sécurité de push et pull entre ton dépôt local et
la remote de GitHub et tu vas travailler ton projet que tu **pusheras** sur
GitHub pour voir l'évolution.
