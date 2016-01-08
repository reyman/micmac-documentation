# gestion des départs

Actuellement dans la fonction **update-world**

Les paramètres sont les suivants : 

#cumulated-pop-flight-expected-float #instantaneous-total-population-to-fly #airplane-size

Première partie, on calcule au niveau des noeud la population qui va être autorisé à voler.


```
ask nodes
    [
      let my-instantaneous-total-population-to-fly ginstantaneous-total-population-to-fly 
      set stock-to-flight stock-to-flight + my-instantaneous-total-population-to-fly

      set gcumulated-pop-flight-expected-float gcumulated-pop-flight-expected-float + my-instantaneous-total-population-to-fly
    ]
```


