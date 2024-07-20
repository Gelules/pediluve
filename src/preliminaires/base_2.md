# Franklin savait compter deux par deux

## De la base 10 à la base 2

[Cours vidéo](https://www.youtube.com/watch?v=bg8eyeYF7lw)

Maintenant que tu as compris comment décomposer un nombre en base 10, tu vas
apprendre à transformer un nombre écrit en base 10 en base 2 et inversement.

Pour rappel, la base 2 a deux chiffres : 0 et 1.

Prends ce tableau en référence

| Indice   | 10              | 9          | 8          | 7          | 6          | 5          | 4          | 3          | 2          | 1          | 0          |
| ------   | --------------- | ---------- | ---------- | ---------- | ---------- | ---------- | ---------- | ---------- | ---------- | ---------- | ---------- |
| Notation | \\[ 2^{10} \\]  | \\[ 2^9\\] | \\[ 2^8\\] | \\[ 2^7\\] | \\[ 2^6\\] | \\[ 2^5\\] | \\[ 2^4\\] | \\[ 2^3\\] | \\[ 2^2\\] | \\[ 2^1\\] | \\[ 2^0\\] |
| Valeur   | 1024            | 512        | 256        | 128        | 64         | 32         | 16         | 8          | 4          | 2          | 1          |

La base 2 ne fait que se multiplier par 2 à chaque nouvel indice.

Le tableau va jusqu'à 1024 car c'est le strict minimum à connaître par coeur.

Prends un nombre, complètement au hasard : 651.

Tu vas le soustraire par la puissance de 2 inférieure ou égale la plus proche.

Reprends le tableau.
La puissance de 2 inférieure ou égale la plus proche de 651 est... 512.

\\[ 651 - 512 = 139\\]

Tu as **1** fois 512 dans ton nombre de départ, reporte le chiffre 1 sous 512.

| Indice   | 10              | 9          | 8          | 7          | 6          | 5          | 4          | 3          | 2          | 1          | 0          |
| ------   | --------------- | ---------- | ---------- | ---------- | ---------- | ---------- | ---------- | ---------- | ---------- | ---------- | ---------- |
| Notation | \\[ 2^{10} \\]  | \\[ 2^9\\] | \\[ 2^8\\] | \\[ 2^7\\] | \\[ 2^6\\] | \\[ 2^5\\] | \\[ 2^4\\] | \\[ 2^3\\] | \\[ 2^2\\] | \\[ 2^1\\] | \\[ 2^0\\] |
| Valeur   | 1024            | 512        | 256        | 128        | 64         | 32         | 16         | 8          | 4          | 2          | 1          |
| Nombre   |                 | 1          |            |            |            |            |            |            |            |            |            |

Recommence avec le nouveau nombre qui est 139.
La puissance de 2 inférieure ou égale la plus proche de 139 est... 128.
Tu as **1** fois 128 dans ton nouveau nombre, reporte le chiffre 1 sous 128.

\\[ 139 - 128 = 11 \\]

| Indice   | 10              | 9          | 8          | 7          | 6          | 5          | 4          | 3          | 2          | 1          | 0          |
| ------   | --------------- | ---------- | ---------- | ---------- | ---------- | ---------- | ---------- | ---------- | ---------- | ---------- | ---------- |
| Notation | \\[ 2^{10} \\]  | \\[ 2^9\\] | \\[ 2^8\\] | \\[ 2^7\\] | \\[ 2^6\\] | \\[ 2^5\\] | \\[ 2^4\\] | \\[ 2^3\\] | \\[ 2^2\\] | \\[ 2^1\\] | \\[ 2^0\\] |
| Valeur   | 1024            | 512        | 256        | 128        | 64         | 32         | 16         | 8          | 4          | 2          | 1          |
| Nombre   |                 | 1          |            | 1          |            |            |            |            |            |            |            |

Recommence avec le nouveau nombre qui est 11.
La puissance de 2 inférieure ou égale la plus proche de 11 est... 8.
Tu as **1** fois 8 dans ton nouveau nombre, reporte le chiffre 1 sous 8.

\\[ 11 - 8 = 3 \\]

| Indice   | 10              | 9          | 8          | 7          | 6          | 5          | 4          | 3          | 2          | 1          | 0          |
| ------   | --------------- | ---------- | ---------- | ---------- | ---------- | ---------- | ---------- | ---------- | ---------- | ---------- | ---------- |
| Notation | \\[ 2^{10} \\]  | \\[ 2^9\\] | \\[ 2^8\\] | \\[ 2^7\\] | \\[ 2^6\\] | \\[ 2^5\\] | \\[ 2^4\\] | \\[ 2^3\\] | \\[ 2^2\\] | \\[ 2^1\\] | \\[ 2^0\\] |
| Valeur   | 1024            | 512        | 256        | 128        | 64         | 32         | 16         | 8          | 4          | 2          | 1          |
| Nombre   |                 | 1          |            | 1          |            |            |            | 1          |            |            |            |

Recommence avec le nouveau nombre qui est 3.
La puissance de 2 inférieure ou égale la plus proche de 3 est... 2.
Tu as **1** fois 2 dans ton nouveau nombre, reporte le chiffre 1 sous 2.

\\[ 3 - 2 = 1 \\]

| Indice   | 10              | 9          | 8          | 7          | 6          | 5          | 4          | 3          | 2          | 1          | 0          |
| ------   | --------------- | ---------- | ---------- | ---------- | ---------- | ---------- | ---------- | ---------- | ---------- | ---------- | ---------- |
| Notation | \\[ 2^{10} \\]  | \\[ 2^9\\] | \\[ 2^8\\] | \\[ 2^7\\] | \\[ 2^6\\] | \\[ 2^5\\] | \\[ 2^4\\] | \\[ 2^3\\] | \\[ 2^2\\] | \\[ 2^1\\] | \\[ 2^0\\] |
| Valeur   | 1024            | 512        | 256        | 128        | 64         | 32         | 16         | 8          | 4          | 2          | 1          |
| Nombre   |                 | 1          |            | 1          |            |            |            | 1          |            | 1          |            |

Recommence avec le nouveau nombre qui est 1.
La puissance de 2 inférieure ou égale la plus proche de 1 est... 1.
Tu as **1** fois 1 dans ton nouveau nombre, reporte le chiffre 1 sous 1.

\\[ 1 - 1 = 0 \\]

| Indice   | 10              | 9          | 8          | 7          | 6          | 5          | 4          | 3          | 2          | 1          | 0          |
| ------   | --------------- | ---------- | ---------- | ---------- | ---------- | ---------- | ---------- | ---------- | ---------- | ---------- | ---------- |
| Notation | \\[ 2^{10} \\]  | \\[ 2^9\\] | \\[ 2^8\\] | \\[ 2^7\\] | \\[ 2^6\\] | \\[ 2^5\\] | \\[ 2^4\\] | \\[ 2^3\\] | \\[ 2^2\\] | \\[ 2^1\\] | \\[ 2^0\\] |
| Valeur   | 1024            | 512        | 256        | 128        | 64         | 32         | 16         | 8          | 4          | 2          | 1          |
| Nombre   |                 | 1          |            | 1          |            |            |            | 1          |            | 1          | 1          |

Il te reste 0, tu as terminé. Reprends le tableau et ajoute **0** aux cases où
tu n'as pas écrit **1**.

| Indice   | 10              | 9          | 8          | 7          | 6          | 5          | 4          | 3          | 2          | 1          | 0          |
| ------   | --------------- | ---------- | ---------- | ---------- | ---------- | ---------- | ---------- | ---------- | ---------- | ---------- | ---------- |
| Notation | \\[ 2^{10} \\]  | \\[ 2^9\\] | \\[ 2^8\\] | \\[ 2^7\\] | \\[ 2^6\\] | \\[ 2^5\\] | \\[ 2^4\\] | \\[ 2^3\\] | \\[ 2^2\\] | \\[ 2^1\\] | \\[ 2^0\\] |
| Valeur   | 1024            | 512        | 256        | 128        | 64         | 32         | 16         | 8          | 4          | 2          | 1          |
| Nombre   |                 | 1          | 0          | 1          | 0          | 0          | 0          | 1          | 0          | 1          | 1          |

Ce sont les puissances de 2 que tu n'as pu soustraire à chaque nombre que tu
avais.

Tu peux donc dire que 651 en base 10 s'écrit 1010001011 en base 2.

## De la base 2 à la base 10

Tu vas maintenant faire l'inverse, passer de la base 2 à la base 10. Toujours
avec le tableau. Tu vas voir ça va être encore plus rapide.

Prenons un nombre en base 2 complètement au hasard : 1010011010.

Tu vas inscrire ce nombre dans le tableau le plus à droite possible.

| Indice   | 10              | 9          | 8          | 7          | 6          | 5          | 4          | 3          | 2          | 1          | 0          |
| ------   | --------------- | ---------- | ---------- | ---------- | ---------- | ---------- | ---------- | ---------- | ---------- | ---------- | ---------- |
| Notation | \\[ 2^{10} \\]  | \\[ 2^9\\] | \\[ 2^8\\] | \\[ 2^7\\] | \\[ 2^6\\] | \\[ 2^5\\] | \\[ 2^4\\] | \\[ 2^3\\] | \\[ 2^2\\] | \\[ 2^1\\] | \\[ 2^0\\] |
| Valeur   | 1024            | 512        | 256        | 128        | 64         | 32         | 16         | 8          | 4          | 2          | 1          |
| Nombre   |                 | 1          | 0          | 1          | 0          | 0          | 1          | 1          | 0          | 1          | 0          |

Maintenant, tu n'as qu'à reprendre les puissances de 2 avec un **1** en dessous
et les sommer ensemble.

\\[ 512 + 128 + 16 + 8 + 2 = 666 \\]

## Dans le cas de grands nombres

Si tu dois passer de la base 10 à la base 2 mais avec un nombre plus grand que
le tableau, il existe une technique pour généraliser la transformation.

Prenons un nombre vraiment plus grand que 1024 : 6789.

Tu vas diviser par 2 ton nombre et garder à chaque fois le **reste** de côté.
Rappelle toi de tes cours de primaire, c'est une opération euclidienne.

L'opération mathématique pour avoir le reste est %.

Ainsi si j'écris
\\[ x \\% 2 = 0 \\]
c'est qu'il reste 0 à la division **x / 2**. Tu peux aussi dire que *x* est pair.

Et si j'écris
\\[ x \\% 2 = 1 \\]
c'est qu'il reste 1 à la division **x / 2**. Tu peux aussi dire que *x* est impair.

Tu vas faire apparaître le résultat petit à petit avec cet affichage :

Résultat = 

Il se remplira à chaque itération de tes calculs en y inscrivant le reste que tu
viens de calculer sur la gauche.

\\[ 6789 / 2 = 3394 \\]
\\[ 6789 \\% 2 = 1 \\]
Résultat = 1

\\[ 3394 / 2 = 1697 \\]
\\[ 3394 \\% 2 = 0 \\]
Résultat = 01

\\[ 1697 / 2 = 848 \\]
\\[ 1697 \\% 2 = 1 \\]
Résultat = 101

\\[ 848 / 2 = 424 \\]
\\[ 848 \\% 2 = 0 \\]
Résultat = 0101

\\[ 424 / 2 = 212 \\]
\\[ 424 \\% 2 = 0 \\]
Résultat = 00101

\\[ 212 / 2 = 106 \\]
\\[ 212 \\% 2 = 0 \\]
Résultat = 000101

\\[ 106 / 2 = 53 \\]
\\[ 106 \\% 2 = 0 \\]
Résultat = 0000101

\\[ 53 / 2 = 26 \\]
\\[ 53 \\% 2 = 1 \\]
Résultat = 10000101

\\[ 26 / 2 = 13 \\]
\\[ 26 \\% 2 = 0 \\]
Résultat = 010000101

\\[ 13 / 2 = 6 \\]
\\[ 13 \\% 2 = 1 \\]
Résultat = 1010000101

\\[ 6 / 2 = 3 \\]
\\[ 6 \\% 2 = 0 \\]
Résultat = 01010000101

\\[ 3 / 2 = 1 \\]
\\[ 3 \\% 2 = 1 \\]
Résultat = 101010000101

\\[ 1 / 2 = 0 \\]
\\[ 1 \\% 2 = 1 \\]
Résultat = 0101010000101

Ta dernière division donne 0. Tu as terminé.

Tu sais maintenant que 6789 s'écrit 0101010000101 en base 2.
