# Run Command

Tu ne le sais peut-être pas, ton shell est configuré par un fichier **Run
Command**. C'est un fichier caché dans ton **HOME**.

Si tu es sur bash, ton fichier de configuration est
```sh
$ ~/.bashrc
```

Si tu es sur zsh, ton fichier de configuration est
```sh
$ ~/.zshrc
```

Si tu es sur un autre shell... regarde le man de ton shell pour savoir où se
trouve ton fichier de configuration.

## mkcd

On va agrémenter ton fichier de configuration avec une petite fonction bien
sympathique que j'aime bien.

Ouvre ton fichier de configuration et ajoute à la fin ces lignes :
```sh
mkcd ()
{
    [ ! -d "$1" ] && mkdir -p $1
    cd $1
}
```

Pour mettre à jour la configuration du shell où tu te trouves, exécute
```sh
$ . ~/.zshrc
```

Accorde la commande avec ton fichier de configuration.

La commande '.' exécute le fichier que tu donnes. Ton shell va donc exécuter son
fichier de Run Command pour se mettre à jour.

Tu peux aussi utiliser la commande **source**, c'est la même chose.

Pour les prochains shells, tu n'auras pas à faire cette commande. Ca sera
appliqué automatiquement.

Mais que fais cette commande ?

Décortiquons tout ça.

```sh
mkcd ()
{

}
```

Ca, c'est une **fonction** en shell. Une fonction c'est du code que tu pourras
appeler depuis ton shell.

```sh
    [ ! -d "$1" ] && mkdir -p $1
```
Cette ligne est compliquée à lire. Mais tu dois reconnaître la commande **mkdir
-p**.

```sh
    [ ! -d "$1" ]
```

Ce morceau de code va vérifier si le **1**er argument n'existe pas comme
répertoire.

```sh
    && mkdir -p $1
```

**&&** est une porte logique. Dans le contexte du shell, il s'agit de la porte
**AND** et exécutera la partie à droite seulement si la partie de gauche renvoie
Vrai.

La partie de droite créee une arborescence de répertoires.

```sh
    cd $1
```

cd va te déplacer dans le répertoire envoyé en **1**er argument.

La fonction mkcd va donc créer un répertoire ou même toute une arborescence de
répertoire et t'y **cd** automatiquement.

```sh
$ pwd
/home/gelules
$ ls /tmp/tests
ls: cannot access '/tmp/tests': No such file or directory
$ mkcd /tmp/tests/pediluve/shell
$ pwd
/tmp/tests/pediluve/shell
$
```
