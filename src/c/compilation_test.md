# Compilation de test

Le langage C est un langage **compilé**. A l'inverse du shell, tu ne vas pas
exécuter du C comme tu l'écris. Tu vas utiliser un **compilateur** pour
transformer ton code course en **langage machine**.

Tu vas pour ce cours faire tes codes de test dans un seul et unique fichier que
tu vas appeler **test.c**. Ton compilateur est **gcc**. Installe le si tu ne
l'as pas.

```text
$ which gcc
/usr/bin/gcc
$
```

Voici le fichier le plus petit que tu peux utiliser pour faire du C.

```c
int main(void)
{
    return 0;
}
```

Tu peux écrire ton code entre les accolades pour commencer.

Pour compiler et essayer ton programme, voici la commande à utiliser :
```text
$ gcc test.c -o mon_super_programme
$ ./mon_super_programme
$
```

Sache que tu peux commenter ton code pour le documenter et décrire que tu fais.
Il existe deux types de commentaire. Les singie lines et les multilines.

```c
/* Cette fonction main
ne prend rien en entrée et ne fait que
retourner 0 */

int main(void)
{
    // retourne 0 en exit status;
    return 0;
}
```

Voilà, tu es prêt pour la suite.
