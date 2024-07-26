# Tableaux

Un tableau est une collection de valeurs du même type. On peut accéder aux
éléments par des index.

Un tableau se crée ainsi :
```text
type nom_tableau[nombre_elements] = { valeur_1, valeur_2, valeur_3 };
```

On peut mettre autant d'éléments que l'on veut.

## Tableaux de types simples

Pour créer un tableau d'entiers, de floats ou de char, il suffit de remplir le
tableau avec les bonnes valeurs.

```c
int variable = 666;
int levels[6] = {0, 1, -1, 2600, variable, 42 };

char alpha[3] = {'x', 'y', 'z'};
```

Pour accéder à un élément du tableau, il suffit d'utiliser cette notation :

```c
element = array[index];
```

A savoir : l'index commence **toujours** à 0.

Ainsi si je reprends le tableaux levels, il faut le lire avec les index suivants
:

| Index  | 0 | 1 | 2  | 3    | 4   | 5  |
| -----  | - | - | -- | ---- | --- | -- |
| Valeur | 0 | 1 | -1 | 2600 | 666 | 42 |


Ainsi, pour accéder à un élémeent d'un tableau de type **int** :

```c
int levels[6] = {0, 1, -1, 2600, variable, 42 };

int level = levels[2]; // => level = -1

levels[0] = 21; // array = 21 1 -1 2600 666 42
```

Attention à ne pas utiliser un index plus grand que le nombre d'éléments dans le
tableau. Si tu dépasses, tu récupéreras une valeur ailleurs en mémoire, que tu
ne contrôles pas.

#### Tableau à zéro

Si tu veux remplir une partie du tableau et laisser le reste à 0 ou même
l'initialiser complètement à 0, tu n'es pas obligé de tout définir, le
compilateur va pour toi mettre la partie non définie à 0.

```c
int array_1[10] = { 1, 1, 1 }; // => 1 1 1 0 0 0 0 0 0 0
int array_2[10] = { 0 }; // => 0 0 0 0 0 0 0 0 0 0
```

#### Nombre d'éléments calculé à la compilation

Si tu ne sais pas combien d'éléments ton tableau va recevoir, tu n'es pas obligé
de mettre une taille, le compilateur comptera le nombre d'éléments que tu as
écrit entre les accolades.

```c
int array[] = { 1, 2, 3, 4, 5 }; // => 5 éléments
```

### Taille d'un tableau

Pour avoir la taille utilisée par un tableau en mémoire, tu peux utiliser
l'opérateur que tu connais, **sizeof**.

A ton avis, combien d'octets prend en mémoire un tableau de type **int** à
**10** éléments ?

Si un **int** utilise 4 octets, alors 10 **int** vont en utiliser 10 fois plus,
donc 40 octets.

```c
int array[10] = { 0 };
int size = sizeof (array);

printf("size of array: %lu\n", size);
```

### Nombre d'éléments dans un tableau

Pour savoir le nombre d'éléments dans un tableau sans compter un par un, on peut
utiliser **sizeof**.

```c
int array[] = { beaucoup mais alors vraiment beaucoup de valeurs };

int nbr_elements = sizeof (array) / sizeof (array[0]);
```

Que fait-on exactement ?

**sizeof (array)** donne la taille du tableau en octets

**sizeof (array[0])** donne la taille d'un élément du tableau en octets

Si on divise la taille totale par la taille d'un élément, nous avons bien le
nombre d'éléments dans un tableau.

On utilise **array[0]** car on ne sait pas combien d'éléments a le tableau, mais
étant donné qu'il doit en avoir au moins 1, on utilise tout simpelemnt le
premier qui est obligatoirement existant.

## Tableaux pour chaines de caractères

Je t'avais dis que pour faire une chaîne de caractères, tu devais écrire :

```c
char *text = "salut les loulous";
```

et que cette chaîne de caractères est constante et que tu ne peux pas la
modifier.

Tu peux utiliser la notation de tableau pour avoir une chaîne de caractères que
tu peux modifier.

```c
char text[] = "salut les poutous";
printf("%s\n", text);
text[10] = 'l';
text[13] = 'l';
printf("%s\n", text);
```
