# PATH

La variable d'environnement **PATH** est une variable particulière. C'est la
variable qui permet à ton shell de trouver les programmes à exécuter.

Si je prends en exemple mon **PATH**
```sh
$ echo $PATH
/usr/local/bin:/usr/bin:/bin:/usr/local/sbin:/home/gelules/.local/bin/:/usr/lib/jvm/default/bin:/usr/bin/site_perl:/usr/bin/vendor_perl:/usr/bin/core_perl:/home/gelules/.local/bin
```

Je peux voir que le 1er répertoire vérifié est **/usr/local/bin**, puis
**/usr/bin**, et ainsi de suite.

On va faire un petit jeu.

Crée le répertoire **/tmp/test/** et **cd** dedans.

```sh
$ mkdir /tmp/test
$ cd /tmp/test
```

Crée le fichier avec ton éditeur et ajoute la ligne suivante dedans :
```sh
$ cat firefox
#!/bin/sh

echo Et non, je ne suis pas Firefox
$
```

Rends le exécutable.

```sh
$ chmod +x firefox
```

On va mettre la variable d'environnement PATH à jour. Elle ne le sera que pour
ton shell actuel, les futurs shells ne seront pas impactés.

```sh
$ PATH=/tmp/test:$PATH
$ firefox
Et non, je ne suis pas Firefox
$
```

Tu peux voir que ton shell trouve d'abord le fichier **firefox** que tu viens de
créer.

Tu peux voir quel programme ton shell trouvera avec la commande **which**.

```sh
$ which firefox
/tmp/test/firefox
$
```
