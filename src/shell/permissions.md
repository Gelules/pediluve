# Permissions

## Comprendre les permissions

Tu te rappelles du *long listing format* de **ls** avec toutes ces informations
imbitables ? C'est le moment de les biter.

Reprenons dans répertoire Test vide.

```text
$ touch fichier
$ mkdir repertoire
$ cp /bin/ls . # Si tu as une erreur, essaie avec /usr/bin/ls
$ ls -l
total 136
-rw-r--r-- 1 gelules wheel      0 Jul 20 21:29 fichier
-rwxr-xr-x 1 gelules wheel 129728 Jul 20 21:29 ls
drwxr-xr-x 2 gelules wheel   4096 Jul 20 21:29 repertoire
$
```

La commande **cp** copie le binaire /bin/ls dans '.', c'est à dire le répertoire
où tu te trouves.

Il est très probable que tu n'aies pas la même sortie. Déjà au niveau des dates
et des heures, mais aussi sur la colonne avec "wheel". Ne t'inquiète pas, tout
va bien.

Décortiquons tout ça.

La première colonne contient les informations sur le type de fichier et les
permissions du fichier. Rappelle toi, '-' signifie que c'est un simple fichier,
et 'd' signifie que c'est un répertoire (**d**irectory).

Ensuite, le reste de la colonne, prenons le fichier **ls** :
```text
rwxr-xr-x
```

Il faut diviser ces 9 caractères en 3 groupes de 3 caractères.

| User | Group | Other |
| ---- | ----- | ----- |
| rwx  | r-x   | r-x   |

Avant d'expliquer les lettres, je dois expliquer les colonnes du tableau.

**User** donne des informations sur l'utilisateur qui possède le fichier. Si on
relit la sortie de **ls -l** plus haut, on peut voir que l'utilisateur qui
possède le fichier est **gelules**.

**Group** donne des informations sur le groupe qui possède le fichier. Si on
relit la sortie de **ls -l** plus haut, on peut voir que le groupe qui
possède le fichier est **wheel**.

**Other** est le reste du monde qui n'est ni l'utilisateur gelules ni les
utilisateurs dans le groupe wheel.

Tu peux voir dans quel groupe tu es avec la commande **group**.

```text
$ group
```

Revenons aux lettres.

**r** signifie **r**ead, pour lecture.

**w** signifie **w**rite, pour écriture.

**x** signifie e**x**ecute, pour exécution.

L'utilisateur a le droit de lire, modifier et exécuter le binaire.

Le groupe a le droit de lire et exécuter le binaire.

Tous les autres ont le droit de lire et exécuter le binaire.

## Changer les permissions

Pour modifier les permissions, tu peux utiliser la commande **chmod**.

Mais avant ça, il va falloir revoir un peu la base 2.

| r | w | x |
| - | - | - |
| 1 | 0 | 1 |

Tu peux voir ici, je demande à ce que les permissions du fichier donnent le
droit de lecture et d'exécution et interdisent le droit de modification. La
valeur de 101 en base 10 est... 5.

Il faut faire 3 fois cette gymnastique pour avoir 3 chiffres. Le 1er sera le
droit pour l'utilisateur, le 2eme les droits pour le groupe et le 3eme les
droits pour les autres.

Par exemple, je souhaite donner les permissions suivantes au fichier :
l'utilisateur peut lire, modifier et exécuter le fichier, le groupe peut lire et
modifier le fichier et les autres ne peuvent qu'exécuter le fichier.

| r | w | x | r | w | x | r | w | x |
| - | - | - | - | - | - | - | - | - |
| 1 | 1 | 1 | 1 | 1 | 0 | 0 | 0 | 1 |

Il faut traduire par paquet de 3.

On a donc :

111 = 7

110 = 6

001 = 1

Le droit à appliquer sera 761.

```text
$ chmod 761 ls
$ ls -l ls
-rwxrw---x 1 gelules wheel 129728 Jul 20 21:29 ls
$
```

Comme tu peux le voir, le fichier **ls** a vu ses permissions être modifiées.

Sache qu'un répertoire a des droits d'exécution. Le droit d'exécution d'un
répertoire permet de s'y **cd**.

Faisons un autre exemple.

```text
$ chmod 300 repertoire
```

Maintenant je n'ai que les droits de mofidication et d'exécution sur le
répertoire **repertoire**.

```text
$ nano repertoire/test
...
$ ls repertoire
ls: cannot open directory 'repertoire': Permission denied
$ cat repertoire/test
...
$
```

Tu ne peux pas afficher le contenu, mais tu peux quand même t'y déplacer et
modifier son contenu.
