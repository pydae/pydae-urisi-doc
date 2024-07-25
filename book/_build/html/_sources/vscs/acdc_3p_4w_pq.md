(ac_3ph_4w_)=
# VSC with coupling inductor

```{figure} ac_3ph_4w_l.svg
:height: 300px
:name: ac_3ph_4w


```



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




## Model



### Phases and neutral complex voltages to ground

$$
\begin{align}
    \vec v_a &= v_{ar} + j v_{ai} \\
    \vec v_b &= v_{br} + j v_{bi} \\
    \vec v_c &= v_{cr} + j v_{ci} \\
    \vec v_n &= v_{nr} + j v_{ni}  
\end{align}
$$    

### Phases and neutral complex currents

$$
\begin{align}
    \vec i_a &= i_{ar} + j i_{ai} \\
    \vec i_b &= i_{br} + j i_{bi} \\
    \vec i_c &= i_{cr} + j i_{ci} \\
    \vec i_n &= i_{nr} + j i_{ni}  
\end{align}
$$    

### Losses per phase and neutral

$$
\begin{align}
p_{la} = A_l + B_l |\vec i_a| + C_l |\vec i_a|^2 \\
p_{lb} = A_l + B_l |\vec i_b| + C_l |\vec i_b|^2 \\
p_{lc} = A_l + B_l |\vec i_c| + C_l |\vec i_c|^2 \\
p_{ln} = A_l + B_l |\vec i_n| + C_l |\vec i_n|^2 
\end{align}
$$    

Total losses:

$$
p_l = p_{la} + p_{lb} + p_{lc} + p_{ln} 
$$


### Complex powers for the AC side

$$
\begin{align}
    s_a &= \left( \vec v_a - \vec v_n \right)  {\vec i_a}^* \\
    s_b &= \left( \vec v_b - \vec v_n \right)  {\vec i_b}^* \\
    s_c &= \left( \vec v_b - \vec v_n \right)  {\vec i_c}^*
\end{align}
$$

### Algebraic equations for AC side

$$
\begin{align}
    g_1 = 0 &=  \Re\left(s_a \right) - p_a^\star \\
    g_2 = 0 &=  \Re\left(s_b \right) - p_b^\star \\
    g_3 = 0 &=  \Re\left(s_c \right) - p_c^\star \\
    g_4 = 0 &=  \Im\left(s_a \right) - q_a^\star \\
    g_5 = 0 &=  \Im\left(s_b \right) - q_b^\star \\
    g_6 = 0 &=  \Im\left(s_c \right) - q_c^\star 
\end{align}
$$    

$$
\begin{align}
    0 &=  i_{nr} + i_{ar} + i_{br} + i_{cr} \\
    0 &=  i_{ni} + i_{ai} + i_{bi} + i_{ci} 
\end{align}
$$    




$$ v_{dc} = v_{dp} - v_{dn} $$
    
$$p_{ac} = p_a + p_b + p_c $$

$$
p_{dc} =  p_{ac} + p_l
$$


$$ i_d = \frac{p_{dc}}{v_{dc}} $$


    eq_i_neg = -i_neg - p_dc/v_dc
    #eq_v_og = -v_og/R_gdc - i_pos - i_neg 


    grid.dae['g'] += [eq_i_a_r,eq_i_a_i,
                      eq_i_b_r,eq_i_b_i,
                      eq_i_c_r,eq_i_c_i,
                      eq_i_n_r,eq_i_n_i,
                      eq_i_pos,eq_i_neg,#eq_v_og,
                      eq_p_dc
                      ]
    
    grid.dae['y_ini'] += [i_a_r,   i_a_i,
                      i_b_r,   i_b_i,
                      i_c_r,   i_c_i,
                      i_n_r,   i_n_i,
                      i_pos,i_neg,#v_og,
                      p_dc]

    grid.dae['y_run'] += [i_a_r,   i_a_i,
                      i_b_r,   i_b_i,
                      i_c_r,   i_c_i,
                      i_n_r,   i_n_i,
                      i_pos,i_neg,#v_og,
                      p_dc]

    # current injections ac side
    for ph in ['a','b','c','n']:
        i_s_r = sym.Symbol(f'i_vsc_{bus_ac_name}_{ph}_r', real=True)
        i_s_i = sym.Symbol(f'i_vsc_{bus_ac_name}_{ph}_i', real=True)  
        idx_r,idx_i = grid.node2idx(bus_ac_name,ph)
        grid.dae['g'] [idx_r] += -i_s_r
        grid.dae['g'] [idx_i] += -i_s_i
        i_s = i_s_r + 1j*i_s_i
        i_s_m = np.abs(i_s)
        grid.dae['h_dict'].update({f'i_vsc_{bus_ac_name}_{ph}_m':i_s_m})

    # current injections dc side
    idx_r,idx_i = grid.node2idx(f'{bus_dc_name}','a')
    grid.dae['g'] [idx_r] += i_pos 
    grid.dae['g'] [idx_i] += v_posi/1e3

    idx_r,idx_i = grid.node2idx(f'{bus_dc_name}','b')
    grid.dae['g'] [idx_r] += i_neg 
    grid.dae['g'] [idx_i] += v_negi/1e3  
    



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

### Example input

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






### Outputs

| Variable   | pydae name   | Description           |  Units  |
| :--------- | :----------  | :-------------------- |:-------:|     
| $p_{dc}$   | ``p_dc_<id>``| DC side power         |  W      | 

