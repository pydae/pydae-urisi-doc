(ac_3ph_4w_)=
# VSC with coupling inductor

```{figure} ac_3ph_4w_l.svg
:height: 300px
:name: ac_3ph_4w


```

### Typical data

```{code} 
...
vscs:[
     {bus_ac:  "AC1", bus_dc:"DC1", type:"acdc_3ph_4w_pq", "A":350.0, "B":0.0,"C":0.03},
     ],
```


## Parameters


| Data            | Description                                         | Units        |
| :----------     | :-------------------------------------------------- |:------:      |  
| ``bus_ac``      | From bus name                                       | -            |
| ``bus_dc``      | To bus name                                         | -            |
| ``A``           | No load losses                                      |  W           | 
| ``B``           | Coefficient for losses proportional $I_{RMS}$       |  W/A         | 
| ``C``           | Coefficient for losses proportional $I_{RMS}^2$     |  W/A^2       | 
| ``monitor``     | See line monitor section                            | True/False   | 


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


#### Phase currents equations

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

#### Neutral currents equations

$$
\begin{align}
    g_7 &=  i_{nr} + i_{ar} + i_{br} + i_{cr} \\
    g_8 &=  i_{ni} + i_{ai} + i_{bi} + i_{ci} 
\end{align}
$$    


### Algebraic equations for DC side

$$ v_{dc} = v_{dp} - v_{dn} $$
    
$$p_{ac} = p_a + p_b + p_c $$

$$
p_{dc} =  p_{ac} + p_l
$$


$$ i_d = \frac{p_{dc}}{v_{dc}} $$



$$ \mathbf g = \left[ g_1,g_2,g_3,g_4,g_5,g_6,g_7,g_8 \right]^T $$
$$ \mathbf y = \left[ i_{ar}, i_{ai}, i_{br}, i_{bi}, i_{cr}, i_{ci}, i_{nr}, i_{ni}
 \right]^T $$




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

