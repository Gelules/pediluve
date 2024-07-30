# Flux systèmes

## Sortie standard

La sortie standard (ou **stdout**) est le flux de texte affiché sur ton terminal
quand tout se passe bien.

Par exemple, quand tu exécutes
```text
$ ls -l fichier_existant # assure toi que le fichier existe
```
Tout ce qui est affiché passe par **stdout**.

Tu peux rediriger le flux dans un fichier en utilisant un chevron.

```text
$ ls -l > fichier_stdout
$ cat fichier_stdout
```

Comme tu peux le voir, **ls -l** n'a pas affiché de résultat, tout a été
redirigé dans un fichier qui n'existait pas.

Recommence l'opération.

```text
$ ls -l > fichier_stdout
$ cat fichier_stdout
```

Le fichier n'a pas gardé l'information précédente. Il a été *tronqué*.

Si tu veux garder le contenu du fichier à chaque redirection, tu peux utiliser
la **double redirection**.

```text
$ ls -l >> fichier_stdout
$ cat fichier_stdout
```

Et là, le contenu déjà présent reste dans le fichier.

Si tu veux rediriger stdout dans le **vide**, c'est à dire ne pas l'afficher et
ne pas le rediriger dans un fichier, tu peux utiliser le fichier **/dev/null**
comme fichier de redirection.

```text
$ ls -l > /dev/null
```

C'est un fichier spécial utilisé uniquement pour rediriger des flux dans le
vide.

## Erreur standard

Le flux standard des erreurs (ou **stderr**) s'affiche aussi sur ton terminal
mais en empruntant un autre flux. Il ne s'affiche qu'en cas d'erreur.

Prenons la situtation suivante :

```text
$ ls
fichier_existant
$ ls -l fichier_existant fichier_inexistant
ls: cannot access 'fichier_inexistant': No such file or directory
-rw-r--r-- 1 gelules wheel 0 Jul 20 21:29 fichier_existant
$
```

La première ligne avec le message d'erreur emprunte le flux d'erreur, et la
seconde emprunte stdout.

Tu peux les séparer dans des fichiers différents ainsi :
```text
$ ls -l fichier_existant fichier_inexistant >stdout.txt 2>stderr.txt
$ cat stdout.txt stderr.txt
...
```

Le **2** est le chiffre de référence pour **stderr**. **stdout** utilise **1**
mais tu n'es pas obligé de l'écrire, sauf à une condition.

Si tu veux rediriger **stderr** vers **stdout**, tu dois le faire de cette
façon.

```text
$ ls -l fichier_existant fichier_inexistant 1>stdout.txt 2>&1
```

Le caractère **esperluette** '&' indique au shell que **1** n'est pas un nom de
fichier mais le flux numéro 1.

Le premier **1** devant **stdout.txt** n'est pas obligatoire, mais je voulais te
montrer que tu peux l'écrire quand même.

## Pipe

Les pipes servent à rediriger le **stdout** d'un programme dans le **stdin**
d'un autre programme.

**stdin** est **l'entrée standard**. C'est un flux où tu fais en temps normal de
l'entrée clavier. Ce que fais ton shell à chaque fois que tu appuies sur Entrée,
il lit son entrée standard pour recevoir ta commande.

Faisons quelques exemples plus parlant :
```text
$ ls
$ ls -l / > racine.txt
$ wc -l racine.txt
```

**wc -l** te permet de compter le nombre de lignes dans un fichier. Mais tu
aurais pu faire ça en une seule commande grâce au **pipe** (tuyau).

```text
$ ls -l / | wc -l
```

Le pipe '|' te permet de passer la sortie de **ls** dans l'entrée de **wc**.

Beaucoup d'outils sur Linux fonctionne ainsi.

Prenons un enchaînement de commandes plus drôle :

```text
$ ls -l / | cut -d ' ' -f 1 | tee permissions | wc -l
```

Voici deux nouvelles commandes.

**cut** va couper des colonnes selon un délimiteur.

Prenons la sortie de **ls -l /**.
```text
$ ls -l /
total 56
lrwxrwxrwx   1 root root       7 Apr  7 20:02 bin -> usr/bin
drwxr-xr-x   4 root root    4096 Jul 19 01:59 boot
drwxr-xr-x  19 root root    3880 Jul 20 16:52 dev
drwxr-xr-x  95 root root    4096 Jul 20 22:14 etc
drwxr-xr-x   3 root root    4096 Sep 13  2022 home
lrwxrwxrwx   1 root root       7 Apr  7 20:02 lib -> usr/lib
lrwxrwxrwx   1 root root       7 Apr  7 20:02 lib64 -> usr/lib
drwx------   2 root root   16384 Sep 13  2022 lost+found
drwxrwx---   1 root vboxsf  4096 Jul  1 02:05 media
drwxr-xr-x   2 root root    4096 Dec  7  2021 mnt
drwxr-xr-x   2 root root    4096 Dec  7  2021 opt
dr-xr-xr-x 227 root root       0 Jul 20 16:52 proc
drwxr-x---  14 root root    4096 Sep 23  2023 root
drwxr-xr-x  29 root root     680 Jul 20 16:55 run
lrwxrwxrwx   1 root root       7 Apr  7 20:02 sbin -> usr/bin
drwxr-xr-x   4 root root    4096 Sep 13  2022 srv
dr-xr-xr-x  13 root root       0 Jul 20 21:28 sys
drwxrwxrwt  15 root root     360 Jul 21 00:00 tmp
drwxr-xr-x  10 root root    4096 Jul 20 22:14 usr
drwxr-xr-x  12 root root    4096 Jul 20 16:52 var
```

La commande **cut** que j'utilise délimite chaque **field** (champ) en utilisant
le délimiteur ESPACE ' '.

On n'aura donc que la première colonne avec **cut**.
On n'aura donc que la première colonne avec **cut -d ' ' -f 1**

```text
$ ls -l / | cut -d ' ' -f1
total
lrwxrwxrwx
drwxr-xr-x
drwxr-xr-x
drwxr-xr-x
drwxr-xr-x
lrwxrwxrwx
lrwxrwxrwx
drwx------
drwxrwx---
drwxr-xr-x
drwxr-xr-x
dr-xr-xr-x
drwxr-x---
drwxr-xr-x
lrwxrwxrwx
drwxr-xr-x
dr-xr-xr-x
drwxrwxrwt
drwxr-xr-x
drwxr-xr-x
```

Ensuite la commande **tee** va rediriger sa sortie dans deux flux, un fichier et
**stdout**.
Imagine la lettre 'T' (tee en pronociation Anglaise), la barre de gauche est son
entrée standard, la barre qui descend est le fichier, la barre de droite est
**stdout**.

```text
$ ls -l / | cut -d ' ' -f1 | tee permissions
total
lrwxrwxrwx
drwxr-xr-x
drwxr-xr-x
drwxr-xr-x
drwxr-xr-x
lrwxrwxrwx
lrwxrwxrwx
drwx------
drwxrwx---
drwxr-xr-x
drwxr-xr-x
dr-xr-xr-x
drwxr-x---
drwxr-xr-x
lrwxrwxrwx
drwxr-xr-x
dr-xr-xr-x
drwxrwxrwt
drwxr-xr-x
drwxr-xr-x
$ cat permissions
...
```

tee a bel et bien redirigé ce que tu vois sur **stdout** dans un fichier nommé
**permissions**.

Et enfin, **wc -l** affiche le nombre de ligne reçu depuis **stdout**.

Voilà la puissance de Linux. Utiliser la sortie d'un programme comme donnée pour
l'entrée d'un autre programme.
