# Tips and tricks

Tout au long des derniers chapitres, tu t'es écorché les doigts à taper des
commandes et sûrement mal taper le nom d'une commande, ce qui t'a valu de
recommencer.

Qu'à cela ne tienne, tu vas découvrir ici quelques raccourcis claviers.

# Touches fléchées

Déjà, les touches fléchées te permettent de déplacer ton cursus à gauche et à
droite si tu dois modifier ta commande avant de l'exécuter.

Ensuite, les touches fléchées haut et bas te permettent de te déplacer dans ton
historique de commandes et en rappeller plus rapidement qu'en réécrivant une
commande.

# Autocomplétion

Ton shell est capable d'autocompléter tes commandes. Appuie sur sur la touche de
tabulation pour lui demander d'autocompléter.

```text
$ touch travail ventre ventricule
$ ls t<TAB>
```

Tu verras que le fichier **travail** va s'autocompléter tout seul.

```text
$ ls v<TAB>
     ventr
```

Là il va faire face à un problème. Le shell ne peut pas deviner à ta place si tu
veux ventre ou ventricule. En appuyant une deuxième fois sur TAB, il t'affichera
quels fichiers correspondent.

```text
$ ls v<TAB><TAB>
     ventre ventricule
```

A toi de régler l'ambiguïté en ajoute **e** ou **i**.

# Arrêt d'un programme

Si jamais tu as lancé un programme ou un script depuis ton terminal et que tu
veux arrêter son exécution, exécute la combinaison de touches **ctrl+c** pour
envoyer un signal d'arrêt et reprendre la main sur ton terminal.

# Nettoyer le terminal

Si tu veux nettoyer tout ce qui est affiché sur ton terminal pour repartir sur
une vue propre, exécute la combinaison de touches **ctrl+l**.

# Recherche arrière

Avec **ctrl+r**, tu peux recherche une commande. Par exemple **ctrl+r** *cp -*
te montrera la dernière commande qui contient *cp -r*, si tu rappuies sur
**ctrl+r**, la commande précédent s'affichera, jusqu'à afficher la toute
première commande dans ton historique qui contient *cp -r*.

# Déplacement rapide du curseur

Si tu utilises **ctrl+fleche** gauche ou droite, tu peux déplacer le curseur de
mot en mot.

Tu peux aussi faire **alt+f** pour *forward* (avant) et **alt+b** pour
*backward* (arrière) pour faire pareil.

Tu peux aussi faire la combinaison **ctrl+a** pour envoyer le cursus au tout
début de la ligne, et **ctrl+e** pour l'envoyer à la fin de la ligne.

# Suppression avant / après le curseur

Si ton curseur est au milieu de la commande, et que tu veux supprimer tout ce
qu'il y a à droite, tu peux faire la combinaison **ctrl+k**. Si tu veux
supprimer tout ce qu'il y a à gauche, effectuer la combinaison **ctrl+u**.
