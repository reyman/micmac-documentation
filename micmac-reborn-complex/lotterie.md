# Lotterie

= Fonctionnement de la lotterie

L'inverse a lieu lors de la création de l'avion devant se rendre d'une ville à l'autre et en particulier lors du calcul des ses passagers. Le problème est le suivant : comment tirer un nombre de sains, infectés et susceptibles entiers à partir des trois stocks d'une population \(qui peuvent avoir un nombre non-entier d'individus\), tout en respectant les proportions de chacun des stocks.

Un algorithme dit de "loterie" a donc été introduit. Cet algorithme est présenté ici car il est assez général pour être appliqué à de nombreux problèmes. Il est basé sur deux sous-programmes: \texttt{find-state} et \texttt{generate-Group}.

Etant donné un ensemble de valeurs \(entières\) représentant le nombre d'individus dans chacun des état, \texttt{find-state} choisit au hasard l'un des états avec une probabilité proportionnelle au nombre d'individus dans cet état. Cette fonction renvoie une valeur entière représentant l'état choisi, cet entier correspond à l'index de l'état choisi dans la liste passée en paramètre.

## \[source,bash\]

to-report find-state \[\#roundedStock\]

let roundedPop sum \#roundedStock let random-value \(random roundedPop\) + 1

let state 0 let step-i 0

if roundedPop &gt; 0 \[ foreach \#roundedStock \[  
if state = 0 \[ set random-value random-value - item step-i \#roundedStock ifelse random-value &lt;= 0 \[ set state step-i + 1  
\]\[ set step-i step-i + 1 \] \] \] \]

```text
report state
```

## end

La fonction \texttt{generate-Group} prend en paramètre la liste du nombre des individus dans chacun des états possibles \texttt{pop} et le nombre d'individus dans le groupe à générer \(\texttt{sample\_number}\). Elle renvoie le groupe généré contenant \texttt{sample\_number} individus avec la même proportions d'individus dans chacun des états que \texttt{pop}. Le groupe généré contient un nombre entier dans chacun des états. De plus la population renvoyée est ôtée de la population passée en paramètre. Dans cette fonction, deux précautions sont prises préalablement : \begin{itemize} \item tout d'abord la population passée en paramètre est arrondie état par état à l'entier inférieur. Cela signifie que si un des état contient une valeur de $0.3$ elle sera arrondie à $0$. \item il est vérifiée que la population passée en paramètre a une taille supérieure, après avoir été arrondie, au nombre d'agents de la population attendue en sortie. \end{itemize}

Ensuite la fonction \texttt{find-state} est appelée \texttt{int\(sample\_number\)}. A chaque appel, un individu est extrait de la population initiale et ajouté à la population qui va être renvoyée. En conséquence \(d'après l'algorithme de \texttt{find-state}\), si à un moment au cours de l'exécution de l'algorithme le nombre d'individus \(de la population passée en paramètre\) dans un des états passe à $0$, aucun individu dans cet état ne pourra plus être tiré.

## \[source,bash\]

to-report generate-passengers \[pop sample\_number\]

let rounded\_pop recompute-rounded-population pop let S\_pop item 0 rounded\_pop let I\_pop item 1 rounded\_pop let R\_pop item 2 rounded\_pop

let state 0 let Si 0 let Ii 0 let Ri 0

```text
  if ((sum rounded_pop) >= int(sample_number))
  [ 
    ;; One returned state by find-state
    repeat sample_number 
    [ 
      ;;compute/recompute population at each turn
      set state find-state recompute-rounded-population (list S_pop I_pop R_pop)

      if state = 1 [
        set Si Si + 1
        set S_pop S_pop - 1
      ]

      if state = 2 [
        set Ii Ii + 1
        set I_pop I_pop - 1
      ]

      if state = 3 [
        set Ri Ri + 1
        set R_pop R_pop - 1
      ]
    ]
  ]
```

if Si = 0 and Ii = 0 and Ri = 0 \[ show "ERROR STATE EQUAL TO 0" print sum rounded\_pop \]

report \(list Si Ii Ri\)

## end

## \[source,bash\]

to-report recompute-rounded-population \[pop\]  
report \(list int\(item 0 pop\) int\(item 1 pop\) int\(item 2 pop\)\)

## end

==

