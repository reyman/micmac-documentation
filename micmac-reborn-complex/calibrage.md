# calibrage

= Tests et calibrages

== Noeud test SIR

Les utilitaires qui touchent au calibrage et à la vérification du modèles MicMac sont regroupées dans le fichier `calibration_and_test.nls` :

Trois procédures servent à initialiser, et mettre à jour le noeud test `nodeTests` :

* create-testNode 
* infect-testNode
* compute-SIR-testNode 

La méthode `compute-SIR-testNode` est appelée à chaque itération du modèle dans `update-world`, cette procédure met à jour les stock SIR de `nodeTests`.

== Calibrage

=== Signature

La signature de la fonction est la suivante dans netlogo `to do-calibrage [#mobility-rate #S-At-Node #I-At-Node #R-At-Node #number-nodes #beta #h #TerritorySize-km #durationEpidemy-days #Epsilon]`

.Arguments de la fonction \[options="header"\] \|=== \| argument de la fonction \|signification \| \#mobility-rate \| taux de mobilité fixé \| \#S-At-Node \| valeur du stock S voulue pour le noeud de calibrage \| \#I-At-Node \| valeur du stock I voulue pour le noeud de calibrage \| \#R-At-Node \| valeur du stock R voulue pour le noeud de calibrage \| \#number-node \| nombre de noeuds définies pour le modèle \| \#beta \| valeur beta \| \#h \| valeur de h \| \#TerritorySize-km \| taille du territoire  
\| \#durationEpidemy-days \| durée de l'épidémie \| \#Epsilon \| epsilon \|===

.Retour attendu de la fonction \[options="header"\] \|=== \| argument de la fonction \|signification \| \#speed-factor \| Vitesse des véhicule \| \#nbStepCalib \| Le nombre de pas nécessaire avant extinction de l'épidémie \(I inf. à Epsilon\) \| \#potential-population-departure \| La population susceptible de voler à chaque pas de temps. Un stock global ventilé ensuite sur chaque noeud. \|===

=== Calcul des sorties

La sortie `#potential-population-departure` est calculée en tenant compte :

. de la population totale  équivalente à l'ensemble des stocks \(I+S+R\) sur les noeuds , . du taux de mobilité  défini de façon globale par l'utilisateur, . de la durée d'épidémie  fonction de la maladie choisie , .  qui est le nombre de pas de temps \(ou de recalcul RK4 du SIR\) nécessaire au SIR sur un noeud avant que l'épidémie ne s'étéigne \(`I_Node` inf. `#Epsilon`\)

Le calcul résumé est le suivant : 

