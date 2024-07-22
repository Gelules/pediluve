# Quotting

Le quotting est la façon de formater du texte. Tu te rappelles de la commande
**echo** qui affiche du texte sur **stdout** mais qui peut aussi afficher des
variables.

## Simple quote

La simple quote te permet d'afficher du texte sans qu'il ne soit évalué. Ca
veut dire que tu peux afficher le nom d'une variable sans qu'elle soit remplacée
par sa valeur.

```sh
$ cat script.sh
#!/bin/sh

nom=gelules
echo 'Mon nom est $nom'
$ ./script.sh
Mon nom est $nom
$
```

Comme tu peux le voir, mettre du texte entre simple quote affiche le texte tel
qu'écrit dans le script, sans être évalué par le shell.

## Double quote

Le double quote te permet de visuellement savoir où commence et où termine ton
texte, le shell qui sera dedans sera évalué. Avec **echo**, c'est comme ne pas
mettre de quotes, mais tu te repères plus facilement à la lecture de ton script.

```sh
$ cat script.sh
#!/bin/sh

nom=gelules
echo "Mon nom est $nom"
$ ./script.sh
Mon nom est gelules
$
```

## Escape

Une question t'a peut-être traversé l'esprit : Comment afficher une simple quote
ou une double quote sans qu'elle ne soit comprise comme un début ou fin de texte
? Ou même afficher le signe dollar '$' sans utiliser de simple quote ?

Tu peux **échapper** un caractère spécial avec l'antislash.

```sh
$ cat script.sh
#!/bin/sh

echo Voici un dollar : \$
echo Voici un simple quote : \'
echo Voici un double quote : \"
echo Voici un antislash: \\
$ ./script.sh
Voici un dollar : $
Voici un simple quote : '
Voici un double quote : "
Voici un antislash: \
$
```

Entre simple quote, tu peux afficher sans problème un double quote. Pareil
inversement, tu peux entre double quote afficher un simple quote.

```sh
$ cat script.sh
#!/bin/sh

echo "Voici un double quote entre double quote => \" <= pas mal hein ?"
echo 'Voici un double quote entre simple quote => " <= pas mal hein ?'
echo "Voici un simple quote entre double quote => ' <= pas mal hein ?"
```
```text
$ ./script.sh
Voici un double quote entre double quote => " <= pas mal hein ?
Voici un double quote entre simple quote => " <= pas mal hein ?
Voici un simple quote entre double quote => ' <= pas mal hein ?
$
```

Tu ne peux en revanche rien échapper entre simple quote. Donc pas de simple
quote entre simple quote. Mais tu peux arrêter ton simple quote en plein milieu
de ton appel à **echo**, échapper la simple quote et reprendre en simple quote
juste après.

```sh
$ cat script.sh
#!/bin/sh

echo 'Je fais presque tout en simple quote, en voici une =>' \' '<= pas mal hein ?'
```

```text
$ ./script.sh
Je fais presque tout en simple quote, en voici une => ' <= pas mal hein ?
$
```
