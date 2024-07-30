# Tests et conditions

Tu sais récupérer les variables envoyées en paramètres à ton script, tu sais en
créer, tu sais faire un peu de maths et afficher toutes ces variables. C'est
bien. Mais que dirais-tu de rendre tes scripts un peu plus vivants ? D'avoir des
exécutions différentes selon ce que tu envoies en paramètres ? C'est déjà plus
intéressant.

## Conditions

Une condition en shell est un test qui va renvoyer Vrai ou Faux. Si c'est Vrai,
alors le script va emprunter un chemin d'exécution, si c'est Faux, alors le
script va emprunter un autre chemin d'exécution.

# Test

Tu peux tester plusieurs choses en shell : les nombres, les chaînes de
caractères, l'existence de fichier, les exécutions d'autres programmes.

Je t'invite à lire le **man 1 test** qui liste tous les tests possibles.

Comme tu peux le vois, on peut combiner les tests avec les portes logiques
**AND** et **OR**.

Par exemple pour tester une chaîne de caractères, tu utilises le test

```sh
[ chaine1 = chaine2 ]
```

Ce test renverra Faux.

Attention à bien laisser des ESPACES ' ' entre le signe '$' et à côté des
crochets '[' et ']'. Si tu ne laisses pas d'espaces, le shell ne comprendra pas
que c'est un test et boguera.

### Protection

Avant de montrer des exemples, je dois te montrer une technique de protection
des scripts pour éviter des crashs embêtants.

```sh
#!/bin/sh

mot_de_passe=$1

if [ $mot_de_passe = "pediluve" ]
then
    echo "Ouverture de la porte secrète"
else
    echo "Mauvais mot de passe"
fi
```

Exécute ce script sans lui envoyer de paramètre.

```text
$ ./script.sh
./script.sh: line 5: [: =: unary operator expected
Mauvais mot de passe
$
```

Que s'est-il passé ?

La variable n'a pas de valeur, le shell a donc lu la ligne avec le test
littéralement de cette manière :

```sh
if [ = "pediluve" ]
```

Ceci n'est pas du shell valide. Il faut une valeur avant le signe '='.

Tu peux protéger ta variable en lui mettant des double quotes.

```sh
#!/bin/sh

mot_de_passe=$1

if [ "$mot_de_passe" = "pediluve" ]
then
    echo "Ouverture de la porte secrète"
else
    echo "Mauvais mot de passe"
fi
```

Si tu exécutes le script sans paramètre, voici ce que le shell lit.

```sh
if [ "" = "pediluve" ]
```

Le shell comprend alors qu'il teste une chaîne de caractères vide avec
"pediluve".

## Exemples

### if elif else

Avant de te montrer de réels exemples, tu vas apprendre à enchainer les tests.

**if** sert à tester une ou plusieurs conditions. Si tout est **Vrai**, alors le
code qui suit sera exécuté.

**elif** est la concaténation de **else if**. Il faut aussi mettre une
condition, et si la condition est **Vraie**, alors le code qui suit sera
exécuté. Tu peux enchainer autant de **elif** que tu veux. Tu n'es pas obligé
d'utiliser **elif** quand tu fais des tests.

**else** contient du code qui sera exécuté si tous les tests précédents étaient
**Faux**. Il ne faut pas lui mettre de test.

```sh
#!/bin/sh

# Si le code secret n'est pas bon
# on écrit sur stderr que le code est faux
# et on quitte le script avec l'exit status 1
if [ "$1" != "super_mot_de_passe" ]
then
    echo "Mauvais mot de passe" >&2
    exit 1
fi

if [ "$2" = "gelules" ]
then
    echo "Bonjour maitre"
elif [ "$2" = "pediluvien" ]
then
    echo "Bonjour jeune apprenti"
elif [ "$2" = "piscinien" ]
then
    echo "Bonjour, tu viens te rafraichir la mémoire ?"
else
    echo "Tu m'es inconnu"
fi
```

### Petit jeu vidéo

Pour apprendre à faire des tests, au lieu de t'énumérer tous les tests
possibles, je préfère te montrer plein d'exemples différents. A toi ensuite de
lire le **man 1 test** pour compléter tes connaissances.

Imaginons que tu codes un petit jeu vidéo en shell.

```sh
#!/bin/sh

# Si le nombre d'arguments n'est pas 2
if [ $# -ne 2 ]
then
    echo "Usage: $0 LOGIN SALLE_DE_TP" >&2
    exit 1
fi

login=$1
tp=$2
save_file=sauvegarde.txt

# Si le fichier de sauvegarde n'existe pas et que c'est bien un pédiluvien qui
# joue au jeu, on crée le fichier de sauvegarde
if [ ! -f "$save_file" ] -a [ "$login" != "gelules" ]
then
    touch "$save_file"
fi

# Exception pour le maitre de jeu
if [ "$login" = "gelules" ]
then
    echo "TP gelules dans 'salle secrète'" >> "gelules_sauvegarde.txt"
    exit
fi

if [ "$tp" = "donjon" ]
then
    echo "TP $login dans 'donjon'" >> "$save_file"
    exit
elif [ "$tp" = "tour" ]
then
    echo "TP $login dans 'tour'" >> "$save_file"
    exit
elif [ "$tp" = "chambre" ]
then
    echo "TP $login dans 'chambre'" >> "$save_file"
    exit
else
    echo "Mauvaise TP" >&2
    exit 1
fi
```

Je te laisse essayer le script.

Il n'est pas optimisé du tout. Comme tu peux le voir, il y a du code qui se
répète. On retrouve beaucoup de fois

```sh
echo "TP $login dans 'LIEU'" >> "$save_file"
```

mais c'est un problème pour plus tard. Pour l'instant il faut que tu apprennes à
jouer avec les tests.

Je t'invite à regarder plus en détail comment tester les nombres. Dans mon
exemple je teste si le nombre d'argument est **N**ot **E**qual à 2. Mais tu peux
tester une égalité, si le nombre est strictement inférieur ou inférieur ou égal,
et pareil avec la supériorité.
