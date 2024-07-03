# Shunt elements

Impedances that can be connected beetwen phases, phases and neutral and phases and neutral and ground.

 
## Typical neutral grounding

```{code} 
        {"bus": "1" , "R":  3.0, "X": 0.0, "bus_nodes": [3,0]}
```


where:

* ``"bus"``: name of the bus
* ``"bus_node"``: list of nodes where the shunt element is connected
* ``"R"``: shunt element resistance (Ω)
* ``"X"``: shunt element reactance (Ω)

