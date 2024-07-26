# Chaîne de caractères

Il y a une chose que je n'ai pas mentionnée quant aux chaînes de caractères,
c'est comment elles sont réellement construites par le compilateur.

Quand **printf** affiche ta chaîne, il ne peut pas calculer la taille avec la
technique de **sizeof**.

Pour ça, le compilateur va ajouter une valeur très spéciale à la fin de la
chaîne de caractères, la valeur **\0**.

Ainsi en **parcourant** ta chaîne de caractères, **printf** sait où s'arrêter :
une fois qu'il a atteind **\0**.

Voici comment est en mémoire une chaîne de caractères.

Pour la chaîne de caractères suivante :

```c
char text[] = "coucou";
```

| Index  | 0 | 1 | 2 | 3 | 4 | 5 | 6  |
| -----  | - | - | - | - | - | - | -  |
| Valeur | c | o | u | c | o | u | \0 |

Tu peux voir dans le **man 1 ascii** que le caractère **\0** a la valeur **0**.
