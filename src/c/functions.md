# Fonctions

Une fonction est un bout de code que tu peux appeler quand tu veux.

Une fonction possède un identifiant (un nom), un type de retour et une entrée
pour des paramètres. C'est ce qu'on appelle la **signature**.

Voici comment définir une fonction et sa **portée** (la zone qui délimite le
début et la fin du code qui sera exécuté).

Les variables déclarées et définies dans une fonction ne sont vivantes que
pendant l'exécution de cette fonction. Au **retour** d'une fonction, toutes les
variables disparaissent.

```c
type identifiant(type_param1 param1, type_param2 param2)
{
}
```

Tu n'es pas obligé de mettre des paramètres ou de valeurs de retour. Tu peux
utiliser le type **void** pour ça.

```c

// Ne retourne rien et ne prend rien en entrée
void fonction_1(void)
{
}

// Retourne un float et ne prend rien en entrée
float fonction_2(void)
{
}

// Ne retourne rien et prend un entier en entrée
void fonction_3(int entier)
{
}

// Retourne un caractère et prend 1 float et 1 caractère en entrée
char fonction_4(float flottant, char caractere)
{
}
```

Comme avec la fonction main, il ne te reste plus qu'à mettre le code entre les
accolades.

Attention, si tu veux créer une fonction, pour le moment écrit la au dessus de
la fonction main.

Le compilateur est un outil puissant mais pas très intelligent. Si ta fonction
main appelle la fonction **fonction_1**, elle doit être **définie** au dessus de
la fonction main pour qu'il sache qu'elle existe déjà. Si elle est en dessous,
il te dira qu'il ne trouve pas ta fonction. Le compilateur lit un code source
comme nous : de gauche à droite de haut en bas.

Crée une fonction qui prend deux entiers en entrée et retourne l'addition des
deux.

```c
#include <stdio.h>

int addition(int a, int b)
{
    return a + b;
}

int main(void)
{
    int val_1 = 42;
    int val_2 = 51;
    int result = addition(val_1, val_2);

    printf("result = %d\n", result);

    return 0;
}
```

Bravo ! Tu viens de créer ta première fonction. Quelle fierté. Tant d'autres
t'attendent déjà.

Le positionnement des variables est important. **val_1** enverra sa valeur à
**a** et **val_2** enverra sa valeur à **b**.

Il faut que les variables que tu envoies soient du même type. Si j'avais défini
**val_1** comme étant un **float**, mon code aurait été faux.


Petit exercice pratique : Crée 4 fonctions pour les 4 opérations mathémathiques
que tu as appris plus jeune : addition, soustraction, multiplication et
division.

Voici une correction... sera t-il parfaite ?

```c
int addition(int a, int b)
{
    return a + b;
}

int soustraction(int a, int b)
{
    return a - b;
}

int multiplication(int a, int b)
{
    return a * b;
}

int division(int a, int b)
{
    return a / b;
}
```

Penses-tu que tout fonctionne correctement avec ce que tu connais des
mathématiques ?

Il y a une *petite* erreur : si tu envoies **0** en deuxième paramètre à la
fonction **division**, il y aura une **division par 0**.

Voici une correction possible : si b vaut 0, alors on retourne 0.

```c
int division(int a, int b)
{
    if (b == 0)
    {
        return 0;
    }

    return a / b;
}
```

Pour tester une égalité, tu dois utiliser la double égalité '=='. Avant que tu
n'essaies, non, ça ne fonctionne pas avec les chaines de caractères. Mais ça
fonctionne sur les caractères uniques.

Tu verras plus tard comment agrémenter ton code de tests et conditions.

### Quitter une fonction qui ne renvoie rien

Si tu fois quitter une fonction qui ne renvoie rien (void), tu peux utiliser le
mot-clé **return** seul.

```c
void positive_printer(int n)
{
    if (n < 0)
    {
        return;
    }

    printf("n: %d\n");
}
```
