# gestion des E/S aéroports

= gestion des entrees/sorties aeroports

image::images/img-reborn-complex/ES\_aeroport.svg.png\[ES,width=400,align=center\]

Chaque aéroport comprend deux arguments dédié aux entrées / sorties des avions : une entrée \(`in_airport`\) et une sortie \(`out_airport`\).

Les avions ne peuvent en effet atterrir dans un aéroport que si la sortie de l'aéroport faisant partir l'avion est ouverte \(`out_airport`\), et si l'entrée de l'aéroport recevant l'avion est ouverte \(`in_airport = 1`\).

Par défaut toutes les entrées et les sorties d'aéroports sont ouvertes au début de la simulation \( `in-airport = 1` et `out-airport = 1`\) au début du programme.

Le lecteur pourra remarquer dans ce diagramme d'activité que les deux stratégies sont cumulables, la première stratégie étant traité avant la deuxième stratégie dans le code. Selon que l'utilisateur du modèle active ou n'active pas l'une ou l'autre de ces stratégies, la combinatoire peut donc être assez complexe.

== Signature

La signature de la procédure est la suivante dans netlogo `to update-node-airport [#node]`

.Arguments de la fonction \[options="header"\] \|=== \| argument de la fonction \|signification \| \#node\| aéroport à modifier \|===

== Stratégie 1

Dans le cas de la link:./strategies.adoc\[stratégie 1\], on teste pour chaque aéroport si la proportion d'infecté _I_ dépasse le seuil `gtheta1`. Si c'est le cas on ferme les entrées et les sorties de cet aéroports \( `in-airport = 0` et `out-airport = 0`\). C'est une mise en quarantaine stricte, qui dure jusqu'à ce que la proportion d'infecté _I_ repasse en dessous de .

La proportion d'infecté est calcul en fonction de la population présente dans chaque aéroport 

## \[source,bash\]

if gstrategy1 = true \[ ask node \[ ifelse \(I\_Node / \( I\_Node + S\_Node + R\_Node\) &gt; gtheta1 \) \[ set out-airport 0 set in-airport 0 \] \[ set out-airport 1 set in-airport 1 \] \]

## \]

== Stratégie 2

Dans le cas de la link:./strategies.adoc\[stratégie 2\], on teste pour chaque aéroport si la proportion d'infecté _I_ dépasse le seuil `gtheta2`. Si c'est le cas on ferme les entrées de cet aéroports \( `in-airport = 1` et `out-airport = 0`\). La particularité

## \[source,bash\]

if gstrategy2 = true \[ ask node \[ ifelse I\_Node / \( I\_Node + S\_Node + R\_Node\) &gt; gtheta2 \[ set in-airport 0 \] \[ set in-airport 1 \] \]

## \]

