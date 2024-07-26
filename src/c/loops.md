# Boucles

Les boucles sont un moyen de répéter du code autant de fois que nécessaire.

## while

La boucle while exécute du code tant que la condition est **Vraie**.

```c
#include <stdio.h>

int main(void)
{
    int i = 0;

    while (i < 10)
    {
        printf("%d\n", i);
        ++i;
    }

    return 0;
}
```

```text
$ ./mon_super_programme
0
1
2
3
4
5
6
7
8
9
$
```

Si la condition est tout de suite **Fausse**, alors la boucle ne sera **jamais**
exécutée.

```c
#include <stdio.h>

int main(void)
{
    int i = 10;

    while (i < 10)
    {
        printf("%d\n", i);
        ++i;
    }

    return 0;
}
```

```text
$ ./mon_super_programme
$
```

## do while

**do while** est une boucle qui va exécuter **au moins une fois** le code de la
boucle.

```c
#include <stdio.h>

int main(void)
{
    int i = 0;

    do
    {
        printf("%d\n", i);
        ++i;
    } while (i < 10);

    return 0;
}
```

Note le point-virgule ';' à la toute fin de la ligne avec le **while**.

```text
$ ./mon_super_programme
0
1
2
3
4
5
6
7
8
9
$
```

Le code sera **toujours** exécuté au moins une fois.

```c
#include <stdio.h>

int main(void)
{
    int i = 10;

    do
    {
        printf("%d\n", i);
        ++i;
    } while (i < 10);

    return 0;
}
```

```text
$ ./mon_super_programme
10
$
```

## for

Une boucle **for** est séparée en trois instructions.

* **INITIALISATION** qui est exécutée une seule fois au tout début de la boucle
* **CONDITION** qui est testée à chaque itération
* **INSTRUCTION** qui est exécutée à chaque itération après le test de la condition, sauf la première fois


```c
for (INITIALISATION; CONDITION; INSTRUCTION)
{
    // Le code
}
```

Note qu'il y a une séparation avec des point-virgules ';'.

```c
#include <stdio.h>

int main(void)
{
    for (int i = 0; i < 10; ++i)
    {
        printf("%d\n", i);
    }

    return 0;
}
```

```text
$ ./mon_super_programme
0
1
2
3
4
5
6
7
8
9
$
```


Tu peux aussi t'en servir pour **parcourir** les chaînes de caractères.

```c
#include <stdio.h>

int my_strlen(char *str)
{
    int result = 0;
    for (int i = 0; str[i] != '\0'; ++i)
    {
        ++result;
    }

    return result;
}

int main(void)
{
    char *ptr = "coucou les loulous";
    int ptr_size = my_strlen(ptr);

    printf("Longueur de '%s' = %d\n", ptr, ptr_size);

    return 0;
}
```

```text
$ ./mon_super_programme
Longueur de 'coucou les loulous' = 18
$
```

Ici tu recodes la fonction **strlen** qui retourne le nombre de caractères dans
une chaîne de caractères.

Je t'invite à lire **man 3 strlen**.
