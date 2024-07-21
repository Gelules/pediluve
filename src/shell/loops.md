# Boucles

Les boucles sont un moyen de répéter une séquence de code autant de fois que
nécessaire.

Imagine que tu veuilles créer les fichiers day_0.txt day_1.txt day_2.txt etc.
jusqu'à day_10.txt. Tu ne vas quand même pas écrire les noms de ces 11 fichiers
dans ton script ?

## while

**while** a une iou plusieurs conditions, et le code de la condition sera
répété tant que la condition est **Vraie**.

```sh
#!/bin/sh

i=0
while [ i -le 10 ]
do
    touch day_${i}.txt
    i=$((i + 1))
done
```

Ce code va créer la liste des fichiers day_0.txt jusqu'à day_10.txt.

Essaie maintenant de modifier le script pour le rendre plus modulable. Tu dois
utiliser des arguments pour :

* Avoir un nom de fichier différent que day
* Partir d'un nombre de départ différent que 0
* Finir à un nombre différent que 10. Attention, le nombre de fin doit être
  strictement supérieur que le nombre de départ
* Avoir une extension différent que txt

Voici un exemple de corrigé :
```sh
#!/bin/sh

if [ $# -ne 4 ]
then
    echo "Usage: $0 FILENAME START STOP EXTENSION" >&2
    exit 1
fi

if [ "$3" -le "$2" ]
then
    echo "Le nombre de départ doit être strictement supérieur que le nombre de fin" >&2
    exit 1
fi

filename=$1
start=$2
stop=$3
extension=$4

while [ "$start" -le "$stop" ]
do
    touch "${filename}_${start}.${extension}"
    start=$((start + 1))
done
```

On peut tester l'environnement du système. Par exemple, tant qu'un répertoire
n'existe pas, on boucle sur un message d'erreur.

```sh
#!/bin/sh

while [ ! -d ventre ]
do
    echo "Le répertoire 'ventre' n'existe pas"
done

touch ventre/gateau_chocolat
touch ventre/gateau_caramel
touch ventre/gateau_vanille
touch ventre/gateau_pistache

echo "Burp"
```

Il faut utiliser un deuxième shell pour créer le répertoire.

### Lire un fichier ligne par ligne

Il est possible de lire un fichier ligne par ligne avec une boucle while.

```sh
#!/bin/sh

if [ ! -f input_file ]
then
    echo "input_file n'existe pas" >&2
    exit 1
fi

while read line
do
    echo "La ligne est: $line"
done < input_file
```

Evidemment, tu peux remplacer **input_file** par un paramètre.

## until

**until** est exactement la même chose que **while**, à la différence que le
code exécuté est répété tant que la condition est **Fausse**. Plus exactement,
**jusqu'à** ce qu'elle soit **Vraie**.


```sh
#!/bin/sh

i=0

# Tant que i n'égale pas 10, on exécute le code de la boucle
until [ $i -eq 10 ]
do
    echo $i
    i=$((i + 1))
done
```

## for

**for** sert à boucler sur une séquence. Avec un point de départ, un point de
fin.

Tu peux boucler sur un ensemble d'éléments, ou une séquence de nombres.

```sh
#!/bin/sh

for element in je suis un sequence
do
    echo $element
done
```

Tu peux boucler sur des séquences générées en pure shell.

```sh
#!/bin/sh

for element in {a..z}
do
    echo $element
done
```

Pour les nombres il y a une différence. Je te laisse tester toutes ces
différences :

```sh
#!/bin/sh

# De 1 à 20 par pas de 1
for nombre in {1..20}
do
    echo $nombre
done

# De 1 à 20 par pas de 4
for nombre in {1..20..4}
do
    echo $nombre
done

# De 20 à 1 par pas de 1
for nombre in {20..1}
do
    echo $nombre
done

# De 20 à 1 par pas de 6
for nombre in {20..1..6}
do
    echo $nombre
done
```

Tu peux aussi boucler sur les paramètres. Tu vas ici comprendre la différence
entre **$@** et **$***

Teste les scripts avec au moins deux paramètres.

```sh
#!/bin/sh

for arg in $@
do
    echo $arg
done
```

```sh
#!/bin/sh

for arg in $*
do
    echo $arg
done
```

Jusqu'ici, aucune différence. Ajoute maintenant les variables entre double
quotes.

```sh
#!/bin/sh

for arg in "$@"
do
    echo $arg
done
```

```sh
#!/bin/sh

for arg in "$*"
do
    echo $arg
done
```

Tu peux maintenant voir la différence. **$@** reste une liste alors que **$\***
devient un seul argument.
