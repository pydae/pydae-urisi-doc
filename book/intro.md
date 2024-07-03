# Welcome to pydae-urisi

Unbalanced power system analysis and simulation using pydae.


```{figure} ./base_system.svg
:height: 250px
:name: avr-ntsst1

Power system in pydae 
```

```
data = {
"system":{S_base:1e6, K_p_agc:0.01, K_i_agc:0.01, K_xif:0.01},       
"buses":[],
"transformers":[],
"lines":[],
"loads":[],
"shunts":[],
"sources":[],
"vscs":[],
"line_codes":{}
}
```
