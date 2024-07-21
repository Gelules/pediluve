# Scripts

Voici un gros chapitre, l'introduction aux scripts shell !

On va voir ici comment créer un fichier script, comment l'exécuter et afficher
les paramètres qu'on lui donne. Les prochaines chapitres étofferont petit à
petit ce que tu peux faire par le script.

En définition, un script shell, c'est juste un fichier avec des commandes
shells. En exécutant le fichier, tu exécuteras les commandes dedans.

En réalité, quand tu exécutes ton shell au clavier, il ne fait pas de différence
avec un fichier script. Il est juste en attente de la prochaine ligne à lire et
attend la fin de fichier (que tu peux envoyer avec la combinaison **ctrl+d**, ce
qui fermera ton shell).

Ce qui fait que tout ce que tu vas voir à partir d'ici est possible à exécuter
dans ton terminal.

Voici le minimum d'un script shell :
```
#!/bin/sh
```

C'est un commentaire particulier qui indique quel interpréteur utiliser. Par
habtiude on utilise **/bin/sh** car c'est un interpréteur présent sur tous les
systèmes Linux. Plus rarement tu verras **/bin/bash** car ce dernier a des
extensions que n'a pas **sh**. Evite de mettre **zsh** à moins de réellement
utiliser une fonctionnalité qui n'est pas présente sur **sh**, car tous les
systèmes n'ont pas **zsh** installés.

Pour rendre exécutable ton script, tu peux calculer les valeurs qui vont bien
avec **chmod**, ou aller plus vite en exécutant cette commande :
```sh
$ chmod +x script.sh
```

Et maintenant pour l'exécuter :
```sh
$ ./script.sh
```

Voilà. Ton script ne fait pas encore grand chose.

Pour information, je vais écrire un énorme script, mais ne t'inquiète pas, il
est **commenté** pour que tu comprennes ce que fait le script. Je donnerai
ensuite des exemples d'exécution pour que tu voies les différences.

Avant de montrer le script, je dois te présenter une nouvelle commande :
**echo**. Elle affiche ce que tu lui donnes en paramètre sur **stdout**.

```sh
$ echo Coucou les amis !
Coucou les amis !
$
```

Ce ne te semble pas utile pour le moment, mais ça va vite changer.

```sh
#!/bin/sh

# Afficher la façon dont on exécute le script
echo $0

# Afficher le nombre d'argument
echo $#

# Afficher le 1er argument
echo $1

# Afficher le 2eme argument
echo $2

# Afficher le 9eme argument
echo $9

# Afficher le 10ème argument
echo ${10}

# Afficher la liste des arguments avec *
echo $*

# Afficher la liste des arguments avec @
echo $@
```

Ce que tu vois ici sont des variables spéciales. Elles sont en lien avec le
script et auront des valeurs différentes selon comment tu exécutes le script.

Exécute le script avec ces paramètres et regarde ce qu'il se passe.

```sh
$ ./script.sh
...
$ ./script.sh toto
...
$ ./script.sh toto tata titi tutu
...
$ ./script.sh toto 'tata titi' tutu
...
$ ./script.sh toto "tata titi" tutu
...
$ ./script.sh je vais toucher le 10eme argument juste pour voir qu il s affiche bien
...
$
```

Tu comprendras la différence entre les deux dernières variables plus tard.
