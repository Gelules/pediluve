# La fonction main et l'environnement de développement

La fonction main est le point d'entrée des programmes en C.

Une fonction est une zone qui contient du code.

Tu pourras créer tes propres fonctions plus tard, que tu pourras appeler depuis
la fonction main.

Pour l'instant, voici ce que tu as :

```c
int main(void)
{
    return 0;
}
```

Décortiquons tout ça.

**int** signifie que la fonction retourne un **int**eger, c'est à dire un
entier. C'est effectivement le cas avec le **return 0** dans le code. Tu
retournes la valeur 0 dans le shell comme **exit status**.

**void** veut dire que la fonction ne prend pas de paramètres. Donc tu ne peux
pas envoyer de paramètre à l'exécution de ton programme, à l'inverse de
programmes que tu as déjà utilisés comme **ls**, **echo**, **mkdir**, etc. Tu
verras juste après comment faire.


Change le 0 par un 42, compile ton programme, et exécute le. Tu verras que tu
auras un **exit status** à 42.

```c
int main(void)
{
    return 42;
}
```

```text
$ gcc test.c -o mon_super_programme
$ ./mon_super_programme
$ echo $?
42
$
```

Tu comprends mieux maintenant comment les programmes que tu sais utiliser te
renvoient des **exit status** maintenant.

## Argument

La fonction **main** peut prendre des arguments. Voici comment :

```c
int main(int argc, char *argv[])
{
    return 0;
}
```

Oh là là, en voilà une nouvelle écriture compliquée.

Décortiquons tout ça.

**int argc** signifie que **argc** est de type **int**, c'est un entier. Il
s'agit ici du nombre d'arguments (*arguments counter*) que ton programme reçoit à son exécution. En
shell, c'est l'équivalent de la variable **$#**.

char \*argv[] ; celui là est un peu plus difficile. **char** signifie caractère.
Donc il y a des caractères en jeu ici, du texte.

L'étoile \* signifie pointeur, tu sauras ce que c'est plus tard.o

[] signifie **tableau** (array).

argv est un tableau de chaines de caractères. Il contient autant de chaines de
caractères que la valeur de **argc**.

Son nom signifie *arguments values*

Voici un bout de code pour voir les paramètres que tu envoies en entrée à ton
programme.

```c
#include <stdio.h>

int main(int argc, char *argv[])
{
    for (int i = 0; i < argc; i = i + 1)
    {
        printf("argv[%d] = %s\n", i, argv[i]);
    }

    return 0;
}
```

Que de nouvelles complications !

Décortiquons tout ça.

#include <stdio.h> veut dire qu'on va inclure stdio.h. C'est un fichier quelque
part dans les répertoires systèmes. C'est ce qu'on appelle une bibliothèque (et
pas une librairie, une librairie c'est un endroit avec des livres. En revanche
la traduction de bibliothèque en Anglais et library, d'où cet abus de langage).
Cette bibliothèque contient du code pour indiquer à gcc qu'il existe quelque
part une fonctione appelée **printf**.

Ensuite il y a une boucle for. La boucle for initialise une variable **i** de
type **int** à 0.
Elle va continuer son exécution tant que **i est plus petit que argc**, et à
chaque itération, **i s'incrémente de 1**. Tu peux voir que toutes les étapes de
la boucle sont séparées par des point-virgules ';'.

Ensuite, entre les accolades de la boucle, il y a un appel à la fonction
**printf**. Le nom de la fonction signifie **print format**. Tu vas formater du
texte avec des arguments.

Dans argv[%d], %d attend un entier. **i** qui est envoyé en paramètre juste
après sera remplacé et aura sa valeur affichée entre les crochets.

%s est un code qui attend une chaine de caractères. **argv** est le tableau qui
contient des chaines de caractères.

Enfin, \n signifie **saut à la ligne**. Plus exactement *linefeed*.

Compile et exécute ton programme ainsi :
```text
$ gcc test.c -o mon_super_programme
$ ./mon_super_programme coucou les loulous 0 1 10
argv[0] = ./mon_super_programme
argv[1] = coucou
argv[2] = les
argv[3] = loulous
argv[4] = 0
argv[5] = 1
argv[6] = 10
$
```

Voilà à quoi ressemble **argv** au moment de l'exécution
argv =
[
    ./mon_super_programme
    coucou
    les
    loulous
    0
    1
    10
]

Tu peux voir que **i** va aller de ligne en ligne pour afficher chaque valeur.

Tu te poses peut-être la question de pourquoi i commence à 0 et pas 1 ? C'est
comme ça que beaucoup de langages de programmation gèrent les accès mémoires, en
commençant par 0.

Attention, en shell tu aurais pu utiliser les valeurs 0, 1 et 10 comme entiers.
Ce n'est pas le cas ici, les valeurs sont des caractères, tu ne peux pas les
utiliser pour faire des maths comme tu as l'habitude de faire en shell.

Pour transformer une chaine de caractères en entier, tu peux utiliser la
fonction **atoi** qui signifie *ascii to integer*.

ASCII est un standard pour représenter des caractères.

```c
#include <stdio.h>
#include <stdlib.h>

int main(int argc, char *argv[])
{
    int age = 0;

    if (argc != 2)
        return 1;

    age = atoi(argv[1]);

    printf("J'ai %d ans\n", age);

    return 0;
}
```

Tout d'abord, la bibliothèque stdlib.h est inclue. Je te montrerai juste après
comment savoir quelle bibliothèque inclure selon ce que tu veux utiliser.

Je crée la variable **age** à 0 en tant qu'entier. C'est une bonne pratique,
toujours créer ses variables au tout début, avec des valeurs définies à 0, sauf
si tu as absolument besoin d'une autre valeur d'initialisation.

Ici, je teste si argc est différent de 2. Si c'est le cas, je quitte le
programme avec un exit status à 1. Tu peux voir que ce n'est pas comme en shell.
Je teste les valeurs avec des signes d'égalités, pas avec **-ne** comme tu as pu
le voir en shell.

Ensuite je dis que age est égal à l'appel de **atoi** sur le 1er argument. Puis
je l'affiche.

Je t'invite à compiler ton programme et le tester ainsi :

```text
$ gcc test.c -o mon_super_programme
$ ./mon_super_programme
$ echo $?
1
$ ./mon_super_programme 42
J'ai 42 ans
$ echo $?
0
$./mon_super_programme coucou
J'ai 0 ans
$ ./mon_super_programme 42coucou
J'ai 42 ans
$ ./mon_super_programme coucou42
J'ai 0 ans
$
```

**atoi** transforme ton paramètre en nombre seulement s'il trouve au début un
nombre, sinon il renvoie 0.

### man et bibliothèque

Pour savoir quel bibliothèque utiliser, tu vas utiliser ton meilleur ami, le
man.

```text
$ man atoi
...
```

Tu peux voir dans le man de atoi qu'il faut inclure stdlib.h.

Tu peux également vérifier dans le main quelle est la bibliothèque à inclure
pour printf. Il s'agit bien de stdio.h.

```text
$ man 3 printf
...
```

Attention à bien mettre 3 pour bien dire que c'est le printf du langage C que tu
veux utiliser, pas le binaire installé sur le système.

Plus tard dans ton cursus, tu utiliseras des *syscalls*, des appels systèmes. Ce
sont des fonctions fournies par le kernel Linux. La différence est qu'il faut
demander la 2eme section du manuel.

```text
$ man 2 write
```

Tu sauras avec le temps si tu cherches un syscall ou une fonction.

#### Recherche dans le man

Si tu veux lister les sections pour un mot en particulier dans le man, tu peux
utiliser la commande suivante :

```text
$ man -k printf
...
```

Tu verras que ça va générer **BEAUCOUP** de lignes. Tu peux filter en rajoutant
un circonflexe '^' au début du mot et un dollar '$' à a fin, le tout entre
simple quote.

```test
$ man -k '^printf$'
...
```

Ce sont des caractères spéciaux. ^ signifie début de ligne et $ signifie fin de
ligne.

```text
$ man -k '^read$'
...
```

Tu peux voir que *read* existe dans la section 1p, 2 et 3p. Si tu n'avais pas
limité la recherche avec ^ et $, tu aurais eu énormément de résultats pas très
intéressants.
