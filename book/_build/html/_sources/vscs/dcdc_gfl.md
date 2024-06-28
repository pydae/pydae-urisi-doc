(dcdc_gfl_)=
# DC-DC converter GFL

```{figure} dcdc_gfl.svg
:height: 300px
:name: dcdc_gfl


```


## Example input

```{code} 
...
vscs:[
     {"type":"ac_3ph_4w","bus":"A1","S_n":100e3,"U_n":400,
      "R":0.01,"X":0.05,"R_n":0.01,"X_n":0.1,"R_ng":0.01,"X_ng":3.0}
     ],
```

## Inputs

| Variable       | Code            | Description                          |  Units |
| :--------------| :----------     | :-----------------------             | :-----:| 
| $e_{h  }$      | ``e_h_<id>``    | VSC phase a real part voltage        |  V     |    


## Parameters

| Constant   | Code       | pydae name        | Default| Description                               |  Units  |
| :--------- |:---------  |:---------         |-------:| :---------------------------------------- | :------:| 
| $S_n$      | ``S_n``    | ``S_n_<id>``      | -      | Nominal apparent power                    |  VA     | 
| $U_n$      | ``U_n``    | ``U_n_<id>``      | -      | Nominal phase to phase RMS voltage        |  V      | 
| $R$        | ``R``      | ``R_s_<id>``      | 0.01   | Coupling inductor resistance              |  Ω      | 
| $X$        | ``X``      | ``X_s_<id>``      | 0.05   | Coupling inductor reactance               |  Ω      | 
| $R_n$      | ``R_n``    | ``R_sn_<id>``     | 0.01   | Coupling inductor neutral resistance      |  Ω      | 
| $X_n$      | ``X_n``    | ``X_sn_<id>``     | 0.05   | Coupling inductor neutral reactance       |  Ω      | 
| $R_{ng}$   | ``R_ng``   | ``R_ng_<id>``     | 3.0    | Grounding resistance                      |  Ω      | 
| $X_{ng}$   | ``X_ng``   | ``X_ng_<id>``     | 0.0    | Grounding reactance                       |  Ω      | 




## Outputs

| Variable   | pydae name   | Description           |  Units  |
| :--------- | :----------  | :-------------------- |:-------:|     
| $p_{dc}$   | ``p_dc_<id>``| DC side power         |  W      | 

