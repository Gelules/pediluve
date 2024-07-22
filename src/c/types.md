# Types prédéfinis

## Types

Tu as déjà joué avec deux types depuis le début du chapitre en C : les entiers
et les pointeurs sur caractères.

Voici une liste de types que tu peux créer, je vais aussi te montrer les codes à
utiliser pour les afficher avec printf.

Tu peux retrouver les informations des codes à utiliser dans **man 3 printf**.

### Entiers

Les entiers se reconnaissent avec l'utilisation du type **int**. Mais tu peux
ajouter des qualificateurs pour changer la façon de les utiliser.

```c
#include <stdio.h>

int main(void)
{
    // Peut être négatif et positif
    int entier_simple = -42;
    printf("entier_simple = %d\n", entier_simple);

    // Ne peut pas être négatif
    unsigned int entier_non_signe = 333;
    printf("entier_simple = %u\n", entier_non_signe);

    // Ne peut pas avoir une grande taille
    short int petit = 32767;
    printf("petit = %d\n", petit);
    petit = petit + 1;
    printf("petit = %d\n", petit);

    long int large = 2000000000; // 2 milliards
    printf("large = %ld\n", large);

    long long int tres_large = 30000000000; // 30 milliards
    printf("tres_large = %lld\n", tres_large);

    return 0;
}
```

Je te laisse essayer ce code. Il n'est pas exhaustif sur les combinaisons
possibes sur les entiers qu'on peut créer.

Décortiquons tout ça.

La variable **entier_simple** est un entier tout ce qu'il y a de plus simple.
Elle peut aller dans le négatif et le positif.

La variable **entier_non_signe** ne peut pas avoir de signe négatif. Elle sera
toujours strictement positive. La différence avec **entier_simple** est qu'elle
peut avoir une valeur positive deux fois plus grande, mais en contrepartie elle
ne peut peut pas être négative.

Que s'est-il passé avec la variable **petit** ? Le qualificateur **short**
informe que la variable a une petite taille en mémoire, elle peut aller de
-32768 à 32767. Si elle dépasse 32767, elle revient à la valeur la plus petite
qu'elle peut prendre. On appelle ça un **overflow**.

Les variables **large** et **tres_large** peuvent avoir des valeurs énormes.

Tu peux ajouter **unsigned** avec tous les qualificateurs que tu viens de voir.
Ils pourront avoir une valeur positive deux fois plus grande que les variables
implicitement **signed** mais ne pourront jamais avoir une valeur négative.

Voici un tableau des types d'entiers que tu peux avoir, la place qu'ils prennent
en mémoire et leurs limites.

| Nom                       | Octets | Valeurs                                    |
| ------------------------- | ------ | ------------------------                   |
| short int                 | 2      | -32768 à 32767                             |
| unsigned short int        | 2      | 0 à 65535                                  |
| int                       | 4      | -2147483648 à 2147483647                   |
| unsigned int              | 4      | 0 à 4294967295                             |
| long int                  | 8      | -9223372036854775808 à 9223372036854775807 |
| unsigned long int         | 8      | 0 à 18446744073709551615                   |
| long long int             | 8      | -9223372036854775808 à 9223372036854775807 |
| unsigned long long int    | 8      | 0 à 18446744073709551615                   |

S'il n'y a pas de différence entre **long int** et **long long int**, c'est parce
que les architectures actuelles sont des architectures 64 bits. Juste avant
notre ère actuelle, les ordinateurs étaient sur des architectures 32 bits, et
les types en C étaient bien différents.

L'architecture que j'utilise est de l'Intel 64 bits. Mais par exemple Apple qui
a une autre architecture aura peut-être des valeurs différentes.

Pour calculer combien de nombres tu peux avoir avec un type, prends sa taille en
mémoire (sous la colonne **Octets** du tableau), multiplie la par 8. Pourquoi ?
Rappelle toi du chapitre [bits et octets](../preliminaires/bit_byte.html). Un
octet et constitué de 8 bits.

Maintenant que tu as multiplié par 8, pose cette valeur en puissance de 2.

Par exemple, le **short int** prend 2 octets en mémoire, donc 16 bits.

\\[ 2 ^\{16} = 65536 \\]

Tu as donc 65536 nombres possibles avec un **short int**. C'est pour ça que
**signé** tu as la moitié de cette valeur disponible en négatif et pareil en
positif.

Pour le formatage avec **printf**, tu dois utiliser **%d** pour les entiers
signés et **%u** pour les entiers non signés.

Tu dois ajouter **l** pour un **long** et **ll** pour un **long long**. Selon le
système sur lequel tu te trouves, vérifie toujours la taille en octet des types
prédéfinis. Je te montre à la fin de ce chapitre comment faire ça.

### Décimales

Tu peux également utiliser des variables à décimales. Tu en as deux : **float**
et **double**.

Sur mon architecture, **float** prend 4 octets en mémoire et **double** prend 8
octets. On dit que **double** a une précision double.

```c
#include <stdio.h>

int main(void)
{
    float f =  1.234567891011121314;
    double d = 1.234567891011121314;
    long double ld = 1.234567891011121314;

    printf("f  = %.15f\n", f);
    printf("d  = %.15lf\n", d);
    printf("ld = %.15Lf\n", ld);

    return 0;
}
```

Ici, je veux te faire comprendre la différence entre **float** et **double**.

**float** a une précision de 7 chiffres après la virgule, là où **double** a une
précision de 15 chiffres après la virgule.

Dans le printf, j'utilise la notation **%.15f** pour demander à printf de
m'afficher 15 chiffres après la virgule, même à **float**.

Comme tu peux le voir, au bout de quelques chiffres, la valeur affichée n'est
pas du tout la même que celle affectée dans le code.

Voici un tableau récapitulatif sur l'utilisation de float et double.

| Nom           | Octets |
| --------------| ------ |
| float         | 4      |
| double        | 8      |
| long double   | 16     |


Si **long double** peut prendre 128 bis même sur une architecture 64 bits, c'est
parce qu'une partie est utilisée pour la précision, c'est à dire le nombre de
chiffres possible derrière la virgule.

### Caractère

Il existe un type pour les caractères : **char**.

Tu peux l'utiliser comme un entier pour avancer dans l'alphabet.

```c
#include <stdio.h>

int main(void)
{
    char alpha = 'a'; // Des simple quotes, surtout pas des double quotes !
    printf("alpha = %c\n", alpha);
    printf("alpha = %d\n", alpha);
    alpha = alpha + 1;
    printf("alpha = %c\n", alpha);
    printf("alpha = %d\n", alpha);

    return 0;
}
```

Je vais devoir expliquer ce qu'il se passe ici un peu plus en détail.

```text
$ gcc test.c -o mon_super_programme
$ ./mon_super_programme
alpha = a
alpha = 97
alpha = b
alpha = 98
$
```

le caractère 'a' est codé sur la valeur 97. Où trouver cette information ?

Dans le **man ascii**.

```text
Oct   Dec   Hex   Char                        Oct   Dec   Hex   Char
────────────────────────────────────────────────────────────────────────
000   0     00    NUL '\0' (null character)   100   64    40    @
001   1     01    SOH (start of heading)      101   65    41    A
002   2     02    STX (start of text)         102   66    42    B
003   3     03    ETX (end of text)           103   67    43    C
004   4     04    EOT (end of transmission)   104   68    44    D
005   5     05    ENQ (enquiry)               105   69    45    E
006   6     06    ACK (acknowledge)           106   70    46    F
007   7     07    BEL '\a' (bell)             107   71    47    G
010   8     08    BS  '\b' (backspace)        110   72    48    H
011   9     09    HT  '\t' (horizontal tab)   111   73    49    I
012   10    0A    LF  '\n' (new line)         112   74    4A    J
013   11    0B    VT  '\v' (vertical tab)     113   75    4B    K
014   12    0C    FF  '\f' (form feed)        114   76    4C    L
015   13    0D    CR  '\r' (carriage ret)     115   77    4D    M
016   14    0E    SO  (shift out)             116   78    4E    N
017   15    0F    SI  (shift in)              117   79    4F    O
020   16    10    DLE (data link escape)      120   80    50    P
021   17    11    DC1 (device control 1)      121   81    51    Q
022   18    12    DC2 (device control 2)      122   82    52    R
023   19    13    DC3 (device control 3)      123   83    53    S
024   20    14    DC4 (device control 4)      124   84    54    T
025   21    15    NAK (negative ack.)         125   85    55    U
026   22    16    SYN (synchronous idle)      126   86    56    V
027   23    17    ETB (end of trans. blk)     127   87    57    W
030   24    18    CAN (cancel)                130   88    58    X
031   25    19    EM  (end of medium)         131   89    59    Y
032   26    1A    SUB (substitute)            132   90    5A    Z
033   27    1B    ESC (escape)                133   91    5B    [
034   28    1C    FS  (file separator)        134   92    5C    \  '\\'
035   29    1D    GS  (group separator)       135   93    5D    ]
036   30    1E    RS  (record separator)      136   94    5E    ^
037   31    1F    US  (unit separator)        137   95    5F    _
040   32    20    SPACE                       140   96    60    `
041   33    21    !                           141   97    61    a
042   34    22    "                           142   98    62    b
043   35    23    #                           143   99    63    c
044   36    24    $                           144   100   64    d
045   37    25    %                           145   101   65    e
046   38    26    &                           146   102   66    f
047   39    27    '                           147   103   67    g
050   40    28    (                           150   104   68    h
051   41    29    )                           151   105   69    i
052   42    2A    *                           152   106   6A    j
053   43    2B    +                           153   107   6B    k
054   44    2C    ,                           154   108   6C    l
055   45    2D    -                           155   109   6D    m
056   46    2E    .                           156   110   6E    n
057   47    2F    /                           157   111   6F    o
060   48    30    0                           160   112   70    p
061   49    31    1                           161   113   71    q
062   50    32    2                           162   114   72    r
063   51    33    3                           163   115   73    s
064   52    34    4                           164   116   74    t
065   53    35    5                           165   117   75    u
066   54    36    6                           166   118   76    v
067   55    37    7                           167   119   77    w
070   56    38    8                           170   120   78    x
071   57    39    9                           171   121   79    y
072   58    3A    :                           172   122   7A    z
073   59    3B    ;                           173   123   7B    {
074   60    3C    <                           174   124   7C    |
075   61    3D    =                           175   125   7D    }
076   62    3E    >                           176   126   7E    ~
077   63    3F    ?                         │ 177   127   7F    DEL
```

La première colonne est la valeur en **octal** (base 8), la deuxième en base 10,
la troisième en base 16 et enfin la dernière le caractère codé derrière ces
valeurs.

Tu peux retrouver le 'a' minuscule à la valeur 97.

Retiens bien ça, ça sera très important pour la suite de ton cursus.

| Nom           | Octets | Valeurs      |
| ------------- | ------ | ------------ |
| char          | 1      | -128 à 127   |
| unsigned char | 1      | 0 à 255      |


### Void

**void** est un type particulier qui signifie **pas de type**. Il n'a pas de
taille.

Tu verras plus tard comment il est utilisé.


#### sizeof

Pour avoir la taille d'un type, tu peux utiliser la macro **sizeof**. Elle te
donne en octet la taille prise par le type donné en paramètre. Pour information,
sizeof renvoie un **long unsigned int**.

```c
#include <stdio.h>

int main(void)
{
    printf("sizeof (char): %lu\n", sizeof (char));
    printf("sizeof (char*): %lu\n", sizeof (char*));

    printf("sizeof (int): %lu\n", sizeof (int));
    printf("sizeof (int*): %lu\n", sizeof (int*));
    printf("sizeof (short int): %lu\n", sizeof (short int));
    printf("sizeof (long int): %lu\n", sizeof (long int));
    printf("sizeof (long long int): %lu\n", sizeof (long long int));
    printf("sizeof (long long int*): %lu\n", sizeof (long long int*));

    printf("sizeof (float): %lu\n", sizeof (float));
    printf("sizeof (float*): %lu\n", sizeof (float*));

    printf("sizeof (double): %lu\n", sizeof (double));
    printf("sizeof (long double): %lu\n", sizeof (long double));
    printf("sizeof (long double*): %lu\n", sizeof (long double*));

    printf("sizeof (void*): %lu\n", sizeof (void*));

    return 0;
}
```

```text
$ gcc test.c -o mon_super_programme
$ ./mon_super_programme
sizeof (char): 1
sizeof (char*): 8
sizeof (int): 4
sizeof (int*): 8
sizeof (short int): 2
sizeof (long int): 8
sizeof (long long int): 8
sizeof (long long int*): 8
sizeof (float): 4
sizeof (float*): 8
sizeof (double): 8
sizeof (long double): 16
sizeof (long double*): 8
sizeof (void*): 8
$
```

Les valeurs avec des étoiles '\*' sont ce qu'on appelle des **pointeurs**. Tu
verras ce que c'est plus tard. Sache qu'un pointeur fait **toujours** 8 octets.

## Chaines de caractères

Je ne vais pas encore détailler ce qu'est une chaine de caractères, mais je vais
te montrer comment en créer que tu puisses jouer avec.

```c
char *string = "My name Lules. Gé Lules";

printf("string: %s\n", string);
```

Comme tu peux le voir, ça utilise le mot-clé **char** de caractère, mais avec
l'utilisation d'un pointeur en plus. Et tu dois définir ta chaine de caractères
entre guillements.

Sache juste que tu ne peux pas modifier les chaines de caractères définies de
cette manière. Tu verras comment réellement jouer avec plus tard.
