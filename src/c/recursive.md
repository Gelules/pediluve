# Récursivité

Avais-tu pensé à appeler la fonction dans laquelle tu étais ?

Voici un exemple :

```c
unsigned int mystery(unsigned int n)
{
    if (n == 0)
        return n;

    return mystery(n - 1) + n;
}
```

Arrives-tu à déterminer ce que fait cette fonction ?

Elle somme l'ensemble des nombres dans l'intervalle [0;n].

En effet, la fonction va sans cesse se rappeler en décrémentant n de 1 jusqu'à
arriver à 0.

Tu verras pendant ta Piscine d'autres cas d'utilisation de la récursivité. Sache
que c'est utile pour résoudre des problèmes en découpant le problème en
sous-problème et en itérant dessus.
