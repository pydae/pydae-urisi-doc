(ess_dcac_)=
# BESS with DC/AC

```{figure} ac_3ph_4w_l.svg
:height: 300px
:name: ess_dcac


```

\begin{equation}
Z = R + jX 
\end{equation}

\begin{equation}
Z_n = R_n + jX_n 
\end{equation}

\begin{equation}
Z_{ng} = R_{ng} + jX_{ng} 
\end{equation}

$$
\begin{align}
\vec v_{ta} &= v_{tar} +j v_{tai}  \\ 
\vec v_{tb} &= v_{tbr} +j v_{tbi}  \\ 
\vec v_{tc} &= v_{tcr} +j v_{tci}  \\ 
\vec v_{tn} &= v_{tnr} +j v_{tni}   
\end{align}
$$

## Example input

```{code} 
...
vscs:[
     {"type":"ac_3ph_4w","bus":"A1","S_n":100e3,"U_n":400,
      "R":0.01,"X":0.05,"R_n":0.01,"X_n":0.1,"R_ng":0.01,"X_ng":3.0}
     ],
```

### Inputs

| Variable       | Code            | Description                          |  Units |
| :--------------| :----------     | :-----------------------             | :-----:| 
| $v_{tar}$      | ``v_ta_r_<id>`` | VSC phase a real part voltage        |  V     |    
| $v_{tai}$      | ``v_ta_i_<id>`` | VSC phase a imaginary part voltage   |  V     |             
| $v_{tbr}$      | ``v_tb_r_<id>`` | VSC phase b real part voltage        |  V     |    
| $v_{tbi}$      | ``v_tb_i_<id>`` | VSC phase b imaginary part voltage   |  V     |    
| $v_{tcr}$      | ``v_tc_r_<id>`` | VSC phase c real part voltage        |  V     |    
| $v_{tci}$      | ``v_tc_i_<id>`` | VSC phase c imaginary part voltage   |  V     |    
| $v_{tnr}$      | ``v_tn_r_<id>`` | VSC neutral real part voltage        |  V     |    
| $v_{tni}$      | ``v_tn_i_<id>`` | VSC neutral imaginary part voltage   |  V     |    

### Parameters

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




### Outputs

| Variable   | pydae name   | Description           |  Units  |
| :--------- | :----------  | :-------------------- |:-------:|     
| $p_{dc}$   | ``p_dc_<id>``| DC side power         |  W      | 

