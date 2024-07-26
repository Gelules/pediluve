# Plusieurs fichiers

Depuis le début, tu compiles un seul et unique fichier. Mais un programme ce
n'est pas qu'un seul fichier. C'est une multitude de fichiers compilés ensemble.

Pour la ligne de commande, c'est simple, il suffit d'ajouter le nom de test
fichiers.

Tu as créer un fichier test.c avec le **main** et un fichier math.c avec les
fonctions **addition** et **soustraction** que tu connais si bien maintenant.

```c
// test.c

#include <stdio.h>

int main(void)
{
    int a = 42;
    int b = 2600;
    int result = addition(a, b);

    printf("result: %d\n", result);

    return 0;
}
```

```c
/// math.c

int addition(int a, int b)
{
    return a + b;
}

int soustraction(int a, int b)
{
    return a - b;
}
```

Compile.

```text
$ gcc test.c math.c -o mon_super_programme
test.c: In function ‘main’:
test.c:9:18: error: implicit declaration of function ‘addition’ [-Wimplicit-function-declaration]
    9 |     int result = addition(a, b);
      |
```

Bigre, la fonction main ne trouve pas la fonction addition. Pourtant le fichier
est bien dans la compilation.

C'est parce que le compilateur ne fonctionne pas comme ça. C'est moche, mais tu
ne vas pas voir ça maintenant, mais pendant ta Piscine.

Il faut indiquer à la fonction main que tes fonctions de maths existent, et ça
dans le fichier test.c

Tu vas **déclarer** les fonctions.

Déclarer signifie que tu indiques au compilateur qu'il existe des fonctions avec
un identifiant, des paramètres et un type de sortie.

Définir signifie créer le code des fonctions déclarées.

Ca fonctionne aussi pour des variables. Tu peux définir **i** ainsi :

```c
int i;
```

et le définir avec le symbole d'égalité.

```c
i = 0;

// ou directement le définir en le déclarant

int i = 0;
```

Tu vas d'abord créer ton premier fichier header, que tu vas appeler **math.h**.

```c
#ifndef MATH_H
#define MATH_H

int addition(int a, int b);
int soustraction(int a, int b);

#endif /* !MATH_H */
```

Ne fais pas attention aux code avec **ifndef**, **define** et **endif**. Ils
sont là pour éviter des redéfinitions de code. Tu sauras aussi ce que c'est
pendant ta Piscine.

Ce que tu fais ici, c'est annoncer qu'il existe, quelque part, des fonctions
**addition** et **soustraction**. **addition** prend 2 int en paramètres et
retourne 1 int. Pareil pour **soustraction**.

Tu vas maintenant informer **test.c** que ces fonctions existent.

```c
// test.c

#include <stdio.h>

#include "math.h"

int main(void)
{
    int a = 42;
    int b = 2600;
    int result = addition(a, b);

    printf("result: %d\n", result);

    return 0;
}
```

Vois-tu la différence entre une bibliothèque installée dans le système et une
bibliothèque locale ?

Celle dans le système est inclue avec des chevrons '<' et '>' tandis que la
bibliothèque locale est inclue par des guillements '"'.

Egalement, ce sont dans ces fichiers que tu dois initialiser tes structures.

Recompile.

```text
$ gcc test.c math.c -o mon_super_programme
$
```

Et voilà, à partir de maintenant, tu peux créer des programmes qui utilisent
plusieurs fichiers.
