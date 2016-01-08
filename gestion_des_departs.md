# gestion des départs

Actuellement dans la procédure **update-world**


Première partie, on calcule la population qui va être autorisé à voler.

```
ask nodes
    [
      let my-instantaneous-total-population-to-fly ginstantaneous-total-population-to-fly 
      set stock-to-flight stock-to-flight + my-instantaneous-total-population-to-fly

      set gcumulated-pop-flight-expected-float gcumulated-pop-flight-expected-float + my-instantaneous-total-population-to-fly
    ]
```

