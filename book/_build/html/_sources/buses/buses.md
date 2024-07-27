# Buses

## Typical 3 phase bus without neutral

```{code} 
{name: "1",  "pos_x":   0, "pos_y":   0, "units": "m", "U_kV":20.0, "N_nodes":3, "phi_deg_0":30.0},
```

## Typical 3 phase bus with neutral

```{code} 
{"name": "2",  "pos_x":   0, "pos_y":  0, "units": "m", "U_kV":0.4, "monitor":true}

```

## Parameters


| Data          | Description                                         |  Units    |
| :----------   | :-------------------------------------------------- |:---------:|  
| ``name``      | Name of the bus                                     | -         |
| ``pos_x``     | Optional x position                                 | ``units`` |
| ``pos_y``     | Optional y position                                 | ``units`` |
| ``units``     | m = meters, km = kilometers                         |   -       |
| ``U_kV``      | Nominal phase-phase RMS voltage                     | kV        |
| ``N_nodes``   | Number of nodes (by deafualt is 4)                  |  -        |
| ``phi_deg_0`` | Phase a voltage angle initial guess (default=0)     | degrees   | 
| ``monitor``   | See bus monitor                                     | True/False| 


## Bus monitor

When setting ``"monitor":True`` the phase to phase and phase to neutral voltages are computed and added as DAE system outputs in vectos $\mathbf z$.

