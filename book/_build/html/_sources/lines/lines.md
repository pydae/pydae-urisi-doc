# Lines


```{figure} lines.svg
:height: 200px
:name: Dyn11


```
 
## Typical 3 phase line with neutral using code

```{code} 
{"bus_j": "2", "bus_k": "3", "code": "UG1", "m": 100.0, monitor:true, sym:true},
```

## Typical 3 phase line with neutral using R and X

```{code} 
{"bus_j": "2", "bus_k": "3", "R":0.5, "X":0.08, "m": 100.0, monitor:true, sym:true},
``` 

## Typical single phase line  

```{code} 
{ bus_j: "3",  bus_k: "4",  code: "UG1sp", m: 100.0, vsc_line:true, monitor:true, bus_j_nodes:[0,3], bus_k_nodes:[0,3]},
``` 



## Parameters


| Data            | Description                                         |  Units       |
| :----------     | :-------------------------------------------------- |:---------:   |  
| ``bus_j``       | From bus name                                       | -            |
| ``bus_k``       | To bus name                                         | -            |
| ``code``        | See line code section                               | -            |
| ``m``           | Line longitud                                       | ``m``        |
| ``monitor``     | See line monitor section                            | True/False   | 
| ``sym``         | See line symbolic section                           | True/False   | 
| ``bus_j_nodes`` | See line bus nodes section                          | True/False   | 
| ``bus_k_nodes`` | See line bus nodes section                          | True/False   | 
| ``R``           | Resistance per km                                   | $\Omega$/km$ | 
| ``X``           | Reactance per km                                    | $\Omega$/km$ | 




## Line code

In ``code`` it is posiisble to introduce the reference to the primitive matrix of the line.

```{code} 
"line_codes":
      {
      "UG1":
            {"R":[[ 0.211,  0.049,  0.049,  0.049],
                  [ 0.049,  0.211,  0.049,  0.049],
                  [ 0.049,  0.049,  0.211,  0.049],
                  [ 0.049,  0.049,  0.049,  0.211]],
             "X":[[ 0.747,  0.673,  0.651,  0.673],
                  [ 0.673,  0.747,  0.673,  0.651],
                  [ 0.651,  0.673,  0.747,  0.673],
                  [ 0.673,  0.651,  0.673,  0.747]], "I_max":430.0
      },
```

## Line monitor

When setting ``"monitor":True`` the phase to phase and phase to neutral voltages are computed and added as DAE system outputs in vectos $\mathbf z$.

## Line symbolic


## Line bus nodes

