# Exercices

Voici une liste d'exercices pour t'entrainer sur tout ce que tu as vu.

Les corrections sont au prochain chapitre.

## Fonctions simples

Ecris le code des fonctions suivantes pour additionner, soustraire, multiplier
et diviser des entiers ensemble.

Attention, si tu viens à diviser par 0, retourne 0.

```c
int addition(int a, int b);

int substraction(int a, int b);

int multiplication(int a, int b);

int divide(int a, int b);
```

Ecris le code des fonctions and, or, xor, not qui retournent les opérations
bitwises correspondantes.

```c
int and(int a, int b);

int or(int a, int b);

int xor(int a, int b);

int not(int a);
```

Ecris le code qui retourne le double, le carré et le cube d'un entier.

```c
int double_int(int a);

int square(int a);

int cube(int a);
```

Ecris le code qui retourne la valeur de 2<sup>n</sup>. Indice pour être efficace 
: utilise le shifting.

```c
int power_of_two(unsigned int n);
```

Ecris le code de la fonction **int_len** qui retourne le nombre de caractères
utilisés pour **afficher** un entier.

* Si n vaut 0 :  retourne 1
* Si n vaut -1 : retourne 2
* Si n vaut 1 : retourne 1
* Si n vaut 2600 : retourne 4
* Si n vaut -42 : retourne 3
* etc.

```c
int int_len(n);
```

Ecris le code des fonctions

**is_lowercase** qui retourne 1 si le caractère envoyé est une lettre de
l'alphabet en minuscule, 0 sinon.

**is_uppercase** qui retourne 1 si le caractère envoyé est une lettre de
l'alphabet en majuscule, 0 sinon.

**is_num** qui retourne 1 si le caractère envoyé est un caractère qui représente
un chiffre compris entre 0 et 9, 0 sinon.

Regarde bien le man ascii et réfléchis à comment tester si c'est bien dans la
partie minuscule, majuscule ou numérique.

```c
int is_lowercase(char c);
int is_uppercase(char c);
int is_num(char c);
```

Ecris le code de la fonction **is_alphanum** qui retourne 1 si le caractère en
paramètre correspond à une lettre de l'alphabet en minuscule, ou un chiffre
compris entre 0 et 9, 0 sinon.

Tu peux tout à fait appeller les 3 dernières fonctions depuis la fonction
**is_alphanum**, pense à bien les écrire **au dessus** de la fonction
**is_alphanum**.

```c
int is_lowercase(char c)
{
    // Le code
}

int is_uppercase(char c)
{
    // Le code
}

int is_num(char c)
{
    // Le code
}

int is_alphanum(char c)
{
    // Le code
}
```

Ecris la fonction **graduate** qui :

* Affiche "Mauvais" si la note est comprise dans l'intervalle [0;8]
* Affiche "Moyen" si la note est comprise dans l'intervalle [9;12]
* Affiche "Bien" si la note est comprise dans l'intervalle [13;16]
* Affiche "Très bien" si la note est comprise dans l'intervalle [17;19]
* Affiche "Parfait" si la note est à 20
* Affiche "Quoi ?" si la note n'est pas comprise dans l'intervalle [0;20]

```c
void graduate(int n);
```

## Notions de pointeurs

Ecris le code de la fonction **moyenne** qui renvoie la moyenne de 3 floats en
les remettant à 0 **dans** la fonction.

Une moyenne sur 42 éléments se calcule ainsi : (valeur_1 + valeur 2 + ... +
valeur_42) / 42

```c
float moyenne(float *a, float *b, float *c);
```

Ecris le code de la fonction **odd_even** qui affiche :

* C'est pair : Si la valeur pointée est paire
* C'est impair : Si la valeur pointée est impair

```c
void odd_even(int *value);
```

Ecris le code **swap** qui échange les valeurs pointées de deux pointeurs.

Si tu y arrives, fais le sans créer de variable dans la fonction. Sinon, ce
n'est pas grace, ça sera déjà bien !

```c
void swap(int *a, int *b)
{
    // Le code
}

int main(void)
{
    int a = 42;
    int b = 2600;

    printf("a = %d | b =  %d\n"); // a = 42 | b = 2600
    swap(&a, &b);
    printf("a = %d | b =  %d\n"); // a = 2600 | b = 42

    return 0;
}
```

## Chaînes de caractères

Ecris le code de la fonction **strlen** qui renvoie le nombre de caractères dans
une chaîne de caractères

```c
unsigned int strlen(char *s);
```

Ecris le code de la fonction **upper** qui prend un tableau de caractères en
entrée et qui change les caractères minuscules en caractères majuscules.

Ecris le code de la fonction **lower** qui prend un tableau de caractères en
entrée et qui change les caractères majuscules en caractères minuscules.

Tu peux tout à fait utiliser les fonctions **uppercase** et **lowercase**.

```c
int uppercase(char c)
{
    // Le code
}

int lowercase(char c)
{
    // Le code
}

void upper(char *str)
{
    // Le code
}

void lower(char *str)
{
    // Le code
}

int main(void)
{
    char str[] = "J'aImE b3AuC0uP l3 PeDiLuvE";

    printf("%s\n", str); // "J'aImE b3AuC0uP l3 PeDiLuvE";

    upper(str);

    printf("%s\n", str); // "J'AIME B3AUC0UP L3 PEDILUVE";

    lower(str);

    printf("%s\n", str); // "j'aime b3auc0up l3 pediluve";

    return 0;
}
```

Ecris le code de la fonction **vowels** qui retourne le nombre de voyelles
présentes dans une chaîne de caractères.

```c
int vowels(char *str);
```

Ecris le code de la fonction **miniatoi** qui retourne l'entier représenté sous
chaînes de caractères. Dès que tu rencontres un caractère qui n'est pas
numérique, retourne ce que tu as déjà calculé.

* Si str vaut "0", retourne 0
* Si str vaut "2", retourne 2
* Si str vaut "-42", retourne -42
* Si str vaut "2600", retourne 2600
* Si str vaut "pediluve", retourne 0
* Si str vaut "pediluve666", retourne 0
* Si str vaut "69pediluve777", retourne 69
* Si str vaut "-pediluve7", retourne 0

Tu peux utiliser la fonction **is_num** que tu as écris plus tôt.

```c
int miniatoi(char *str);
```

Avec ça tu as déjà quelques exercices pour apprendre à faire un peu de C et être
à l'aise pour la suite des évènements.
