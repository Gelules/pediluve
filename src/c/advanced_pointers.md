# Pointeurs avancés

Plus tôt, je t'ai dis qu'on pouvait incrémenter un pointeur pour avancer dans un
tableau. Mais comment penses-tu que cela se passe en mémoire ?

Prends deux tableaux de types différents.

```c
char ptr_c[] = "abcdefghijklmnopqrstuvwxyz";
double ptr_d[26] = { 0 };
```

Maintenant tu vas créer les deux **pointeurs** pour avancer en mémoire, et les
deux **pointeurs sur void** correspondants pour avoir leurs adresses.

```c
char array_c[] = "abcdefghijklmnopqrstuvwxyz";
double array_d[26] = { 0 };
char *ptr_c = array_c;
double *ptr_d = array_d;
void *addr_c = ptr_c;
void *addr_d = ptr_d;

```

Pas besoin d'utiliser l'esperluette '&' pour avoir l'adresse, un tableau agit
déjà comme un pointeur, sa valeur est donc déjà une adresse.

Fais quelques affichages.

```c
char array_c[] = "abcdefghijklmnopqrstuvwxyz";
double array_d[26] = { 0 };
char *ptr_c = array_c;
double *ptr_d = array_d;
void *addr_c = ptr_c;
void *addr_d = ptr_d;

printf("addr ptr_c: %p with value %c\n", addr_c, *ptr_c);
printf("addr ptr_d: %p with value %lf\n", addr_d, *ptr_d);

ptr_c = ptr_c + 1;
++ptr_d;
addr_c = ptr_c;
addr_d = ptr_d;

printf("addr ptr_c: %p with value %c\n", addr_c, *ptr_c);
printf("addr ptr_d: %p with value %lf\n", addr_d, *ptr_d);

++ptr_c;
++ptr_d;
addr_c = ptr_c;
addr_d = ptr_d;

printf("addr ptr_c: %p with value %c\n", addr_c, *ptr_c);
printf("addr ptr_d: %p with value %lf\n", addr_d, *ptr_d);
```
```text
$ ./mon_super_programme
addr ptr_c: 0x7ffccc171530 with value a
addr ptr_d: 0x7ffccc171460 with value 0.000000
addr ptr_c: 0x7ffccc171531 with value b
addr ptr_d: 0x7ffccc171468 with value 0.000000
addr ptr_c: 0x7ffccc171532 with value c
addr ptr_d: 0x7ffccc171470 with value 0.000000
$
```

Comme tu peux le voir, le pointeur vers caractère avance de 1 en 1, tandis que
le pointeur vers double avance de 8 en 8 (rappelle toi on est en hexadécimal,
0x8 + 0x8 = 0x10)

Pourquoi ? Parce qu'un caractère prend 1 octet en mémoire et un double prend 8
octets en mémoire, le pointeur va donc avancer d'autant d'octets.

Imagine avoir un tableau de **struct player** assez large.

```c
#include <stdio.h>

struct player
{
    char *name;
    int level;
    double mana;
    int x;
    int y;
    int z;
    char *weapon;
};

int main(void)
{
    unsigned long int size = sizeof (struct player);
    struct player players[16];
    struct player *p = players;
    void *addr_p = p;

    printf("sizeof (struct player): %lu\n", size);

    for (int i = 0; i < 16; ++i)
    {
        addr_p = p + i;
        printf("addr of p[%d]: %p\n", i, addr_p);
    }
}
```

```text
$ $ ./mon_super_programme
sizeof (struct player): 48
addr of p[0]: 0x7fffebaf2210
addr of p[1]: 0x7fffebaf2240
addr of p[2]: 0x7fffebaf2270
addr of p[3]: 0x7fffebaf22a0
addr of p[4]: 0x7fffebaf22d0
addr of p[5]: 0x7fffebaf2300
addr of p[6]: 0x7fffebaf2330
addr of p[7]: 0x7fffebaf2360
addr of p[8]: 0x7fffebaf2390
addr of p[9]: 0x7fffebaf23c0
addr of p[10]: 0x7fffebaf23f0
addr of p[11]: 0x7fffebaf2420
addr of p[12]: 0x7fffebaf2450
addr of p[13]: 0x7fffebaf2480
addr of p[14]: 0x7fffebaf24b0
addr of p[15]: 0x7fffebaf24e0
$
```

Comme tu peux le voir, le tableau de struct avance de 0x30 en 0x30, donc de 48
octets en 48 octets.
