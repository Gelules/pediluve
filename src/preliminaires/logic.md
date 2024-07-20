# Portes logiques

Enfant, tu as appris les opérations mathématiques élémentaires : l'addition, la
soustraction, la multiplication et la division.

En informatique, il existe d'autres opérations élémentaires qu'on appelle des
portes logiques.

Tu vas appliquer ces portes logiques sur des bits, c'est à dire 0 et 1. Tu peux
remplacer 0 par Faux et 1 par Vrai comme valeurs logiques.

## NOT

La porte NOT est un inverseur. Elle prend une entrée et une sortie. Son rôle est
d'inverser la valeur en entrée.

| Entrée | Sortie |
| ------ | ------ |
|      0 |      1 |
|      1 |      0 |

## AND

La porte AND a deux entrées. Pour que le signal de sortie soit Vrai, il faut que
les deux signaux aux entrées le soient également.

| Entrée 1 | Entrée 2 | Sortie |
| ------   | ------   | ------ |
|      0   |      0   |      0 |
|      0   |      1   |      0 |
|      1   |      0   |      0 |
|      1   |      1   |      1 |

Si tu as besoin d'une phrase logique pour mieux comprendre, imagine que tu fais
des courses pour faire un gâteau (miam). Dans une ville, il existe deux
magasins, un spécialisé en lait et l'autre en farine.

Il faut que les deux magasins possèdent les bons produits pour que tu puisses
faire ton gâteau.

## OR

La porte OR a deux entrées. Pour que le signal de sortie soit Vrai, il faut
qu'au moins une des entrées soit à Vrai.

| Entrée 1 | Entrée 2 | Sortie |
| ------   | ------   | ------ |
|      0   |      0   |      0 |
|      0   |      1   |      1 |
|      1   |      0   |      1 |
|      1   |      1   |      1 |

Si tu as besoin d'une phrase logique pour mieux comprendre, imagine que tu fais
des courses pour acheter un gâteau (c'est plus rapide que de le préparer). Dans
une ville, il existe deux magasins spécialisés en gâteaux.

Il faut qu'au moins un des deux magasins soit ouvert pour que tu puisses avoir
ton gâteau.

## XOR

La porte XOR est un *eXclusive OR*, ou un *OU eXclusif*. Elle agit comme la
porte OR à condition d'avoir une exclusivité en entrée.

| Entrée 1 | Entrée 2 | Sortie |
| ------   | ------   | ------ |
|      0   |      0   |      0 |
|      0   |      1   |      1 |
|      1   |      0   |      1 |
|      1   |      1   |      0 |

Si tu as besoin d'une phrase logique pour mieux comprendre, imagine que tu fais
des courses pour le dernier disque de musique de ton artiste préféré. Dans
une ville, il existe deux magasins spécialisés en musique.

Il faut qu'au moins un des deux magasins possède les droits exclusifs de vente
pour qu'il existe une exclusivité. Si les deux magasins possèdent les droits de
vente, alors il n'y a pas d'exclusivité.

# Autres portes
Il existe d'autres portes logiques qui ne sont pas présentées ici. Elles ne te
seront pas utilises pour valider la piscine, mais elles pourraient l'êtres plus
tard. Je te laisse voir la [page Wikipédia à leur sujet](https://fr.wikipedia.org/wiki/Porte_logique).
