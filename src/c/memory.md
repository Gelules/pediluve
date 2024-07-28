# Mémoire

Pour l'instant, tu n'as fait que jouer avec des variables locales aux fonctions
que tu codes. Rappelle toi que ces variables ne sont vivantes que le temps
d'exécution de la fonction.

Comment créer une zone mémoire qui survivrait à la fonction ? Comment créer une
*tableau* à taille variable ?

Dis bonjour à malloc et free.

## Malloc

Malloc (**m**emory **alloc**ator) alloue une zone mémoire dynamique appelée la
**heap** dans laquelle tu peux faire ce que bon te semble. Tu peux y accéder
comme un tableau.

Je t'invite à lire le **man 3 malloc**.

```c
void *malloc(size_t size);
```

Malloc renvoie un **pointeur sur void**. Ca veut dire que tu peux créer un
pointeur du type que tu veux. Mais il peut aussi renvoyer **NULL**, qui est un
*alias* sur **(void \*) 0**. C'est un **pointeur sur l'adresse 0**. Cette
adresse est particulière, tu n'as pas le droit de la déréférencer, sinon ton
programme crashera et t'affichera un **segfault**.

Il prend en entrée un **size_t**. C'est un *alias* sur **unsigned int**. cf.
**man 3type size_t**. C'est aussi ce que retourne **strlen**, profitons-en.

C'est le kernel (noyau) de Linux qui s'occupe de te trouver une zone dans ta
mémoire vive qui est libre.

Mettons que tu veuilles créer une zone mémoire pour accueillir une chaîne de
caractères de la taille que tu veux pour copier le contenu de **argv[1]** (le
premier argument de ton programme).

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

char *arg_copy(char *arg_to_copy)
{
    size_t size = strlen(arg_to_copy);
    char *arg = malloc(size + 1);

    if (arg == NULL)
    {
        return NULL;
    }

    for (size_t i = 0; i < size; ++i)
    {
        arg[i] = arg_to_copy[i];
    }

    arg[size] = '\0';

    return arg;
}

int main(int argc, char *argv[])
{
    if (argc != 2)
    {
        printf("Usage: %s ARG\n", argv[0]);
        return 1;
    }

    char *text = arg_copy(argv[1]);
    if (text == NULL)
    {
        printf("malloc failed\n");
        return 2;
    }

    printf("%s\n", text);

    return 0;
}
```

Décortiquons tout ça.

**text** est un pointeur sur char, il faut que ma fonction **arg_copy** retourne
un pointeur sur char. J'envoie en paramètre **argv[1]**.

Dans la fonction **arg_copy**, je crée le pointeur sur char **arg**. Je demande
à malloc de lui allouer la taille de l'entrée **+ 1**. J'ai besoin de ce
caractère en plus pour écrire le caractère de fin de chaîne de caractères :
**\0**.

Admettons que j'envoie **coucou** en entrée. **size** a la valeur de retour de
**strlen("coucou");**, soit 6.

| Index         | 0 | 1 | 2 | 3 | 4 | 5 | 6  |
| -----         | - | - | - | - | - | - | -  |
| Emplacement   | 1 | 2 | 3 | 4 | 5 | 6 | 7  |
| Valeur        | c | o | u | c | o | u | \0 |

Dans ce tableau, la taille **size** est de 6, et le caractère **\0** est au 7ème
emplacement pour indiquer la fin de la chaîne de caractère. D'où l'utilisation
du **+ 1**.

Maintenant que j'ai ma zone mémoire, je vais copier le contenu de
**arg_to_copy** dans cette zone avec une boucle.

L'avant-dernière ligne de la fonction peut être difficile à comprendre. Etant
donné que **size** égale 6, alors **arg[size]** = **arg[6]**. Si tu reprends le
tableau, l'**index** 6 est l'emplacement où doit se trouver le caractère **\0**.

Etant donné que ma boucle s'arrête juste avant de caractère, je l'écris après
les itérations.

J'aurai aussi pu changer la condition de ma boucle ainsi :

```c
for (size_t i = 0; i <= size; ++i)
```

Ce qui fait que **i** aurai atteint la valeur de **size**.

Mais je voulais réappuyer sur l'utilisation des index sur les chaînes de
caractères.

### Segfault

Pour te montrer pourquoi il est important de **tester** les retours de malloc,
tu vas faire un code qui segfault.

```c
#include <stdio.h>
#include <stdlib.h>

void *my_malloc(size_t length)
{
    (void) length;
    return NULL;
}

int main(void)
{
    char *text = my_malloc(10);

    text[0] = 'B';

    return 0;
}
```

```text
$ ./mon_super_programme
Segmentation fault (core dumped)
$
```

Voilà pourquoi il est essentiel de **toujours** vérifier le retour de malloc.
Imagine que tu livres un programme qui crash en production pour une erreur aussi
simple. Quelle honte !

## Free

Une fois que tu n'as plus besoin de ta zone mémoire, il faut la **libérer**.

La mémoire vive de ton PC est limitée. Si tu demandes sans cesse de la mémoire
sans la libérer, tu utiliseras de la mémoire inutilement que d'autres programmes
pourraient utiliser. C'est ce qu'on appelle une fuite mémoire (momory leak).

Imagine qu'à chaque fois que tu ouvres un onglet sur ton navigateur Internet,
celui-ci demande 100 Mo au kernel, mais qu'une fois l'onglet fermé, ton
navigateur ne libère pas les 100 Mo alloués. Si tu cumules les onglets, tu vas
vite te retrouver sans beaucoup de mémoire vive libre. Tu seras obligé de fermer
ton navigateur pour tout libérer.

Pour libérer la mémoire, tu peux faire appel à free. Je t'invite à lire le **man
3 free**.

```c
char *text = malloc(10);

// du code...

free(text);
```

Après l'appel de free, tu ne dois surtout pas réutiliser la variable libérée. Tu
utiliserais une zone mémoire que ton programme considèrerait comme libre de ta
portée et qui pourrait contenir des valeurs allouées par ton programme et pas
par toi. Tes résultats se retrouveraient faussés.

Si on reprend le premier code de cette page, il faut donc ajouter **free** juste
après le **printf** de la fonction **main** qui est le dernier endroit où la
zone mémoire allouée est utilisée.

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

char *arg_copy(char *arg_to_copy)
{
    size_t size = strlen(arg_to_copy);
    char *arg = malloc(size + 1);

    if (arg == NULL)
    {
        return NULL;
    }

    for (size_t i = 0; i < size; ++i)
    {
        arg[i] = arg_to_copy[i];
    }

    arg[size] = '\0';

    return arg;
}

int main(int argc, char *argv[])
{
    if (argc != 2)
    {
        printf("Usage: %s ARG\n", argv[0]);
        return 1;
    }

    char *text = arg_copy(argv[1]);
    if (text == NULL)
    {
        printf("malloc failed\n");
        return 2;
    }

    printf("%s\n", text);

    free(text);

    return 0;
}
```

**Vive la mémoire libre !**

## Sécurité avec free

Pour faire preuve de sécurité quand tu utilises free, tu peux utiliser une
fonction qui va libérer la zone mémoire et mettre l'adresse du pointeur sur
NULL.

free ne laisse ton pointeur sur laquelle il pointe, donc si tu tt'en sers encore
après, tu liras des valeurs qui ne t'appartiennent plus.

```c
char *text = malloc(10);

// du code...

free(text);

printf("%s\n", text);
text[0] = 'g';
printf("%s\n", text);
```

Ce code compile et peut s'exécuter en donnant un comportement indéfini.

Pour ne pas rencontrer ce genre de bug, tu vas créer une fonction qui va libérer
la zone mémoire et mettre le pointeur sur NULL **pour de bon**. Ainsi si tu
utilises ton pointeur, tu auras un segfault. C'est très bien pour des phases de
tests.

```c
#include <stdlib.h>

void ptr_char_destructor(char **ptr)
{
    free(*ptr);
    *ptr = NULL;
}

int main(void)
{
    char *text = malloc(2600);

    // du code

    ptr_char_destructor(&text);

    // du code

    return 0;
}
```

Oulah oulah. Quelle est cette écriture ?

Etant donné que tu dois mettre **pour de bon** le pointeur à NULL, tu vas
coder une fonction qui va utiliser un **pointeur de pointeur**. Un double
pointeur.

Si un pointeur est une adresse qui pointe un type, alors un pointeur de pointeur
est une adresse qui pointe sur... une adresse.

![multi pointeur](./memory/pointer_pointer.png "multi pointeur")

Donc si tu modifies l'adresse pointée en la mettant à NULL, au retour de la
fonction **ptr_char_destructor**, la valeur du pointeur sera toujours à NULL.

Si tu l'utilises sans faire exprès, tu auras un segfault à l'exécution.

Par exemple, ce code segfault :
```c
#include <stdio.h>
#include <stdlib.h>

void ptr_char_destructor(char **ptr)
{
    free(*ptr);
    *ptr = NULL;
}

int main(void)
{
    char *text = malloc(2600);

    // du code

    ptr_char_destructor(&text);

    // du code

    text[0] = 'g';

    return 0;
}
```

## Valgrind

Valgrind (qu'on prononce ["Val grine de"](https://valgrind.org/docs/manual/faq.html#faq.pronounce))
est un outil pour déboguer et profiler tes programmes. Pour l'occasion, tu vas
l'utiliser pour vérifier que tu as bien libérer ta mémoire.

Prenons un simple et incorrect code.

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

char *arg_copy(char *arg_to_copy)
{
    size_t size = strlen(arg_to_copy);
    char *arg = malloc(size + 1);

    if (arg == NULL)
    {
        return NULL;
    }

    for (size_t i = 0; i < size; ++i)
    {
        arg[i] = arg_to_copy[i];
    }

    arg[size] = '\0';

    return arg;
}

int main(int argc, char *argv[])
{
    if (argc != 2)
    {
        printf("Usage: %s ARG\n", argv[0]);
        return 1;
    }

    char *text = arg_copy(argv[1]);
    if (text == NULL)
    {
        printf("malloc failed\n");
        return 2;
    }

    printf("%s\n", text);

    // free(text);

    return 0;
}
```

```text
$ valgrind ./mon_super_programme coucou
==4902== Memcheck, a memory error detector
==4902== Copyright (C) 2002-2024, and GNU GPL'd, by Julian Seward et al.
==4902== Using Valgrind-3.23.0 and LibVEX; rerun with -h for copyright info
==4902== Command: ./mon_super_programme coucou
==4902==
coucou
==4902==
==4902== HEAP SUMMARY:
==4902==     in use at exit: 7 bytes in 1 blocks
==4902==   total heap usage: 2 allocs, 1 frees, 1,031 bytes allocated
==4902==
==4902== LEAK SUMMARY:
==4902==    definitely lost: 7 bytes in 1 blocks
==4902==    indirectly lost: 0 bytes in 0 blocks
==4902==      possibly lost: 0 bytes in 0 blocks
==4902==    still reachable: 0 bytes in 0 blocks
==4902==         suppressed: 0 bytes in 0 blocks
==4902== Rerun with --leak-check=full to see details of leaked memory
==4902==
==4902== For lists of detected and suppressed errors, rerun with: -s
==4902== ERROR SUMMARY: 0 errors from 0 contexts (suppressed: 0 from 0)
```

Décortiquons tout ça.

Tu peux voir au début la commande exécutée.


```text
==4902== Command: ./mon_super_programme coucou
```

Tu peux voir l'effet du **printf** au milieu des lignes.

Ensuite il y a deux parties qui nous résument l'utilisation mémoire.

```text
==4902== HEAP SUMMARY:
==4902==     in use at exit: 7 bytes in 1 blocks
==4902==   total heap usage: 2 allocs, 1 frees, 1,031 bytes allocated
```

**in use at exit: 7 bytes in 1 blocks** : c'est notre **coucou\0** qui n'a pas
été libéré.

**total heap usage: 2 allocs, 1 frees, 1,031 bytes allocated** : la heap est la
zone mémoire dynamique. Comment peut-il y avoir 2 allocations alors que nous ne
faisons appel à malloc qu'une seule fois ?

Parce que nous ne faisons pas appel à malloc qu'une seule fois.

**printf** fait aussi appel à malloc pour afficher le texte. Mais à l'inverse de
notre code, **printf** fait appel à free, c'est pour ça qu'on peut lire ensuite
qu'il y a un appel à free.

A la fin des logs, on nous indique qu'on peut relancer Valgrind avec l'argument
suivant :

```text
==4902== Rerun with --leak-check=full to see details of leaked memory
```

```text
$ valgrind --leak-check=full ./mon_super_programme coucou
==5307== Memcheck, a memory error detector
==5307== Copyright (C) 2002-2024, and GNU GPL'd, by Julian Seward et al.
==5307== Using Valgrind-3.23.0 and LibVEX; rerun with -h for copyright info
==5307== Command: ./mon_super_programme coucou
==5307==
coucou
==5307==
==5307== HEAP SUMMARY:
==5307==     in use at exit: 7 bytes in 1 blocks
==5307==   total heap usage: 2 allocs, 1 frees, 1,031 bytes allocated
==5307==
==5307== 7 bytes in 1 blocks are definitely lost in loss record 1 of 1
==5307==    at 0x48447A8: malloc (vg_replace_malloc.c:446)
==5307==    by 0x109194: arg_copy (in /tmp/tests/pediluve/c/mon_super_programme)
==5307==    by 0x10923B: main (in /tmp/tests/pediluve/c/mon_super_programme)
==5307==
==5307== LEAK SUMMARY:
==5307==    definitely lost: 7 bytes in 1 blocks
==5307==    indirectly lost: 0 bytes in 0 blocks
==5307==      possibly lost: 0 bytes in 0 blocks
==5307==    still reachable: 0 bytes in 0 blocks
==5307==         suppressed: 0 bytes in 0 blocks
==5307==
==5307== For lists of detected and suppressed errors, rerun with: -s
==5307== ERROR SUMMARY: 1 errors from 1 contexts (suppressed: 0 from 0)
```

Le nouveau bloc de texte intéressant se trouve en plein milieu :

```text
==5307== 7 bytes in 1 blocks are definitely lost in loss record 1 of 1
==5307==    at 0x48447A8: malloc (vg_replace_malloc.c:446)
==5307==    by 0x109194: arg_copy (in /tmp/tests/pediluve/c/mon_super_programme)
==5307==    by 0x10923B: main (in /tmp/tests/pediluve/c/mon_super_programme)
```

Ce bloc se lit de bas en haut.

On peut lire que depuis la fonction **main**, on fait appel à la fonction
**arg_copy** qui elle-meme fait appel à la fonction **malloc** et que 7 octets
sont définitivement perdus depuis cet enchainement d'exécution.

Mais les emplacements ne sont pas humainement lisibles, on a des adresses
mémoire en hexadécimal. Nous allons ajouter un argument à la compilation pour
avoir des **symboles de débug**.

```text
$ gcc -g test.c -o mon_super_programme
```

L'option **-g** permet d'ajouter des symboles de débug à ton programme. Ca te
permet de déboguer plus efficacement tes programmes. Mais attention à ne pas
livrer en production ce que tu produis avec des informations. Des gens mal
intentionnés pourraient s'en servir.

```text
$ valgrind --leak-check=full ./mon_super_programme coucou
...
==5550== 7 bytes in 1 blocks are definitely lost in loss record 1 of 1
==5550==    at 0x48447A8: malloc (vg_replace_malloc.c:446)
==5550==    by 0x109194: arg_copy (test.c:8)
==5550==    by 0x10923B: main (test.c:33)
...
$
```

On peut lire ici que le premier appel à **arg_copy** se fait dans la fonction
**main** à la ligne 33, et que **arg_copy** fait appel à **malloc** ligne 8.

On sait où se trouve notre memory leak !

### Recoder malloc et free

Nous n'allons pas faire ça ici, mais dans les écoles d'informatiques, il y a un
exercice assez répandu qui est de recoder et remplacer malloc et free. C'est un
exercice ma foi fort sympathique.
