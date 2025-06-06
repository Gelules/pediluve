# RTFM : Read The Fucking Manual

Pour en apprendre d'avantages quant aux commandes que tu ne maitrises pas, il
faut que tu fasses confiance à ton meilleur ami : ~~Google~~ le manuel.

Pour l'invoquer, utilise la commande **man**.

```text
$ man ls
```

Le manuel s'affiche. Pour t'y déplacer, utilise les touches fléchées. Pour le
quitter, appuie sur **q**.

Chaque commande a son manuel, mais aussi certaines notions de Linux.


Par exemple, si tu veux en apprendre plus sur ton système de fichier, exécute la
commande
```text
$ man hier
```

hier pour *hierarchy*.

Et si tu veux apprendre à utiliser le manuel, alors consulte le manuel du
manuel.

```text
$ man man
```

Chose intéressante dedans, les sections.
```text
The table below shows the section numbers of the manual followed by the types of pages they contain.

1   Executable programs or shell commands
2   System calls (functions provided by the kernel)
3   Library calls (functions within program libraries)
4   Special files (usually found in /dev)
5   File formats and conventions, e.g. /etc/passwd
6   Games
7   Miscellaneous (including macro packages and conventions), e.g. man(7), groff(7), man-pages(7)
8   System administration commands (usually only for root)
9   Kernel routines [Non standard]
```

Pour ta picine, les 3 premières sections seront à consulter.

La 1ere contient celle des **binaires** (des programmes) que tu utilises depuis
ton shell.

La 2eme et la 3eme contiennet des fonctions que tu peux appeler quand tu fais
du langage C. La 2eme est celle des fonctions que ton Kernel te propose, la 3eme
sont les fonctions de la libc (bibliothèque C).

Un exemple. Si tu veux afficher le manuel de la fonction C printf (tu ne sais
peut-être pas encore ce que c'est, ce n'est pas grave), tu serais tenté
d'exécuter.

```text
$ man printf
```

Si tu le fais, tu verras en haut à gauche **printf(1)**, le '1' entre
parenthèses signifie que tu es dans la **1**ère section du manuel. Ce que tu
veux c'est la **3**ème, pour les appels de la bibliothèque C (library calls).

![mauvais printf](./rtfm/printf_wrong.png "mauvais printf")

Il faut alors utiliser une de ces deux notations :
```text
$ man 3 printf
$ man printf.3
```

![bon printf](./rtfm/printf_good.png "bon printf")

A partir de maintenant, pour toutes les commandes que tu as vues et verras, je
t'invite très fortement à lire le manuel à chaque fois.
