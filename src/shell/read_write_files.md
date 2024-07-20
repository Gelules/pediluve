# Lire et écrire dans des fichiers

Tu as vu comment créer des fichiers vides, mais tu n'as pas encore vu comment
écrire dedans et les lire à la ligne de commande.

## Ecrire dans un fichier

Pour écrire dans un fichier, tu peux utiliser l'éditeur de texte **nano** qui se
veut extrêmement simple d'utilisation et surtout s'exécute dans le terminal.

Mettons que tu sois dans ton **HOME**, nous allons faire les tests d'écriture et
lecture dans le répertoire Test.

```sh
$ mkdir Test
$ cd Test
```

Tu peux appeler **nano** sans nom de fichier derrière, tu pourras donner un nom
après.

```text
$ nano
  GNU nano 8.1                                                   New Buffer

































                                           [ Welcome to nano.  For basic help, type Ctrl+G. ]
^G Help          ^O Write Out     ^F Where Is      ^K Cut           ^T Execute       ^C Location      M-U Undo         M-A Set Mark
^X Exit          ^R Read File     ^\ Replace       ^U Paste         ^J Justify       ^/ Go To Line    M-E Redo         M-6 Copy
```

Tu peux directement écrire ton texte et te déplacer dans le fichier avec les
touches fléchées.

Tu peux voir en bas des commandes notées avec un circonflexe '^'. C'est un alias
pour la touche **ctrl**. Si tu veux sauvegarder ton fichier, appuie sur
**ctrl+o** pour *Write Out*.

Après cette combinaison, **nano** te demande le nom du fichier avec cette ligne
affichée en bas à gauche :
```text
File Name to Write:
```

Donne un nom de fichier. Tu peux même mettre un chemin entier pour le
sauvegarder ailleurs. Appelle ton fichier fichier_test.

Si tu veux quitter **nano**, exécute **ctrl+x**. Si tu as modifié ton fichier
entretemps, il te demandera si tu veux sauvegarder avant de quitter.

De retour sur le shell, tu peux rouvrir ton fichier avec nano en lui donnant son
nom en paramètre.

```sh
$ nano fichier_test
```

## Lire un fichier

Pour lire un fichier, tu peux utiliser la redirection gauche '<' en mettant le
nom de ton fichier.

```sh
$ fichier_test
# Contenu du fichier
$
```

Tu peux aussi utiliser la commande **cat**

```sh
$ cat fichier_test
# Contenu du fichier
$
```

**cat** te sera très utile pour vérifier que tes fichiers respectent une partie
de la norme. La norme en piscine est le style de code (la coding style) à suivre
pour que tes fichiers soient considérés comme valides.

Rouvre ton fichier avec nano et ajoute des espaces à la fin d'une ou plusieurs
lignes de texte. Exécute maintenant 
```sh
$ cat -e fichier_test
# Contenu du fichier avec des '$' en fin de ligne
$
```

Comme tu peux le voir, il y a des dollars en fin de ligne. Mais avant certains
dollars, il y a tes espaces. Ce n'est pas bien ! Un fichier de code ne doit pas
avoir d'espace qui donne ensuite sur une fin de ligne. Ce sont des caractères
inutiles présents dans tes fichiers. Ca prend de la place pour rien et c'est
moche, bouh !

Rouvre ton fichier avec nano et supprime ces espaces en trop.

```sh
$ cat -e fichier_test
Je suis un fichier$
avec     $
des $
espaces              $
en trop$
BERK                           $
$ # Bouh c'est moche
$ nano fichier_test
...
```

```sh
$ cat -e fichier_test
Je suis un fichier$
avec$
des$
espaces$
en trop$
BERK$
$ # Que c'est beau, je suis amoureux 
```
