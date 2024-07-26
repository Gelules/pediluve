# Structures de données

Tu as vu comment utiliser les types prédéfinis par le langage C, mais le C te
permet de créer tes propres structures et quelque part tes propres types.

Il existe différents moyens de *créer ses propres types*, tels que les
**struct**, les **enum** et les **unions**.

Pour le Pédiluve, tu ne vas que voir les **struct**.

Une structure est une collection de différents types. Ca ne fonctionne pas tout
à fait comme un tableau car tu peux accéder aux attributs par leurs noms.

```c
#include <stdio.h>

struct player
{
    char *name;
    int level;
    float mana;
};

int main(void)
{
    struct player p;

    p.name = "gelules";
    p.level = 42;
    p.mana = 2600,6951;

    printf("Player:\n");
    printf("Name: %s\nLevel: %d\nMana: %f\n", p.name, p.level, p.mana);

    return 0;
}
```

Et voilà, tu peux définir des structures qui collectionnent des types
différents.

## Par pointeurs

L'accès aux structures par pointeurs est différent des accès aux tableaux. Quand
c'est une variable locale comme dans le code ci-dessus, tu accès aux attributs
par un point '.'. Quand c'est par pointeur, il faut une flèche '->'.

On va coder les fonctions **player_create** et **player_print**.

**player_create** prend un pointeur vers une **structure player** pour la
remplir avec les paramètres restants.

**player_print** affiche les attributs.

```c
#include <stdio.h>

struct player
{
    char *name;
    int level;
    float mana;
};

void player_create(struct player *p, char *name, int level, float mana)
{
    p->name = name;
    p->level = level;
    p->mana = mana;
}

void player_print(struct player *p)
{
    printf("Name: %s\n", p->name);
    printf("Level: %d\n", p->level);
    printf("Mana: %f\n", p->mana);
}

int main(void)
{
    struct player p;

    player_create(&p, "gelules", 42, 2600.6951);

    player_print(&p);

    return 0;
}
```

Tu peux aussi créer une structure en une seule instruction ainsi :

```c
#include <stdio.h>

struct player
{
    char *name;
    int level;
    float mana;
};

void player_print(struct player *p)
{
    printf("Name: %s\n", p->name);
    printf("Level: %d\n", p->level);
    printf("Mana: %f\n", p->mana);
}

int main(void)
{
    struct player p = {.name = "gelules",
                       .level = 42,
                       .mana = 2600.6951};

    player_print(&p);

    return 0;
}
```

Il n'y a même pas besoin de suivre l'ordre des attributs.

Tu peux voir la taille qu'utilise une structure en mémoire avec sizeof.

```c
struct player
{
    char *name;
    int level;
    float mana;
};

unsigned long int size = sizeof (struct player);

printf("sizeof (struct player): %lu\n", size);
```
