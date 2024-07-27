(trafos_)=
# Transformers

```{code} 
{"bus_j": "1",  "bus_k": "2",  "S_n_kVA": 1000.0, "U_j_kV":20, "U_k_kV":0.4,
 "R_cc_pu": 0.01, "X_cc_pu":0.04, "connection": "Dyn11", 
 "conductors_j":3, "conductors_k":4, monitor:true}
```


## Parameters


| Data            | Description                                         |  Units       |
| :----------     | :-------------------------------------------------- |:---------:   |  
| ``bus_j``       | From bus name                                       | -            |
| ``bus_k``       | To bus name                                         | -            |
| ``S_n_kVA``     | Nominal power                                       | kVA          |
| ``U_j_kV``      | Bus j side nominal voltage                          | kV           |
| ``U_k_kV``      | Bus k side nominal voltage                          | kV           |
| ``R_cc``        | Short circuit resistance in per unit (machine base) | pu-m         | 
| ``X_cc``        | Short circuit reactance in per unit (machine base)  | pu-m         | 
| ``connection``  | See transformer connections section                 | True/False   | 
| ``conductors_j``| See line bus nodes section                          | True/False   | 
| ``conductors_k``| See line bus nodes section                          | True/False   | 


## Transformer connections

### Dyn11

```{figure} Dyn11.svg
:height: 150px
:name: Dyn11


```

Transformers are modeled as in [T1]_.



```{code} 

"transformers":[
         {"bus_j": "Bus_0",  "bus_k": "Bus_1",  "S_n_kVA": 1000.0, "U_j_kV":20, "U_k_kV":0.42,
         "R_cc_pu": 0.01, "X_cc_pu":0.04, "connection": "Dyn11",   "conductors_j": 3, "conductors_k": 4},
      ],
```


### Dyn1
 
```{figure} Dyn1.svg
:height: 150px
:name: Dyn11


```
 
```{code} 

"transformers":[
         {"bus_j": "Bus_0",  "bus_k": "Bus_1",  "S_n_kVA": 1000.0, "U_j_kV":20, "U_k_kV":0.42,
         "R_cc_pu": 0.01, "X_cc_pu":0.04, "connection": "Dyn1",   "conductors_j": 3, "conductors_k": 4},
      ],
```


### Ygd11_3w

```{figure} Ygd11_3w.svg
:height: 150px
:name: Dyn11


```
 
```{code} 

"transformers":[
            {"bus_j": "Bus_0",  "bus_k": "Bus_1",  "S_n_kVA": 2500.0, "U_j_kV":20, "U_k_kV":0.69,
            "R_cc_pu": 0.01, "X_cc_pu":0.04, "connection": "Ygd11_3w",   "conductors_j": 3, "conductors_k": 3},
      ],
```

{cite}`Dugan:03`.


## References

```{bibliography}