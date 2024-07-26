# Corrections

## Fonctions simples

```c
int addition(int a, int b)
{
    return a + b;
}

int substraction(int a, int b)
{
    return a - b;
}

int multiplication(int a, int b)
{
    return a * b;
}

int divide(int a, int b)
{
    if (b == 0)
    {
        return 0;
    }

    return a / b;
}

int and(int a, int b)
{
    return a & b;
}

int or(int a, int b)
{
    return a | b;
}

int xor(int a, int b)
{
    return a ^ b;
}

int not(int a)
{
    return ~a;
}

int double_int(int a)
{
    return a + a;
}

int square(int a)
{
    return a * a;
}

int cube(int a)
{
    return a * a * a;
}

int power_of_two(unsigned int n)
{
    return 1 << n;
}
```

```c
int int_len(n)
{
    int result = 0;
    int sign = (n < 0);

    while (n != 0)
    {
        n = n / 10;
        ++result;
    }

    return result + sign;
}
```

```c
int is_lowercase(char c)
{
    return ('a' <= c && c <= 'z');
}

int is_uppercase(char c);
{
    return ('A' <= c && c <= 'Z');
}

int is_num(char c);
{
    return ('0' <= c && c <= '9');
}

int is_alphanum(char c)
{
    return (is_lowercase(c) || is_uppercase(c) || is_num(c));
}
```

```c
void graduate(int n)
{
    if (0 <= n && n <= 8)
    {
        printf("Mauvais\n");
    }
    else if (9 <= n && n <= 12)
    {
        printf("Moyen\n");
    }
    else if (13 <= n && n <= 16)
    {
        printf("Bien\n");
    }
    else if (17 <= n && n <= 19)
    {
        printf("Très bien\n");
    }
    else if (n == 20)
    {
        printf("Parfait\n")
    }
    else
    {
        printf("Quoi ?\n");
    }
}
```

## Notions de pointeurs

```c
float moyenne(float *a, float *b, float *c)
{
    float result = (*a + *b + *c) / 3

    *a = 0;
    *b = 0;
    *c = 0;

    return result;
}
```

```c
void odd_even(int *value)
{
    if (*value % 2 == 0)
    {
        printf("C'est pair\n");
    }
    else
    {
        printf("C'est impair");
    }
}
```

```c
void swap(int *a, int *b)
{
    int tempo = *a;
    *a = *b;
    *b = tempo;
}

// Ou alors en mode bitwise expert sans avoir à créer une variable temporaire

void swap(int *a, int *b)
{
    *a = *a ^ *b;
    *b = *a ^ *b;
    *a = *a ^ *b;
}
```

## Chaînes de caractères

```c
int strlen(char *s)
{
    int result = 0;
    for (int i = 0; s[i] != '\0'; ++i)
    {
        ++result;
    }

    return result;
}
```

```c
void upper(char *str)
{
    for (int i = 0; str[i] != '\0'; ++i)
    {
        if (is_uppercase(str[i])
        {
            str[i] = str[i] + 32;
        }
    }
}

void lower(char *str)
{
    for (int i = 0; str[i] != '\0'; ++i)
    {
        if (is_lowercase(str[i])
        {
            str[i] = str[i] - 32;
        }
    }

}
```

Pourquoi addition ou soustraire par 32 ?

Si tu regardes le **man ascii**, tu peux voir que la lettre majuscule 'A' a la
valeur 65 et que la lettre minuscule 'a' a la valeur 97. La différence entre 65
et 97 est 32. En additionant ou soustrayant par 32, on peut passer de
l'intervalle minuscule à majuscule et inversement.

```c
int vowels(char *str)
{
    int result = 0;}

    for (int i = 0; str[i] != '\0'; ++i)
    {
        if (str[i] == 'a' || str[i] == 'e' || str[i] == 'i' || str[i] == 'o' || str[i] == 'u' || str[i] == 'y')
        {
            ++result;
        }
    }

    return result;
}
```

```c
int is_num(char c);
{
    if ('0' <= c && c <= '9')
    {
        return 1;
    }

    return 0;
}

int miniatoi(char *str)
{
    int result = 0;
    int sign = 1;

    if (str[0] == '-')
    {
        sign = -1;
        ++str;
    }

    for (int i = 0; str[i] != '\0'; ++i)
    {
        if (is_num(str[i]))
        {
            result = result * 10;
            result = str[i] - '0';
        }
        else
        {
            break;
        }
    }

    return result * sign;
}
```

Décortiquons.

La variable **result** est créée en étant multipliée par 10 petit à petit puis 
on retourne le résultat multiplié par **1** ou **-1**.

Si j'envoie "1234", la variable **result** sera égale aux valeurs suivantes :
* 0     // ligne 13 et ligne 27
* 1     // ligne 28
* 10    // ligne 27
* 12    // ligne 28
* 120   // ligne 27
* 123   // ligne 28
* 1230  // ligne 27
* 1234  // ligne 28

Enfin, on retourne le résultat multiplié par **1** ou **-1**.

\\[ 1234 * 1 = 1234 \\]

Si j'envoie "-1234", on retient que le signe est négatif et on avance le
pointeur après le signe '-'. On refait les mêmes caluls et on retourne 1234
multiplié par -1.

\\[ 1234 * -1 = -1234 \\]
