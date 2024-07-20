# Vous n'avez pas les bases

\\[ chiffre * base \^{indice} \\]

Avant d'attaquer la pratique, il faut revoir quelques préliminaires
mathématiques.

En informatique, plusieurs bases sont utilisées pour travailler avec des
données. Les bases 2, 16 et 8. Cette dernière est plus rarement utilisée et ne
sera pas abordée dans ce cours. Mais avec les connaissances que tu auras en
travaillant les bases 2 et 16, tu sauras travailler avec la base 8 simplement.

Avant de travailler les autres bases, tu vas revoir la base 10 que tu utilises
tous les jours.

La base 10 possède 10 chiffres : 0, 1, 2, 3, 4, 5, 6, 7, 8 et 9.

La base 10 utilise les puissances de 10. Prends ce tableau en référence :

| Indice   | 4           | 3           | 2           | 1           | 0           |
| ------   | -----       | ----        | ---         | --          | -           |
| Notation | \\[ 10^4\\] | \\[ 10^3\\] | \\[ 10^2\\] | \\[ 10^1\\] | \\[ 10^0\\] |
| Valeur   | 10000       | 1000        | 100         | 10          | 1           |

Tu peux voir que \\[ 10^3 = 1000\\]

La base 10 ne fait que se multiplier par 10 pour passer à l'indice suivant.

Ce tableau est à utiliser pour décomposer n'importe quel nombre.

Prenons un nombre pris au hasard : 4269.

Pour décomposer ton nombre tu vas d'abord reporter le nombre sous le tableau en
partant de la droite, ce qui donne :

| Indice   | 4           | 3           | 2           | 1           | 0           |
| ------   | ----------- | ----------- | ----------- | ----------- | ----------- |
| Notation | \\[ 10^4\\] | \\[ 10^3\\] | \\[ 10^2\\] | \\[ 10^1\\] | \\[ 10^0\\] |
| Valeur   | 10000       | 1000        | 100         | 10          | 1           |
| Nombre   |             | 4           | 2           | 6           | 9           |

Tu peux voir que *4* a comme indice *3*, que *2* a comme indice *2*, que *6* a
comme indice *1* et que *9* a comme indice *0*.

Décompose le nombre ainsi :
\\[ 4 * 10\^3 + 2 * 10\^2 + 6 * 10\^1 + 9 * 10\^0 \\]

Calcule les puissances :
\\[ 4 * 1000 + 2 * 100 + 6 * 10 + 9 * 1 \\]

Calcule les multiplications :
\\[ 4000 + 200 + 60 + 9 \\]

Tu as décomposé ton nombre en utilisant la base 10.

Pourquoi tous ces efforts ?

Pour te préparer aux bases 2 et 16.
