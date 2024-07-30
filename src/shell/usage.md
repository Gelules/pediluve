# Utilisation

J'admets ici que c'est la première fois que tu ouvres un shell qui a sa
configuration par défaut.

Une fois sur ton shell, voici ce qui se présente à toi.

```text
username@hostname:~$
```

Décortiquons tout ça.

**username** est ton nom d'utiisateur.

Le arobase '@' veut dire que tu es connecté sur une machine.

**hostname** est le nom de cette machine.

Le deux-points ':' est un simple séparateur pour la suite de la ligne.

Le tilde '~' signifie que tu te trouves dans ton **HOME**. C'est ton répertoire 
personnel avec tes fichiers personnels.

Le dollar '$' signifie que toutes les commandes que tu rentres sont exécutées
comme simple utilisateur.

Si tu avais un signe dièse '#' à la place, ça signifierait que les commandes
seront exécutées en tant que **root** (admin).

Pour simplifier la lecture des codes que je vais présenter, mon shell sera
présenté ainsi :
```text
$
```

Pour essayer, entre la commande **pwd**, et vois la différence de résultat avec
la mienne.

```text
$ pwd
/home/gelules
$
```

La commande **pwd** te dit où te trouves. C'est ton **P**ath **W**orking **D**irectory.

# Shutdown et reboot

Si tu veux arrêter ta machine, exécute la commande
```text
$ shutdown now
```

Si tu veux rebooter ta machine, exécute la commande
```text
$ reboot
```
