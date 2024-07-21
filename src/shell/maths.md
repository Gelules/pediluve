# Mathématiques

C'est parti pour faire un peu de mathématique.

Maintenant que tu sais utiliser des variables, tu vas pouvoir effectuer des
opérations mathématiques avec.

Tu peux faire toute opération mathématique dans des doubles parenthèses
précédées d'un signe dollar '$'.

```sh
#!/bin/sh

echo $((11 + 21))

a=42
b=666

echo $((a * b))

c=$((a + b * 11))
echo $c
```

Si tu mets une variale qui n'est pas un nombre, elle sera remplacée par 0.
