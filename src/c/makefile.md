# Makefile

Un cours complet sur les Makefiles serait bien disproportionné pour un Pédiluve.

Aussi je t'invite à voir ces deux vidéos pour un cours plus complet.

[Makefile, introduction](https://www.youtube.com/watch?v=om6pqsebNQo)

[Makefile, Wvla](https://www.youtube.com/watch?v=ETJH8ne8nAQ)

Pour la suite, je vais te proposer un Makefile fonctionnel, préconstruit. Je te
montrerai comment l'utiliser et comment le modifier en cas d'ajout de fichier.

```makefile
CFLAGS = -std=c99 -pedantic -Wall -Wextra -Wvla -Werror
OBJ = test.o math.o
BIN = test
TARGET = mon_super_programme

all: $(BIN)
        @mv $< $(TARGET)

$(BIN): $(OBJ)

clean:
        $(RM) $(OBJ) $(BIN) $(TARGET)
```

Pour utiliser ce Makefile, tu dois tout simplement appeler **make**.

```text
$ make
cc -std=c99 -pedantic -Wall -Wextra -Wvla -Werror   -c -o test.o test.c
cc -std=c99 -pedantic -Wall -Wextra -Wvla -Werror   -c -o math.o math.c
cc   test.o math.o   -o test
$ ls
Makefile  math.c  math.h  math.o  mon_super_programme  test.c  test.o
$
```

Et voilà, tu as automatisé ta compilation !

Décortiquons tout ça.

Il y a 4 variables dans ce Makefile, CFLAGS, OBJ, BIN et TARGET.

* CFLAGS a les flags de compilation.
* OBJ est le nom de tes fichiers C compilés en fichiers objets, remplace tout simplement l'extension .c en .o
* BIN est un de tes fichiers .c sans extension
* TARGET est le nom du binaire que tu veux avoir comme programme

Si tu veux ajouter des fichiers C dans tes projets, ajoute les noms des fichiers
dans OBJ en remplaçant .c par .o.

Pour faciliter la compilation, il faut que BIN soit le nom d'un fichier .o sans
l'extension.

TARGET est le nom du programme que tu veux avoir à la fin

Enfin, dans la recette **all**, on *move* le nom du binaire généré par celui de
TARGET. On utilise un arobase '@' devant l'instruction pour que ça ne soit pas
affiché pendant l'appel à **make**.

Un fichier objet est un fichier C compilé en langage machine.

Si tu veux supprimer les fichiers générés (le binaire, les fichiers objets,
...), appelle la target **clean** dans la ligne de commande.

```text
$ make clean
rm -f test.o math.o test mon_super_programme
$
```

Je t'invite à regarder les vidéos pour avoir plus de détails sur les Makefiles.
