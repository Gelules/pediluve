# Mathématiques

Tu viens de voir précédemment comment faire des opérations arithématiques
simples avec l'addition, la soustraction, la multiplication et la division. Mais
il reste quelques particularité à découvrir.

## Modulo

Tu vas vu la division, mais tu n'as pas encore vu le reste de la division.

Tu dois utiliser le caractère **%**.

```c
int valeur = 666;
int diviseur = 111;
int reste = valeur % diviseur;

printf("reste de %d par %d = %d%d\n", valeur, diviseur, reste);
```

### Parité

Si tu veux savoir si un nombre est pair ou impair, tu peux vérifier le reste de
la division par 2. S'il reste 0 alors le nombre est pair, s'il reste 1, alors
le nombre est impair.

```c
int pair = 10;
int impair = 11;

int reste = pair % 2;
printf("%d\n", reste);

reste = impair % 2;
printf("%d\n", reste);
```

## Sucre syntaxique

Pour ajouter une valeur à une variable en C, tu serais très tenté de l'écrire de
cette façon :

```c
int i = 0;

// Du code...

i = i + 1;
```

Mais tu peux l'écrire plus rapidement de cette façon :

```c
int i = 0;

// Du code...

i += 1; // => i = i + 1
```

Ca revient à la même chose. Tu peux évidemment mettre un autre signe que le
signe '+' et n'importe quelle expression à droite du égal.

Si tu veux par exemple diviser une valeur par 10 :

```c
int valeur = 5467;

// Du code

valeur /= 10; // => valeur = valeur / 10
```

C'est ce qu'on appelle du sucre syntaxique. La syntaxe est adoucit pour la
rendre plus agréable.

## pré-incrémentation et post-incrémentation

Tu peux écrire encore plus rapidement une incrémentation en C avec l'opérateur
**++**.

```c
int i = 0;

// Du code

i++; // => i = i + 1

// Du code

++i; // => i = i + 1
```

Il y a cependant une différence entre les deux.

La première forme, i++, est une pré-incrémentation. Une autre variable peut
récupérer la valeur de **i** avant que **i** ne s'incrémente.

La deuxième forme, ++i, est une post-incrémentation. **i** va s'incrémenter et
**après** ça, une autre variable peut récupérer la nouvelle valeur de **i**.

Voici un exemple :

```c
int i = 10;

printf("i: %d\n", i);

int j = i++; // => j = 10 ; i = 11

printf("i: %d | j = %d\n", i, j);

int k = ++i; // => k = 12 ; i = 12

printf("i: %d | k = %d\n", i, k);
```

Tu peux faire la même logique avec l'opérateur de soustraction '-'.

## Bitwise

### Logic bit

En plus de faire des opérations sur les variables, tu peux faire des opérations
directement sur leurs bits.

Voici les portes logiques que tu connais en C :

* ~ : NOT
* & : AND
* | : OR
* ^ : XOR

```c
int maximum = ~0; // => NOT(00000000000000000000000000000000) =  11111111111111111111111111111111 = 4294967295

int op_and = 42 & 51; //       101010
                      // AND
                      //       110011
                      //       ======
                      //       100010 = 34
printf("op_and = %d\n", op_and);

int op_or = 42 | 51; //        101010
                     // OR
                     //        110011
                     //        ======
                     //        111011 = 51
printf("op_or = %d\n", op_or);

int op_xor = 42 ^ 51; //       101010
                      // XOR
                      //       110011
                      //       ======
                      //       011001 = 25
printf("op_xor = %d\n", op_xor);
```

### Shifting

Tu peux aussi décaler des bits sur la gauche et sur la droite.

Prenons la valeur 42 en binaire, codée sur un int (4 octets, donc 32 bits).

```text
00000000000000000000000000101010
```

Avec les opérateurs **<<** et **>>**, je peux décaler les bits sur la gauche et
sur la droite. Attention si un bit disparaît d'un côté, il ne réapparait pas de
l'autre.

```c
int valeur = 42;      // valeur = 00000000000000000000000000101010 = 42

valeur = valeur << 1; // valeur = 00000000000000000000000001010100 = 84

valeur = valeur << 2; // valeur = 00000000000000000000000101010000 = 336

valeur = valeur >> 5; // valeur = 00000000000000000000000000001010 = 10

valeur = valeur << 1; // valeur = 00000000000000000000000000010100 = 20
```

Tu peux aussi écrire ces instructions de ces façons :

```c
valeur <<= 2;
valeur >>= 2;
```

## L'inverseur logique

Il existe un deuxième opérateur d'inversion en C qui est le point d'exclamation
'!'. Celui-ci n'inverse pas les valeurs des bits mais la **véracité** d'une
variable.

En C, la valeur 0 vaut **Faux** et n'importe quelle autre valeur vaut **Vrai**.
C'est exactement l'inverse du shell.

Voici comment l'utiliser :

```c
int zero = 0;
int one = 1;
int two = 2;

zero = !zero; // => zero = 1
one = !one;   // => one = 0
two = !two;   // => two = 0

zero = !zero; // => zero = 0
one = !one;   // => one = 1
two = !two;   // => two = 1
```
