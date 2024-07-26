# Flags de compilation

Depuis le début, tu compiles ton code en appelant gcc sur ton fichier source et
le nom du binaire qu'il doit crée, sans aucune autre information.

Tu peux donner des paramètres à gcc pour orienter la compilation.

Voici les paramètres que tu devrais utiliser pour valider avec brio les codes
que tu envoies êtres testés :

* -std=c99 : Utilise le C version 99. Si tu ne suis pas la norme, tu auras un message d'avertissement (warning).
* -pedantic : Utilise la norme ISO du C. Si tu ne suis pas la norme, tu auras un message d'avertissement.
* -Wall : Active beaucoup de warnings.
* -Wextra : Active encore plus de warnings.
* -Werror : Transforme les warnings en erreurs.
* -Wvla : Interdit les tableaux à taille variable.

Un warning permet la compilation, le compilateur t'informe qu'il *peut* y avoir
un comportement indéfini à l'exécution.

Une erreur interdit la compilation. Ainsi si tu as ne serait-ce que le moindre
petit warning, la compilation échouera.

Voici comment compiler avec les flags de compilation présentés.

```text
$ gcc -std=c99 -pedantic -Wall -Wextra -Werror -Wvla test.c -o mon_super_programme
```

Voici un code qui comporte des warnings et erreurs avec les flags de
compilation.

```c
#include <stdlib.h>

void mystery(int *i)
{
    int j = *i * 42;
    *i += j;
}

int main(int argc, char *argv[])
{
    int i;
    int j = i + 1;
    int k = atoi(argv[1]);
    int array[k];
    printf("Coucou\n");

    mystery(&i);

    printf("%u\n", i);
}
```
```text
$ gcc -Wall -Wextra -Wvla -Werror -std=c99 -pedantic test.c -o mon_super_programme
test.c: In function ‘main’:
test.c:14:5: error: ISO C90 forbids variable length array ‘array’ [-Werror=vla]
   14 |     int array[k];
      |     ^~~
test.c:15:5: error: implicit declaration of function ‘printf’ [-Wimplicit-function-declaration]
   15 |     printf("Coucou\n");
      |     ^~~~~~
test.c:2:1: note: include ‘<stdio.h>’ or provide a declaration of ‘printf’
    1 | #include <stdlib.h>
  +++ |+#include <stdio.h>
    2 |
test.c:15:5: error: incompatible implicit declaration of built-in function ‘printf’ [-Werror=builtin-declaration-mismatch]
   15 |     printf("Coucou\n");
      |     ^~~~~~
test.c:15:5: note: include ‘<stdio.h>’ or provide a declaration of ‘printf’
test.c:14:9: error: unused variable ‘array’ [-Werror=unused-variable]
   14 |     int array[k];
      |         ^~~~~
test.c:12:9: error: unused variable ‘j’ [-Werror=unused-variable]
   12 |     int j = i + 1;
      |         ^
test.c:9:14: error: unused parameter ‘argc’ [-Werror=unused-parameter]
    9 | int main(int argc, char *argv[])
      |          ~~~~^~~~
cc1: all warnings being treated as errors
$
```

Ca fait peur hein ? Il suffit pourtant de lire les messages d'erreurs.

```text
test.c:14:5: error: ISO C90 forbids variable length array ‘array’ [-Werror=vla]
   14 |     int array[k];
      |     ^~~
```

Tu crées une tableau dont la taille ne peut être calculé à la compilation.
Comment savoir quelle place prendre en mémoire ? C'est interdit, tu dois définir
une taille fixe pour la compilation, pas l'exécution.

```text
test.c:15:5: error: implicit declaration of function ‘printf’ [-Wimplicit-function-declaration]
   15 |     printf("Coucou\n");
      |     ^~~~~~
test.c:2:1: note: include ‘<stdio.h>’ or provide a declaration of ‘printf’
    1 | #include <stdlib.h>
  +++ |+#include <stdio.h>
    2 |

```

Tu appelles printf sans inclure stdio.h. Lis bien le message, il te dit même à
quelle ligne inclure le fichier.

```text
test.c:12:9: error: unused variable ‘j’ [-Werror=unused-variable]
   12 |     int j = i + 1;
      |         ^
```

Tu crées une variable sans l'utiliser, quelle inutilité !

Si tu es entrain de créer du code que tu veux tester avec des variables pas
encore utilisées, tu peux faire ça :

```c
int i = 0;
int j = i + 1;

(void) j;

fonction(&i);
```

L'instruction ligne 4 ne fait strictement rien avec j. Mais ne rien faire, c'est
déjà faire quelque chose.


Pareil avec **argc**.
