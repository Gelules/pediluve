# Structures de contrôles

Faire du code, c'est bien. Faire du code qui n'exécute pas toujours la même
chose, c'est mieux.

Tu vas apprendre ici à créer des conditions en C.

## if else

Le C n'a que deux mot-clés pour créer des conditions, là où le shell en a trois.

Le mot-clé **if** prend en compte une condition, le mot-clé **else** n'en prend
pas **sauf** s'il est suivi d'un **if**, ce qui donne la construction **else
if**.

Tu ne peux pas facilement faire des comparaisons de chaines de caractères comme
en shell, en C tout se fait avec des entiers. Mais tu peux tester des chaines de
caractères avec des fonctions de la bibliothèque C qui vont retourner des
entiers pour dire **Vrai** ou **Faux**.

### Entiers

Pour tester des entiers, tu peux utiliser les opérateurs :

* < : strictement inférieur
* <= : inférieur ou égal
* == : égal
* != : différent
* \>= : supérieur ou égal
* \> : strictement supérieur

```c
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
    int secret = 42;
    int guess = atoi(argv[1]);

    if (guess < secret)
    {
        printf("Plus grand\n");
    }
    else if (guess > secret)
    {
        printf("Plus petit");
    }
    else // Si ce n'est ni plus petit ni plus grand, alors c'est égal
    {
        printf("Bien deviné !");
    }

    return !(guess == secret);
}
```

La dernière ligne doit être décortiquée.

```c
(guess == secret)
```

retourne 1 si c'est **Vrai** et 0 si c'est **Faux**.

L'opérateur d'inversion '!' va inverser la valeur logique.

```c
// Dans le cas où guess == secret

!(guess == secret) // => !(1)
!(1) // => 0

// Dans le cas où guess != secret
!(guess != secret) // => !(0)
!(0) // => 1
```

Pourquoi faire ça ?

Parce qu'en shell, 0 est Vrai et autre chose que 0 est Faux. Donc pour garder
une cohérence avec le shell qui va recevoir la valeur de retour de ton
programme, j'ai besoin que l'exit status soit à 0 si le nombre deviné est bon et
que l'exit status soit à 1 si le nombre deviné n'est pas le bon.

### Chaines de caractères

Si tu veux tester deux chaines de caractères, tu peux utiliser la fonction
**strcmp**. Je t'invite à lire le man de cette fonction **man 3 strcmp**,
spécialement la fin du manuel ;)

Elle prend deux chaines de caractères en paramètres, retourne 0 si les deux sont
égales, une valeur négative si la première chaine de caractères est
**alphabétiquement** plus petite que la deuxième, une valeur positive dans le
cas inverse.

L'ordre alphabétique est basée sur la table ASCII que tu as vu précédemment.

Ainsi

```c
char *s1 = "a";
char *s2 = "B";
```

s2 est plus petit que s1, car dans la table ASCII, 'B' vient avant 'a'.


```c
#include <stdio.h>
#include <string.h>

int main(int argc, char *argv[])
{
    char *secret = "pediluve";
    char *guess = argv[1];
    int result = strmpc(guess, secret);

    if (result != 0)
    {
        printf("Mauvais mot de passe\n");
    }
    else
    {
        printf("Bon mot de passe\n");
    }

    return result;
}
```

Attention, rappelle toi quand même qu'en shell, l'exit status va de 0 à 255, si
tu retournes une valeur négative, elle sera transformée en une autre valeur.

## switch

Pour éviter de faire des **if else** à rallonge, tu peux tester une variable sur
un **switch** et faire un code beaucoup plus élégant et agréable à lire.

```c
#include <stdio.h>
#include <stdlib.h>

// Ici un ensemble de fonctions

int main(int argc, char *argv[])
{
    int choice = atoi(argv[1]);

    switch (choice)
    {
        case -1:
            printf("En route pour le donjon :\n");
            dungeon();
            break;
        case 0:
            printf("Vous êtes déjà dans le lobby\n");
            break;
        case 1:
            printf("En route pour la tour !\n");
            tower();
            break;
        case 666:
            printf("En route pour le boss\n");
            boss();
            break;
        default:
            printf("Je ne peux accéder à votre requête\n");
    }

    return 0;
}
```

Tu peux voir que c'est beaucoup plus lisible qu'un enchaînement de **if else**.

Le mot-clé **break** sert à partir du **switch** si un des cas était **Vrai** et
pour éviter de tester les autres cas suivants.

Le mot-clé **default** agit comme un **else**, si tous les cas précédents
étaient faux, alors le code de **default** sera exécuté.
