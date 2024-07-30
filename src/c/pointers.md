# Pointeurs

Il est dit par certains que la notion de pointeur est ce qu'il y a de plus
difficile à comprendre en C. Aussi, tu vas répéter avec moi ces quelques
phrases.

**Un pointeur est une adresse.**

**Un pointeur est une adresse.**

**Un pointeur est une adresse.**

Et pour être un peu plus correct.

**Un pointeur est une adresse sur un type.**

**Un pointeur est une adresse sur un type.**

**Un pointeur est une adresse sur un type.**

Voilà. Maintenant tu vas voir, les pointeurs, c'est pas si terrible.

## Mémoire

Il faut comprendre que quand tu exécutes ton programme, il est copié dans la RAM
de ton PC. Tout est dans une **mémoire virtuelle**. Qui va de 0 à 2<sup>64</sup>.

La mémoire fonctionne comme un tableau. Il y a l'adresse 0, puis 1, puis 2, ...

Et dans ces cases mémoires, se trouvent tout ton programme, avec les valeurs de
tes variables.

## Initialiser un pointeur à zéro

Avant d'utiliser un pointeur, tu vas voir comment initialiser unpointeur *à
zéro*.

Pour cela, tu vas lui affecter la valeur **NULL**. C'est un *alias* sur un
pointeur sur void à la valeur 0. C'est à dire (void *)0.

```c
int *ptr = NULL;
```

Voilà, si tu ne sais pas encore où pointera ton pointeur, par sécurité, met le à
NULL.

## Afficher l'adresse d'une variable

Pour afficher l'adresse d'une variable, on va utiliser l'opérateur **&**.

```c
#include <stdio.h>

int main(void)
{
    int value = 42;
    void *addr_value = &value;

    printf("Adresse de value = %p\n", addr_value);

    return 0;
}
```

```text
$ ./mon_super_programme
Adresse de value = 0x7ffd2cd0df1c
$
```

Comme tu peux le voir, le pointeur **addr_value** a comme valeur une adresse.

**Un pointeur est une adresse.**

Une valeur qui commence par **0x** est de l'hexadécimal.

Tu auras très probablement une autre valeur affichée. D'ailleurs chaque
exécution *devrait* t'afficher une valeur différente (c'est une sécurité mise en
place par Linux).

## Déréférencement

C'est là où ça devient difficile.

Rappelle toi : **Un pointeur est une adresse sur un type.**

Reprenons le code précédent, je vais le modifier un peu. Le code précédent
servait à avoir l'adresse de **value**, ici je vais avoir un pointeur sur le
**type** int pour récupérer sa valeur autrement que par **value**.

```c
#include <stdio.h>

int main(void)
{
    int value = 42;
    int *ptr_value = &value;

    return 0;
}
```

**value** est une variable qui vaut 42. Cette variable a une valeur enregistrée
dans une adresse.

**addr_value** est un pointeur. Sa valeur est une adresse, celle où se trouve la
valeur de **value**.

Pour pouvoir accéder à la case mémoire qui contient **42** depuis un pointeur,
il faut le déréférencer.

Rappelle toi, la mémoire fonctionne **comme un tableau**.

Un pointeur sur un int, tu peux le voir comme un tableau de int à un élément.

Tu peux donc utiliser ptr_value[0] pour accéder à la valeur 42.

```c
#include <stdio.h>

int main(void)
{
    int value = 42;
    int *ptr_value = &value;

    printf("Valeur de value = %d\n", ptr_value[0]);

    return 0;
}
```

```text
$ ./mon_super_programme
Valeur de value = 42
$
```

### Encore du sucre syntaxique

Tu verras dans d'autres cours que pour déréférencer un pointeur, il faut
utiliser, avec mon exemple, l'écriture suivant : **\*ptr_value**

```c
#include <stdio.h>

int main(void)
{
    int value = 42;
    int *ptr_value = &value;

    printf("Valeur de value = %d\n", *ptr_value);

    return 0;
}
```
Le code est exactement le même. Parce que l'utilisation des crochets pour
l'accès tableau est du sucre syntaxique.

En réalite, quand tu écris **array[0]**, la mémoire utilise cette notation :
**\*(array + 0))** qui est la même chose que **\*array**

Et quand tu écris **array[1]**, la mémoire utilise cette notation :
**\*(array + 1))** 

Et quand tu écris **array[2]**, la mémoire utilise cette notation :
**\*(array + 2))** 

etc.

L'opérateur \* sert à déréférencer un pointeur pour accéder à la case mémoire
vers laquelle il pointe.

On peut ainsi **modifier** la valeur d'une variable depuis un pointeur.

```c
#include <stdio.h>

int main(void)
{
    int value = 42;
    int *ptr_value = &value;

    *ptr_value = 2600; // Equivalent à "ptr_value[0] = 2600;"

    printf("Valeur de value = %d\n", *ptr_value);

    return 0;
}
```

```text
$ ./mon_super_programme
Valeur de value = 2600
$
```

Bon c'est bien, mais c'est quoi l'utilité réelle des pointeurs ?

## L'utilité des pointeurs

Tu peux utiliser les pointeurs pour changer la valeur d'une ou plusieurs
variables dans une autre fonction.

Quand tu envoies une variable en paramètre d'une fonction, tu envoies en réalité
une copie locale. Si tu modifies la variable dans la fonction appelée, elle
reviendra à sa valeur d'origine dans la fonction appelante.

```c
#include <stdio.h>

void example(int value)
{
    value = 2600;
    printf("Valeur de value = %d\n", value);
}

int main(void)
{
    int value = 42;
    printf("Valeur de value = %d\n", value);

    example(value);

    printf("Valeur de value = %d\n", value);

    return 0;
}
```

```text
$ ./mon_super_programme
Valeur de value = 42
Valeur de value = 2600
Valeur de value = 42
$
```

Utilise la notion de pointeur pour modifier la valeur de value dans la fonction
example.

```c
#include <stdio.h>

void example(int *value)
{
    *value = 2600;
    printf("Valeur de value = %d\n", *value);
}

int main(void)
{
    int value = 42;
    printf("Valeur de value = %d\n", value);

    example(&value);

    printf("Valeur de value = %d\n", value);

    return 0;
}
```

```text
$ ./mon_super_programme
Valeur de value = 42
Valeur de value = 2600
Valeur de value = 2600
$
```

## Pointeurs sur caractères

Voilà donc ce qu'il se cache derrière les pointeurs sur caractères. Au lieu de
n'avoir qu'une valeur en mémoire de type char, il y a plusieurs valeurs de type
char en mémoire les unes à la suite des autres, accessibles avec les crochets du
tableau.

```c
char *ptr_char = "vive le c";
char array_char[] = "vive linux";
```

Le premier **v** de chaque chaînes de caractères est enregistré quelque part en
mémoire, et les autres lettres qui suivent sont à la suite dans la mémoire. On
utilise la notion de pointeurs pour accéder à ses valeurs.

La différence, c'est qu'un tableau possède une taille fixe en mémoire, alors
qu'un pointeur fait 8 octets, car il ne pointe que sur une valeur. Il peut
accéder aux prochaines valeurs comme un tableau mais est défini autrement en
mémoire.

## Arithmétique des pointeurs, 1ere partie

Tu peux changer la valeur d'un pointeur et te déplacer vers la suite de la
chaine.

Pour ça, il suffit d'incrémenter le pointeur.

```c
char *str = "Encore des pointeurs";

printf("%c\n", *str); // => 'E'

str = str + 1;

printf("%c\n", *str); // => 'n'
```
