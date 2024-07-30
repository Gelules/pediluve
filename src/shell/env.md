# Variables d'environnement

Les variables d'environnement sont des variables initialisées au lancement de
ton shell.

Tu peux les avoir avec cette commande :
```text
$ env
```

Voici les variables que tu utiliseras le plus :

Tu peux connaitre le shell exécuté avec la variable **$SHELL**

```sh
$ echo $SHELL
```

Tu peux connaitre le nom d'utilisateur avec la variable $USER

```sh
$ echo $USER
```

Tu peux connaitre le chemin vers le **HOME** de l'utilisateur avec la variable
**HOME**

```sh
$ echo $HOME
```

Tu peux connaitre le répertoire courant avec la variable **$PWD** et le
répertoire courant précédent avec la variable **$OLDPWD**

```sh
echo $PWD
...
echo $OLDPWD
...
```
