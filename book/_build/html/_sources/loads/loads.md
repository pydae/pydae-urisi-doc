# Loads
 

Loads.

```{figure} loads_v2.svg
:height: 200px
:name: fig_loads
```

## Typical 3 phase load with neutral

```{code} 
    { bus: "I02" , kVA: 100.0, pf: 0.85, type:"3P+N", model:"ZIP"}
```



## Typical DC load 

```{code} 
   {"bus": "S15", "kW": 30.0, "type":"DC","model":"ZIP"}
```




## Parameters


| Data            | Description                                         |  Units       |
| :----------     | :-------------------------------------------------- |:---------:   |  
| ``bus``         | Bus name                                            | -            |
| ``kVA``         | Apparent power                                      | kVA          |
| ``pf``          | Power factor                                        | -            |
| ``type``        | See load type section                               | -            |
| ``model``       | See load type section                               | -            |


## Load type

In ``type`` it is posisble to introduce the following options:

- ``3P+N``: Three phase with neutral. Active and reactive powers can be different for each phase.
- ``3P``: Three phase without neutral. Only three phase total active and reactive powers can be defined. The sum of phasorial currents is zero.
- ``DC``: DC load.

## Load model

ZIP (Impedance+Current+Power) loads. 

