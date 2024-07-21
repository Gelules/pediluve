# Variables

Les variables sont des *mots* qui vont avoir une *valeur*.

Tu peux définir une variable ainsi :

```sh
#!/bin/sh

variable=valeur
```

Attention, il faut **absolument** que le signe égal '=' n'ait pas d'espace
autour de lui. Tout doit être collé.

Pour utiliser sa valeur, tu vas coller le signe dollar '$' devant le nom de
cette variable.

Pour afficher une variable, tu peux utiliser **echo**.

```sh
#!/bin/sh

variable=valeur
nombre=42
echo Ma variable variable a comme valeur $variable
echo Mon nombre est $nombre
```

Si tu veux concaténer deux variables ensembles, tu peux utiliser les accolades
pour bien les séparer. Tu peux même en construire de nouvelles comme ça.

```sh
#!/bin/sh

prenom=gel
nom_famille=ules
login=${prenom}${nom_famille}
domain=pediluve.info
mail=${login}@${domain}

echo Mon mail est $mail # L'adresse n'existe pas, pas la peine d'essayer
```
