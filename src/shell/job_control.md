# Job control

Le job control te permet de mettre en pause et remettre en route les programmes
que tu lances depuis ton shell.

Dans cet exemple, il faut que je seul programme lancé soit ton shell, rien
d'autre.

```sh
firefox
...
```

Maintenant que firefox est lancé, tu n'as plus la main sur ton shell. Firefox
l'utilise pour afficher son stdout et stderr.

Exécute la combinaison **ctrl+z** pour mettre Firefox en pause et regagner la
main sur ton shell.

```sh
...
ctrl+z
zsh: suspended  firefox
$
```

Selon le shell que tu utilises, tu peux avoir un message sensiblement différent.

Tu vas maintenant démarrer vlc  et gimp et pareil, exécuter **ctrl+z** pour
reprendre la main à chaque fois.

```sh
$ vlc
...
ctrl+z
zsh: suspended  vlc
$ gimp
...
ctrl+z
zsh: suspended gimp
$
```

Exécute la commande **jobs** pour voir l'état des jobs (processus) démarrés par
ton shell.

```sh
$ jobs
[1]    suspended  firefox
[2]  - suspended  vlc
[3]  + suspended  gimp
$
```

Tu as ta liste de jobs avec des identifiants. Le signe '-' est l'avant-dernier
jobs que tu as suspendu, et le signe '+' et le dernier jobs que tu as suspendu.

Si tu veux remettre un job en **foreground**, c'est à dire que tu relances son
exécution en lui laisant la main sur ton shell, utilise **fg %IDENTIFIANT** en
remplaçant **IDENTIFIANT** par le numéro du job.

```sh
$ fg %1 # firefox est réexécuté et on perd la main sur le shell
...
ctrl+z
```

Si tu veux mettre un job en **background**, c'est à dire que tu relances son
exécution tout en gardant la main sur ton shell, utilise **bg %IDENTIFIANT** en
remplaçant **IDENTIFIANT** par le numéro du job.

```sh
$ fg %1
$ # firefox reprend son exécution et on garde la main sur le shell
```

Pour arrêter un job, utilise la commande **kill %IDENTIFIANT** en remplaçant
**IDENTIFIANT** par le numéro du job.

```sh
kill %1
[1]  + terminated  firefox
$
```

Enfin, si tu veux lancer un processus en arrière-plan directement depuis ton
shell, ajoute le caractère **esperluette** '&' à la fin de ta commande.
```sh
$ vlc  &
[1] 22258
$
```

Le nombre affiché est le numéro du processus dans le système, il est plus que
probable que tu n'aies pas le même. Tu peux retrouver le nom d'un processus avec
son identidiant et la commande **ps**.

```sh
$ ps -p 22258
    PID TTY          TIME CMD
  22258 pts/0    00:00:00 vlc
```
