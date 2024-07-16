# [Python - Power BI] Relatório mensal clínicas
```python
import pandas as pd
import numpy as np
```


```python
faltas = pd.read_excel('Faltas.xlsx')
prod = pd.read_excel('Produtividade.xlsx', skiprows=1)
espera = pd.read_excel("Tempo de Espera.xlsx", skiprows=1)
```


```python
faltas
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>UNIDADE</th>
      <th>Especialidades</th>
      <th>PROFISSIONAL</th>
      <th>Total de Consultas</th>
      <th>Consultas Efetivadas</th>
      <th>% Consultas Efetivadas</th>
      <th>Consultas Canceladas</th>
      <th>% Consultas Canceladas</th>
      <th>Faltas Médicas</th>
      <th>% Faltas Médicas</th>
      <th>Faltas Paciente</th>
      <th>% Faltas Pacientes</th>
      <th>Remarcações Médicas</th>
      <th>% Remarcações Médcas</th>
      <th>Remarcações ADM</th>
      <th>% Remarcações ADM</th>
      <th>Remarcações Pacientes</th>
      <th>% Remarcações Pacientes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Total</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>38757</td>
      <td>22290</td>
      <td>0.575122</td>
      <td>16467</td>
      <td>0.424878</td>
      <td>1086</td>
      <td>0.028021</td>
      <td>13849</td>
      <td>0.357329</td>
      <td>1015</td>
      <td>0.026189</td>
      <td>517</td>
      <td>0.013340</td>
      <td>14912</td>
      <td>0.277800</td>
    </tr>
    <tr>
      <th>1</th>
      <td>CLINICA JA</td>
      <td>Total</td>
      <td>NaN</td>
      <td>8065</td>
      <td>4382</td>
      <td>0.543335</td>
      <td>3683</td>
      <td>0.456665</td>
      <td>427</td>
      <td>0.052945</td>
      <td>2745</td>
      <td>0.340360</td>
      <td>428</td>
      <td>0.053069</td>
      <td>83</td>
      <td>0.010291</td>
      <td>3467</td>
      <td>0.300616</td>
    </tr>
    <tr>
      <th>2</th>
      <td>CLINICA JA</td>
      <td>CLINICO GERAL</td>
      <td>NaN</td>
      <td>2382</td>
      <td>1315</td>
      <td>0.552057</td>
      <td>1067</td>
      <td>0.447943</td>
      <td>109</td>
      <td>0.045760</td>
      <td>896</td>
      <td>0.376154</td>
      <td>34</td>
      <td>0.014274</td>
      <td>28</td>
      <td>0.011755</td>
      <td>929</td>
      <td>0.280580</td>
    </tr>
    <tr>
      <th>3</th>
      <td>CLINICA JA</td>
      <td>CLINICO GERAL</td>
      <td>MEDICO CDS</td>
      <td>201</td>
      <td>102</td>
      <td>0.507463</td>
      <td>99</td>
      <td>0.492537</td>
      <td>0</td>
      <td>0.000000</td>
      <td>73</td>
      <td>0.363184</td>
      <td>0</td>
      <td>0.000000</td>
      <td>26</td>
      <td>0.129353</td>
      <td>105</td>
      <td>0.343137</td>
    </tr>
    <tr>
      <th>4</th>
      <td>CLINICA JA</td>
      <td>CLINICO GERAL</td>
      <td>MEDICO HPD</td>
      <td>683</td>
      <td>404</td>
      <td>0.591508</td>
      <td>279</td>
      <td>0.408492</td>
      <td>30</td>
      <td>0.043924</td>
      <td>249</td>
      <td>0.364568</td>
      <td>0</td>
      <td>0.000000</td>
      <td>0</td>
      <td>0.000000</td>
      <td>234</td>
      <td>0.255180</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>221</th>
      <td>CLINICA DT</td>
      <td>PEDIATRIA</td>
      <td>MEDICO RAD</td>
      <td>173</td>
      <td>86</td>
      <td>0.497110</td>
      <td>87</td>
      <td>0.502890</td>
      <td>44</td>
      <td>0.254335</td>
      <td>42</td>
      <td>0.242775</td>
      <td>0</td>
      <td>0.000000</td>
      <td>1</td>
      <td>0.005780</td>
      <td>106</td>
      <td>0.379928</td>
    </tr>
    <tr>
      <th>222</th>
      <td>CLINICA DT</td>
      <td>PEDIATRIA</td>
      <td>MEDICO SVR</td>
      <td>330</td>
      <td>215</td>
      <td>0.651515</td>
      <td>115</td>
      <td>0.348485</td>
      <td>17</td>
      <td>0.051515</td>
      <td>98</td>
      <td>0.296970</td>
      <td>0</td>
      <td>0.000000</td>
      <td>0</td>
      <td>0.000000</td>
      <td>158</td>
      <td>0.323770</td>
    </tr>
    <tr>
      <th>223</th>
      <td>CLINICA DT</td>
      <td>PEDIATRIA</td>
      <td>MEDICO TDC</td>
      <td>323</td>
      <td>251</td>
      <td>0.777090</td>
      <td>72</td>
      <td>0.222910</td>
      <td>0</td>
      <td>0.000000</td>
      <td>68</td>
      <td>0.210526</td>
      <td>0</td>
      <td>0.000000</td>
      <td>4</td>
      <td>0.012384</td>
      <td>161</td>
      <td>0.332645</td>
    </tr>
    <tr>
      <th>224</th>
      <td>CLINICA DT</td>
      <td>PEDIATRIA</td>
      <td>MEDICO VDS</td>
      <td>367</td>
      <td>266</td>
      <td>0.724796</td>
      <td>101</td>
      <td>0.275204</td>
      <td>29</td>
      <td>0.079019</td>
      <td>71</td>
      <td>0.193460</td>
      <td>0</td>
      <td>0.000000</td>
      <td>1</td>
      <td>0.002725</td>
      <td>201</td>
      <td>0.353873</td>
    </tr>
    <tr>
      <th>225</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>54872</td>
      <td>33138</td>
      <td>0.603915</td>
      <td>21734</td>
      <td>0.396085</td>
      <td>1441</td>
      <td>0.026261</td>
      <td>17917</td>
      <td>0.326524</td>
      <td>1410</td>
      <td>0.025696</td>
      <td>966</td>
      <td>0.017605</td>
      <td>22565</td>
      <td>0.291357</td>
    </tr>
  </tbody>
</table>
<p>226 rows × 18 columns</p>
</div>




```python
faltas_col = faltas[['UNIDADE', 'Especialidades', 'PROFISSIONAL','Consultas Efetivadas', 'Faltas Médicas', 'Faltas Paciente','Remarcações Médicas', 'Total de Consultas']]
faltas_col
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>UNIDADE</th>
      <th>Especialidades</th>
      <th>PROFISSIONAL</th>
      <th>Consultas Efetivadas</th>
      <th>Faltas Médicas</th>
      <th>Faltas Paciente</th>
      <th>Remarcações Médicas</th>
      <th>Total de Consultas</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Total</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>22290</td>
      <td>1086</td>
      <td>13849</td>
      <td>1015</td>
      <td>38757</td>
    </tr>
    <tr>
      <th>1</th>
      <td>CLINICA JA</td>
      <td>Total</td>
      <td>NaN</td>
      <td>4382</td>
      <td>427</td>
      <td>2745</td>
      <td>428</td>
      <td>8065</td>
    </tr>
    <tr>
      <th>2</th>
      <td>CLINICA JA</td>
      <td>CLINICO GERAL</td>
      <td>NaN</td>
      <td>1315</td>
      <td>109</td>
      <td>896</td>
      <td>34</td>
      <td>2382</td>
    </tr>
    <tr>
      <th>3</th>
      <td>CLINICA JA</td>
      <td>CLINICO GERAL</td>
      <td>MEDICO CDS</td>
      <td>102</td>
      <td>0</td>
      <td>73</td>
      <td>0</td>
      <td>201</td>
    </tr>
    <tr>
      <th>4</th>
      <td>CLINICA JA</td>
      <td>CLINICO GERAL</td>
      <td>MEDICO HPD</td>
      <td>404</td>
      <td>30</td>
      <td>249</td>
      <td>0</td>
      <td>683</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>221</th>
      <td>CLINICA DT</td>
      <td>PEDIATRIA</td>
      <td>MEDICO RAD</td>
      <td>86</td>
      <td>44</td>
      <td>42</td>
      <td>0</td>
      <td>173</td>
    </tr>
    <tr>
      <th>222</th>
      <td>CLINICA DT</td>
      <td>PEDIATRIA</td>
      <td>MEDICO SVR</td>
      <td>215</td>
      <td>17</td>
      <td>98</td>
      <td>0</td>
      <td>330</td>
    </tr>
    <tr>
      <th>223</th>
      <td>CLINICA DT</td>
      <td>PEDIATRIA</td>
      <td>MEDICO TDC</td>
      <td>251</td>
      <td>0</td>
      <td>68</td>
      <td>0</td>
      <td>323</td>
    </tr>
    <tr>
      <th>224</th>
      <td>CLINICA DT</td>
      <td>PEDIATRIA</td>
      <td>MEDICO VDS</td>
      <td>266</td>
      <td>29</td>
      <td>71</td>
      <td>0</td>
      <td>367</td>
    </tr>
    <tr>
      <th>225</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>33138</td>
      <td>1441</td>
      <td>17917</td>
      <td>1410</td>
      <td>54872</td>
    </tr>
  </tbody>
</table>
<p>226 rows × 8 columns</p>
</div>




```python
faltas_col.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 226 entries, 0 to 225
    Data columns (total 8 columns):
     #   Column                Non-Null Count  Dtype 
    ---  ------                --------------  ----- 
     0   UNIDADE               224 non-null    object
     1   Especialidades        223 non-null    object
     2   PROFISSIONAL          176 non-null    object
     3   Consultas Efetivadas  226 non-null    int64 
     4   Faltas Médicas        226 non-null    int64 
     5   Faltas Paciente       226 non-null    int64 
     6   Remarcações Médicas   226 non-null    int64 
     7   Total de Consultas    226 non-null    int64 
    dtypes: int64(5), object(3)
    memory usage: 14.3+ KB
    


```python
faltas_rename = {
    'UNIDADE': 'Unidade',
    'Especialidades' : 'Especialidade',
    'PROFISSIONAL' : 'Profissional'
}
faltas_clean = faltas_col.rename(columns = faltas_rename)
faltas_clean
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unidade</th>
      <th>Especialidade</th>
      <th>Profissional</th>
      <th>Consultas Efetivadas</th>
      <th>Faltas Médicas</th>
      <th>Faltas Paciente</th>
      <th>Remarcações Médicas</th>
      <th>Total de Consultas</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Total</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>22290</td>
      <td>1086</td>
      <td>13849</td>
      <td>1015</td>
      <td>38757</td>
    </tr>
    <tr>
      <th>1</th>
      <td>CLINICA JA</td>
      <td>Total</td>
      <td>NaN</td>
      <td>4382</td>
      <td>427</td>
      <td>2745</td>
      <td>428</td>
      <td>8065</td>
    </tr>
    <tr>
      <th>2</th>
      <td>CLINICA JA</td>
      <td>CLINICO GERAL</td>
      <td>NaN</td>
      <td>1315</td>
      <td>109</td>
      <td>896</td>
      <td>34</td>
      <td>2382</td>
    </tr>
    <tr>
      <th>3</th>
      <td>CLINICA JA</td>
      <td>CLINICO GERAL</td>
      <td>MEDICO CDS</td>
      <td>102</td>
      <td>0</td>
      <td>73</td>
      <td>0</td>
      <td>201</td>
    </tr>
    <tr>
      <th>4</th>
      <td>CLINICA JA</td>
      <td>CLINICO GERAL</td>
      <td>MEDICO HPD</td>
      <td>404</td>
      <td>30</td>
      <td>249</td>
      <td>0</td>
      <td>683</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>221</th>
      <td>CLINICA DT</td>
      <td>PEDIATRIA</td>
      <td>MEDICO RAD</td>
      <td>86</td>
      <td>44</td>
      <td>42</td>
      <td>0</td>
      <td>173</td>
    </tr>
    <tr>
      <th>222</th>
      <td>CLINICA DT</td>
      <td>PEDIATRIA</td>
      <td>MEDICO SVR</td>
      <td>215</td>
      <td>17</td>
      <td>98</td>
      <td>0</td>
      <td>330</td>
    </tr>
    <tr>
      <th>223</th>
      <td>CLINICA DT</td>
      <td>PEDIATRIA</td>
      <td>MEDICO TDC</td>
      <td>251</td>
      <td>0</td>
      <td>68</td>
      <td>0</td>
      <td>323</td>
    </tr>
    <tr>
      <th>224</th>
      <td>CLINICA DT</td>
      <td>PEDIATRIA</td>
      <td>MEDICO VDS</td>
      <td>266</td>
      <td>29</td>
      <td>71</td>
      <td>0</td>
      <td>367</td>
    </tr>
    <tr>
      <th>225</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>33138</td>
      <td>1441</td>
      <td>17917</td>
      <td>1410</td>
      <td>54872</td>
    </tr>
  </tbody>
</table>
<p>226 rows × 8 columns</p>
</div>




```python
faltas_clean = faltas_clean.dropna()
faltas_clean.isnull().sum()
```




    Unidade                 0
    Especialidade           0
    Profissional            0
    Consultas Efetivadas    0
    Faltas Médicas          0
    Faltas Paciente         0
    Remarcações Médicas     0
    Total de Consultas      0
    dtype: int64




```python
faltas_clean = faltas_clean.reset_index(drop=True)
faltas_clean
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unidade</th>
      <th>Especialidade</th>
      <th>Profissional</th>
      <th>Consultas Efetivadas</th>
      <th>Faltas Médicas</th>
      <th>Faltas Paciente</th>
      <th>Remarcações Médicas</th>
      <th>Total de Consultas</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>CLINICA JA</td>
      <td>CLINICO GERAL</td>
      <td>MEDICO CDS</td>
      <td>102</td>
      <td>0</td>
      <td>73</td>
      <td>0</td>
      <td>201</td>
    </tr>
    <tr>
      <th>1</th>
      <td>CLINICA JA</td>
      <td>CLINICO GERAL</td>
      <td>MEDICO HPD</td>
      <td>404</td>
      <td>30</td>
      <td>249</td>
      <td>0</td>
      <td>683</td>
    </tr>
    <tr>
      <th>2</th>
      <td>CLINICA JA</td>
      <td>CLINICO GERAL</td>
      <td>MEDICO JPS</td>
      <td>195</td>
      <td>0</td>
      <td>170</td>
      <td>0</td>
      <td>365</td>
    </tr>
    <tr>
      <th>3</th>
      <td>CLINICA JA</td>
      <td>CLINICO GERAL</td>
      <td>MEDICO TMP</td>
      <td>614</td>
      <td>79</td>
      <td>404</td>
      <td>34</td>
      <td>1133</td>
    </tr>
    <tr>
      <th>4</th>
      <td>CLINICA JA</td>
      <td>DERMATOLOGIA CLINICA E CIRURGICA</td>
      <td>MEDICO BSG</td>
      <td>347</td>
      <td>26</td>
      <td>296</td>
      <td>93</td>
      <td>763</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>171</th>
      <td>CLINICA DT</td>
      <td>PEDIATRIA</td>
      <td>MEDICO LFS</td>
      <td>274</td>
      <td>51</td>
      <td>90</td>
      <td>17</td>
      <td>444</td>
    </tr>
    <tr>
      <th>172</th>
      <td>CLINICA DT</td>
      <td>PEDIATRIA</td>
      <td>MEDICO RAD</td>
      <td>86</td>
      <td>44</td>
      <td>42</td>
      <td>0</td>
      <td>173</td>
    </tr>
    <tr>
      <th>173</th>
      <td>CLINICA DT</td>
      <td>PEDIATRIA</td>
      <td>MEDICO SVR</td>
      <td>215</td>
      <td>17</td>
      <td>98</td>
      <td>0</td>
      <td>330</td>
    </tr>
    <tr>
      <th>174</th>
      <td>CLINICA DT</td>
      <td>PEDIATRIA</td>
      <td>MEDICO TDC</td>
      <td>251</td>
      <td>0</td>
      <td>68</td>
      <td>0</td>
      <td>323</td>
    </tr>
    <tr>
      <th>175</th>
      <td>CLINICA DT</td>
      <td>PEDIATRIA</td>
      <td>MEDICO VDS</td>
      <td>266</td>
      <td>29</td>
      <td>71</td>
      <td>0</td>
      <td>367</td>
    </tr>
  </tbody>
</table>
<p>176 rows × 8 columns</p>
</div>




```python
faltas_clean['Especialidade'].unique()
```




    array(['CLINICO GERAL', 'DERMATOLOGIA CLINICA E CIRURGICA', 'PEDIATRIA',
           'ANESTESIOLOGIA', 'ANGIOLOGIA/CIRUR VASCULAR', 'CARDIOLOGIA',
           'CIRURGIA GERAL', 'CIRURGIA ONCOLOGICA', 'CIRURGIA PEDIATRICA',
           'GASTROENTEROLOGIA', 'GINECOLOGIA CLINICA', 'MASTOLOGIA',
           'NEUROLOGIA', 'ONCOLOGIA CLINICA/QUIMIOTERAPIA',
           'OTORRINOLARINGOLOGIA', 'PROCTOLOGIA', 'UROLOGIA',
           'CIRURGIA GINECOLOGICA', 'CIRURGIA TORACICA', 'NEUROCIRURGIA',
           'OBSTETRICIA / PRE NATAL', 'ONCOLOGIA PEDIATRICA',
           'ORTOPEDIA E TRAUMATOLOGIA', 'CIRURGIA BUCO MAXILO FACIAL',
           'CIRURGIA DE CABECA E PESCOCO'], dtype=object)




```python
faltas_clean[faltas_clean.duplicated(subset = ['Unidade', 'Profissional'], keep = False)].sort_values(by = 'Profissional')
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unidade</th>
      <th>Especialidade</th>
      <th>Profissional</th>
      <th>Consultas Efetivadas</th>
      <th>Faltas Médicas</th>
      <th>Faltas Paciente</th>
      <th>Remarcações Médicas</th>
      <th>Total de Consultas</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>151</th>
      <td>CLINICA DT</td>
      <td>ORTOPEDIA E TRAUMATOLOGIA</td>
      <td>MEDICO AFL</td>
      <td>63</td>
      <td>0</td>
      <td>21</td>
      <td>0</td>
      <td>84</td>
    </tr>
    <tr>
      <th>123</th>
      <td>CLINICA DT</td>
      <td>CLINICO GERAL</td>
      <td>MEDICO AFL</td>
      <td>469</td>
      <td>1</td>
      <td>212</td>
      <td>8</td>
      <td>690</td>
    </tr>
    <tr>
      <th>83</th>
      <td>CLINICA SL</td>
      <td>NEUROCIRURGIA</td>
      <td>MEDICO DAF</td>
      <td>39</td>
      <td>8</td>
      <td>7</td>
      <td>0</td>
      <td>54</td>
    </tr>
    <tr>
      <th>88</th>
      <td>CLINICA SL</td>
      <td>NEUROLOGIA</td>
      <td>MEDICO DAF</td>
      <td>37</td>
      <td>21</td>
      <td>17</td>
      <td>0</td>
      <td>75</td>
    </tr>
    <tr>
      <th>89</th>
      <td>CLINICA SL</td>
      <td>NEUROLOGIA</td>
      <td>MEDICO JAP</td>
      <td>73</td>
      <td>31</td>
      <td>38</td>
      <td>0</td>
      <td>143</td>
    </tr>
    <tr>
      <th>84</th>
      <td>CLINICA SL</td>
      <td>NEUROCIRURGIA</td>
      <td>MEDICO JAP</td>
      <td>31</td>
      <td>0</td>
      <td>17</td>
      <td>0</td>
      <td>70</td>
    </tr>
    <tr>
      <th>92</th>
      <td>CLINICA SL</td>
      <td>NEUROLOGIA</td>
      <td>MEDICO MRF</td>
      <td>69</td>
      <td>0</td>
      <td>49</td>
      <td>0</td>
      <td>119</td>
    </tr>
    <tr>
      <th>85</th>
      <td>CLINICA SL</td>
      <td>NEUROCIRURGIA</td>
      <td>MEDICO MRF</td>
      <td>63</td>
      <td>0</td>
      <td>15</td>
      <td>0</td>
      <td>78</td>
    </tr>
    <tr>
      <th>98</th>
      <td>CLINICA SL</td>
      <td>OBSTETRICIA / PRE NATAL</td>
      <td>MEDICO MVP</td>
      <td>122</td>
      <td>0</td>
      <td>17</td>
      <td>0</td>
      <td>141</td>
    </tr>
    <tr>
      <th>68</th>
      <td>CLINICA SL</td>
      <td>CIRURGIA GINECOLOGICA</td>
      <td>MEDICO MVP</td>
      <td>148</td>
      <td>0</td>
      <td>46</td>
      <td>0</td>
      <td>198</td>
    </tr>
    <tr>
      <th>100</th>
      <td>CLINICA SL</td>
      <td>OBSTETRICIA / PRE NATAL</td>
      <td>MEDICO RAC</td>
      <td>23</td>
      <td>0</td>
      <td>5</td>
      <td>0</td>
      <td>28</td>
    </tr>
    <tr>
      <th>80</th>
      <td>CLINICA SL</td>
      <td>GINECOLOGIA CLINICA</td>
      <td>MEDICO RAC</td>
      <td>27</td>
      <td>0</td>
      <td>12</td>
      <td>0</td>
      <td>39</td>
    </tr>
    <tr>
      <th>86</th>
      <td>CLINICA SL</td>
      <td>NEUROCIRURGIA</td>
      <td>MEDICO TTS</td>
      <td>63</td>
      <td>0</td>
      <td>30</td>
      <td>0</td>
      <td>94</td>
    </tr>
    <tr>
      <th>94</th>
      <td>CLINICA SL</td>
      <td>NEUROLOGIA</td>
      <td>MEDICO TTS</td>
      <td>81</td>
      <td>0</td>
      <td>41</td>
      <td>0</td>
      <td>124</td>
    </tr>
    <tr>
      <th>133</th>
      <td>CLINICA DT</td>
      <td>DERMATOLOGIA CLINICA E CIRURGICA</td>
      <td>MEDICO WFA</td>
      <td>106</td>
      <td>1</td>
      <td>21</td>
      <td>0</td>
      <td>131</td>
    </tr>
    <tr>
      <th>132</th>
      <td>CLINICA DT</td>
      <td>DERMATOLOGIA CLINICA E CIRURGICA</td>
      <td>MEDICO WFA</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>39</td>
    </tr>
    <tr>
      <th>87</th>
      <td>CLINICA SL</td>
      <td>NEUROCIRURGIA</td>
      <td>MEDICO WJS</td>
      <td>29</td>
      <td>0</td>
      <td>11</td>
      <td>0</td>
      <td>40</td>
    </tr>
    <tr>
      <th>95</th>
      <td>CLINICA SL</td>
      <td>NEUROLOGIA</td>
      <td>MEDICO WJS</td>
      <td>66</td>
      <td>0</td>
      <td>35</td>
      <td>0</td>
      <td>102</td>
    </tr>
  </tbody>
</table>
</div>




```python
faltas_clean.loc[(faltas_clean['Especialidade'] == 'ORTOPEDIA E TRAUMATOLOGIA') & (faltas_clean['Profissional'] == 'MEDICO AFL'), 'Profissional'] = 'MEDICO AFLJ'

```


```python
faltas_clean[faltas_clean.duplicated(subset = ['Unidade', 'Profissional'], keep = False)].sort_values(by = 'Profissional')
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unidade</th>
      <th>Especialidade</th>
      <th>Profissional</th>
      <th>Consultas Efetivadas</th>
      <th>Faltas Médicas</th>
      <th>Faltas Paciente</th>
      <th>Remarcações Médicas</th>
      <th>Total de Consultas</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>83</th>
      <td>CLINICA SL</td>
      <td>NEUROCIRURGIA</td>
      <td>MEDICO DAF</td>
      <td>39</td>
      <td>8</td>
      <td>7</td>
      <td>0</td>
      <td>54</td>
    </tr>
    <tr>
      <th>88</th>
      <td>CLINICA SL</td>
      <td>NEUROLOGIA</td>
      <td>MEDICO DAF</td>
      <td>37</td>
      <td>21</td>
      <td>17</td>
      <td>0</td>
      <td>75</td>
    </tr>
    <tr>
      <th>84</th>
      <td>CLINICA SL</td>
      <td>NEUROCIRURGIA</td>
      <td>MEDICO JAP</td>
      <td>31</td>
      <td>0</td>
      <td>17</td>
      <td>0</td>
      <td>70</td>
    </tr>
    <tr>
      <th>89</th>
      <td>CLINICA SL</td>
      <td>NEUROLOGIA</td>
      <td>MEDICO JAP</td>
      <td>73</td>
      <td>31</td>
      <td>38</td>
      <td>0</td>
      <td>143</td>
    </tr>
    <tr>
      <th>85</th>
      <td>CLINICA SL</td>
      <td>NEUROCIRURGIA</td>
      <td>MEDICO MRF</td>
      <td>63</td>
      <td>0</td>
      <td>15</td>
      <td>0</td>
      <td>78</td>
    </tr>
    <tr>
      <th>92</th>
      <td>CLINICA SL</td>
      <td>NEUROLOGIA</td>
      <td>MEDICO MRF</td>
      <td>69</td>
      <td>0</td>
      <td>49</td>
      <td>0</td>
      <td>119</td>
    </tr>
    <tr>
      <th>68</th>
      <td>CLINICA SL</td>
      <td>CIRURGIA GINECOLOGICA</td>
      <td>MEDICO MVP</td>
      <td>148</td>
      <td>0</td>
      <td>46</td>
      <td>0</td>
      <td>198</td>
    </tr>
    <tr>
      <th>98</th>
      <td>CLINICA SL</td>
      <td>OBSTETRICIA / PRE NATAL</td>
      <td>MEDICO MVP</td>
      <td>122</td>
      <td>0</td>
      <td>17</td>
      <td>0</td>
      <td>141</td>
    </tr>
    <tr>
      <th>80</th>
      <td>CLINICA SL</td>
      <td>GINECOLOGIA CLINICA</td>
      <td>MEDICO RAC</td>
      <td>27</td>
      <td>0</td>
      <td>12</td>
      <td>0</td>
      <td>39</td>
    </tr>
    <tr>
      <th>100</th>
      <td>CLINICA SL</td>
      <td>OBSTETRICIA / PRE NATAL</td>
      <td>MEDICO RAC</td>
      <td>23</td>
      <td>0</td>
      <td>5</td>
      <td>0</td>
      <td>28</td>
    </tr>
    <tr>
      <th>86</th>
      <td>CLINICA SL</td>
      <td>NEUROCIRURGIA</td>
      <td>MEDICO TTS</td>
      <td>63</td>
      <td>0</td>
      <td>30</td>
      <td>0</td>
      <td>94</td>
    </tr>
    <tr>
      <th>94</th>
      <td>CLINICA SL</td>
      <td>NEUROLOGIA</td>
      <td>MEDICO TTS</td>
      <td>81</td>
      <td>0</td>
      <td>41</td>
      <td>0</td>
      <td>124</td>
    </tr>
    <tr>
      <th>132</th>
      <td>CLINICA DT</td>
      <td>DERMATOLOGIA CLINICA E CIRURGICA</td>
      <td>MEDICO WFA</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>39</td>
    </tr>
    <tr>
      <th>133</th>
      <td>CLINICA DT</td>
      <td>DERMATOLOGIA CLINICA E CIRURGICA</td>
      <td>MEDICO WFA</td>
      <td>106</td>
      <td>1</td>
      <td>21</td>
      <td>0</td>
      <td>131</td>
    </tr>
    <tr>
      <th>87</th>
      <td>CLINICA SL</td>
      <td>NEUROCIRURGIA</td>
      <td>MEDICO WJS</td>
      <td>29</td>
      <td>0</td>
      <td>11</td>
      <td>0</td>
      <td>40</td>
    </tr>
    <tr>
      <th>95</th>
      <td>CLINICA SL</td>
      <td>NEUROLOGIA</td>
      <td>MEDICO WJS</td>
      <td>66</td>
      <td>0</td>
      <td>35</td>
      <td>0</td>
      <td>102</td>
    </tr>
  </tbody>
</table>
</div>




```python
faltas_clean[faltas_clean.duplicated(subset = ['Unidade', 'Especialidade','Profissional'], keep = False)].sort_values(by ='Profissional')
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unidade</th>
      <th>Especialidade</th>
      <th>Profissional</th>
      <th>Consultas Efetivadas</th>
      <th>Faltas Médicas</th>
      <th>Faltas Paciente</th>
      <th>Remarcações Médicas</th>
      <th>Total de Consultas</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>132</th>
      <td>CLINICA DT</td>
      <td>DERMATOLOGIA CLINICA E CIRURGICA</td>
      <td>MEDICO WFA</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>39</td>
    </tr>
    <tr>
      <th>133</th>
      <td>CLINICA DT</td>
      <td>DERMATOLOGIA CLINICA E CIRURGICA</td>
      <td>MEDICO WFA</td>
      <td>106</td>
      <td>1</td>
      <td>21</td>
      <td>0</td>
      <td>131</td>
    </tr>
  </tbody>
</table>
</div>




```python
faltas_clean = faltas_clean.groupby(['Unidade', 'Especialidade', 'Profissional'], as_index =False).sum()
```


```python
faltas_clean[faltas_clean.duplicated(subset = ['Unidade', 'Especialidade','Profissional'], keep = False)].sort_values(by ='Profissional')
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unidade</th>
      <th>Especialidade</th>
      <th>Profissional</th>
      <th>Consultas Efetivadas</th>
      <th>Faltas Médicas</th>
      <th>Faltas Paciente</th>
      <th>Remarcações Médicas</th>
      <th>Total de Consultas</th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>
</div>




```python
# limpeza faltas_clean concluída
faltas_clean
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unidade</th>
      <th>Especialidade</th>
      <th>Profissional</th>
      <th>Consultas Efetivadas</th>
      <th>Faltas Médicas</th>
      <th>Faltas Paciente</th>
      <th>Remarcações Médicas</th>
      <th>Total de Consultas</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>CLINICA JA</td>
      <td>CLINICO GERAL</td>
      <td>MEDICO CDS</td>
      <td>102</td>
      <td>0</td>
      <td>73</td>
      <td>0</td>
      <td>201</td>
    </tr>
    <tr>
      <th>1</th>
      <td>CLINICA JA</td>
      <td>CLINICO GERAL</td>
      <td>MEDICO HPD</td>
      <td>404</td>
      <td>30</td>
      <td>249</td>
      <td>0</td>
      <td>683</td>
    </tr>
    <tr>
      <th>2</th>
      <td>CLINICA JA</td>
      <td>CLINICO GERAL</td>
      <td>MEDICO JPS</td>
      <td>195</td>
      <td>0</td>
      <td>170</td>
      <td>0</td>
      <td>365</td>
    </tr>
    <tr>
      <th>3</th>
      <td>CLINICA JA</td>
      <td>CLINICO GERAL</td>
      <td>MEDICO TMP</td>
      <td>614</td>
      <td>79</td>
      <td>404</td>
      <td>34</td>
      <td>1133</td>
    </tr>
    <tr>
      <th>4</th>
      <td>CLINICA JA</td>
      <td>DERMATOLOGIA CLINICA E CIRURGICA</td>
      <td>MEDICO BSG</td>
      <td>347</td>
      <td>26</td>
      <td>296</td>
      <td>93</td>
      <td>763</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>171</th>
      <td>CLINICA DT</td>
      <td>PEDIATRIA</td>
      <td>MEDICO LFS</td>
      <td>274</td>
      <td>51</td>
      <td>90</td>
      <td>17</td>
      <td>444</td>
    </tr>
    <tr>
      <th>172</th>
      <td>CLINICA DT</td>
      <td>PEDIATRIA</td>
      <td>MEDICO RAD</td>
      <td>86</td>
      <td>44</td>
      <td>42</td>
      <td>0</td>
      <td>173</td>
    </tr>
    <tr>
      <th>173</th>
      <td>CLINICA DT</td>
      <td>PEDIATRIA</td>
      <td>MEDICO SVR</td>
      <td>215</td>
      <td>17</td>
      <td>98</td>
      <td>0</td>
      <td>330</td>
    </tr>
    <tr>
      <th>174</th>
      <td>CLINICA DT</td>
      <td>PEDIATRIA</td>
      <td>MEDICO TDC</td>
      <td>251</td>
      <td>0</td>
      <td>68</td>
      <td>0</td>
      <td>323</td>
    </tr>
    <tr>
      <th>175</th>
      <td>CLINICA DT</td>
      <td>PEDIATRIA</td>
      <td>MEDICO VDS</td>
      <td>266</td>
      <td>29</td>
      <td>71</td>
      <td>0</td>
      <td>367</td>
    </tr>
  </tbody>
</table>
<p>176 rows × 8 columns</p>
</div>




```python
prod
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>UNIDADE</th>
      <th>ESPECIALIDADES</th>
      <th>MEDICO</th>
      <th>Qtd. Consultas</th>
      <th>Qtd. Retorno</th>
      <th>Atendimento Geral</th>
      <th>Qtd. Horas</th>
      <th>Produtividade</th>
      <th>Meta</th>
      <th>Qtd. Consultas.1</th>
      <th>...</th>
      <th>Atendimento Geral.24</th>
      <th>Qtd. Horas.24</th>
      <th>Produtividade.24</th>
      <th>Meta.24</th>
      <th>Qtd. Consultas.25</th>
      <th>Qtd. Retorno.25</th>
      <th>Atendimento Geral.25</th>
      <th>Qtd. Horas.25</th>
      <th>Produtividade.25</th>
      <th>Meta.25</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>179.0</td>
      <td>14.0</td>
      <td>193.0</td>
      <td>29.831667</td>
      <td>6.47</td>
      <td>5.5</td>
      <td>1654.0</td>
      <td>...</td>
      <td>89.0</td>
      <td>18.235</td>
      <td>4.88</td>
      <td>5.5</td>
      <td>29619</td>
      <td>3131</td>
      <td>32750</td>
      <td>5617.094722</td>
      <td>5.83</td>
      <td>5.5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Total</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>179.0</td>
      <td>14.0</td>
      <td>193.0</td>
      <td>29.831667</td>
      <td>6.47</td>
      <td>5.5</td>
      <td>1261.0</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>20136</td>
      <td>1915</td>
      <td>22051</td>
      <td>3621.978333</td>
      <td>6.09</td>
      <td>5.5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>CLINICA JA</td>
      <td>Total</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>321.0</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>3973</td>
      <td>360</td>
      <td>4333</td>
      <td>648.283611</td>
      <td>6.68</td>
      <td>5.5</td>
    </tr>
    <tr>
      <th>3</th>
      <td>CLINICA JA</td>
      <td>CLINICO GERAL</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>128.0</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1138</td>
      <td>177</td>
      <td>1315</td>
      <td>134.781111</td>
      <td>9.76</td>
      <td>5.5</td>
    </tr>
    <tr>
      <th>4</th>
      <td>CLINICA JA</td>
      <td>CLINICO GERAL</td>
      <td>MEDICO CDS</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>36.0</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>98</td>
      <td>4</td>
      <td>102</td>
      <td>10.565278</td>
      <td>9.65</td>
      <td>5.5</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>209</th>
      <td>CLINICA DT</td>
      <td>PEDIATRIA</td>
      <td>MEDICO RAD</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>86</td>
      <td>0</td>
      <td>86</td>
      <td>15.692500</td>
      <td>5.48</td>
      <td>5.5</td>
    </tr>
    <tr>
      <th>210</th>
      <td>CLINICA DT</td>
      <td>PEDIATRIA</td>
      <td>MEDICO SVR</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>206</td>
      <td>9</td>
      <td>215</td>
      <td>55.434444</td>
      <td>3.88</td>
      <td>5.5</td>
    </tr>
    <tr>
      <th>211</th>
      <td>CLINICA DT</td>
      <td>PEDIATRIA</td>
      <td>MEDICO TDC</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>27.0</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>235</td>
      <td>16</td>
      <td>251</td>
      <td>50.071667</td>
      <td>5.01</td>
      <td>5.5</td>
    </tr>
    <tr>
      <th>212</th>
      <td>CLINICA DT</td>
      <td>PEDIATRIA</td>
      <td>MEDICO VDS</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>241</td>
      <td>25</td>
      <td>266</td>
      <td>57.236111</td>
      <td>4.65</td>
      <td>5.5</td>
    </tr>
    <tr>
      <th>213</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>179.0</td>
      <td>14.0</td>
      <td>193.0</td>
      <td>29.831667</td>
      <td>6.47</td>
      <td>5.5</td>
      <td>1654.0</td>
      <td>...</td>
      <td>89.0</td>
      <td>18.235</td>
      <td>4.88</td>
      <td>5.5</td>
      <td>29619</td>
      <td>3131</td>
      <td>32750</td>
      <td>5617.094722</td>
      <td>5.83</td>
      <td>5.5</td>
    </tr>
  </tbody>
</table>
<p>214 rows × 159 columns</p>
</div>




```python
prod = prod[['UNIDADE', 'ESPECIALIDADES', 'MEDICO','Atendimento Geral.25','Qtd. Horas.25']]
prod
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>UNIDADE</th>
      <th>ESPECIALIDADES</th>
      <th>MEDICO</th>
      <th>Atendimento Geral.25</th>
      <th>Qtd. Horas.25</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>32750</td>
      <td>5617.094722</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Total</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>22051</td>
      <td>3621.978333</td>
    </tr>
    <tr>
      <th>2</th>
      <td>CLINICA JA</td>
      <td>Total</td>
      <td>NaN</td>
      <td>4333</td>
      <td>648.283611</td>
    </tr>
    <tr>
      <th>3</th>
      <td>CLINICA JA</td>
      <td>CLINICO GERAL</td>
      <td>NaN</td>
      <td>1315</td>
      <td>134.781111</td>
    </tr>
    <tr>
      <th>4</th>
      <td>CLINICA JA</td>
      <td>CLINICO GERAL</td>
      <td>MEDICO CDS</td>
      <td>102</td>
      <td>10.565278</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>209</th>
      <td>CLINICA DT</td>
      <td>PEDIATRIA</td>
      <td>MEDICO RAD</td>
      <td>86</td>
      <td>15.692500</td>
    </tr>
    <tr>
      <th>210</th>
      <td>CLINICA DT</td>
      <td>PEDIATRIA</td>
      <td>MEDICO SVR</td>
      <td>215</td>
      <td>55.434444</td>
    </tr>
    <tr>
      <th>211</th>
      <td>CLINICA DT</td>
      <td>PEDIATRIA</td>
      <td>MEDICO TDC</td>
      <td>251</td>
      <td>50.071667</td>
    </tr>
    <tr>
      <th>212</th>
      <td>CLINICA DT</td>
      <td>PEDIATRIA</td>
      <td>MEDICO VDS</td>
      <td>266</td>
      <td>57.236111</td>
    </tr>
    <tr>
      <th>213</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>32750</td>
      <td>5617.094722</td>
    </tr>
  </tbody>
</table>
<p>214 rows × 5 columns</p>
</div>




```python
prod = prod.rename(columns = {
    'UNIDADE': 'Unidade',
    'ESPECIALIDADES': 'Especialidade',
    'MEDICO': 'Profissional',
    'Atendimento Geral.25' : 'Atendimento Produtividade',
    'Qtd. Horas.25' : 'Quantidade Horas Produtividade'
})
prod
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unidade</th>
      <th>Especialidade</th>
      <th>Profissional</th>
      <th>Atendimento Produtividade</th>
      <th>Quantidade Horas Produtividade</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>32750</td>
      <td>5617.094722</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Total</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>22051</td>
      <td>3621.978333</td>
    </tr>
    <tr>
      <th>2</th>
      <td>CLINICA JA</td>
      <td>Total</td>
      <td>NaN</td>
      <td>4333</td>
      <td>648.283611</td>
    </tr>
    <tr>
      <th>3</th>
      <td>CLINICA JA</td>
      <td>CLINICO GERAL</td>
      <td>NaN</td>
      <td>1315</td>
      <td>134.781111</td>
    </tr>
    <tr>
      <th>4</th>
      <td>CLINICA JA</td>
      <td>CLINICO GERAL</td>
      <td>MEDICO CDS</td>
      <td>102</td>
      <td>10.565278</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>209</th>
      <td>CLINICA DT</td>
      <td>PEDIATRIA</td>
      <td>MEDICO RAD</td>
      <td>86</td>
      <td>15.692500</td>
    </tr>
    <tr>
      <th>210</th>
      <td>CLINICA DT</td>
      <td>PEDIATRIA</td>
      <td>MEDICO SVR</td>
      <td>215</td>
      <td>55.434444</td>
    </tr>
    <tr>
      <th>211</th>
      <td>CLINICA DT</td>
      <td>PEDIATRIA</td>
      <td>MEDICO TDC</td>
      <td>251</td>
      <td>50.071667</td>
    </tr>
    <tr>
      <th>212</th>
      <td>CLINICA DT</td>
      <td>PEDIATRIA</td>
      <td>MEDICO VDS</td>
      <td>266</td>
      <td>57.236111</td>
    </tr>
    <tr>
      <th>213</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>32750</td>
      <td>5617.094722</td>
    </tr>
  </tbody>
</table>
<p>214 rows × 5 columns</p>
</div>




```python
prod_clean = prod.dropna()
prod_clean.isnull().sum()
```




    Unidade                           0
    Especialidade                     0
    Profissional                      0
    Atendimento Produtividade         0
    Quantidade Horas Produtividade    0
    dtype: int64




```python
prod_clean.loc[(prod_clean['Especialidade'] == 'ORTOPEDIA E TRAUMATOLOGIA') & (prod_clean['Profissional'] == 'MEDICO AFL'), 'Profissional'] = 'MEDICO AFLJ'
prod_clean.reset_index(drop=True)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unidade</th>
      <th>Especialidade</th>
      <th>Profissional</th>
      <th>Atendimento Produtividade</th>
      <th>Quantidade Horas Produtividade</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>CLINICA JA</td>
      <td>CLINICO GERAL</td>
      <td>MEDICO CDS</td>
      <td>102</td>
      <td>10.565278</td>
    </tr>
    <tr>
      <th>1</th>
      <td>CLINICA JA</td>
      <td>CLINICO GERAL</td>
      <td>MEDICO HPD</td>
      <td>404</td>
      <td>35.775833</td>
    </tr>
    <tr>
      <th>2</th>
      <td>CLINICA JA</td>
      <td>CLINICO GERAL</td>
      <td>MEDICO JPS</td>
      <td>195</td>
      <td>25.015833</td>
    </tr>
    <tr>
      <th>3</th>
      <td>CLINICA JA</td>
      <td>CLINICO GERAL</td>
      <td>MEDICO TMP</td>
      <td>614</td>
      <td>63.424167</td>
    </tr>
    <tr>
      <th>4</th>
      <td>CLINICA JA</td>
      <td>DERMATOLOGIA CLINICA E CIRURGICA</td>
      <td>MEDICO BSG</td>
      <td>346</td>
      <td>32.639722</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>162</th>
      <td>CLINICA DT</td>
      <td>PEDIATRIA</td>
      <td>MEDICO LFS</td>
      <td>272</td>
      <td>81.645278</td>
    </tr>
    <tr>
      <th>163</th>
      <td>CLINICA DT</td>
      <td>PEDIATRIA</td>
      <td>MEDICO RAD</td>
      <td>86</td>
      <td>15.692500</td>
    </tr>
    <tr>
      <th>164</th>
      <td>CLINICA DT</td>
      <td>PEDIATRIA</td>
      <td>MEDICO SVR</td>
      <td>215</td>
      <td>55.434444</td>
    </tr>
    <tr>
      <th>165</th>
      <td>CLINICA DT</td>
      <td>PEDIATRIA</td>
      <td>MEDICO TDC</td>
      <td>251</td>
      <td>50.071667</td>
    </tr>
    <tr>
      <th>166</th>
      <td>CLINICA DT</td>
      <td>PEDIATRIA</td>
      <td>MEDICO VDS</td>
      <td>266</td>
      <td>57.236111</td>
    </tr>
  </tbody>
</table>
<p>167 rows × 5 columns</p>
</div>




```python
prod_clean['Especialidade'].unique()
```




    array(['CLINICO GERAL', 'DERMATOLOGIA CLINICA E CIRURGICA', 'PEDIATRIA',
           'ANESTESIOLOGIA', 'ANGIOLOGIA/CIRUR VASCULAR', 'CARDIOLOGIA',
           'CIRURGIA GERAL', 'CIRURGIA PEDIATRICA', 'GASTROENTEROLOGIA',
           'GINECOLOGIA CLINICA', 'MASTOLOGIA', 'NEUROLOGIA',
           'OTORRINOLARINGOLOGIA', 'PROCTOLOGIA', 'UROLOGIA',
           'CIRURGIA GINECOLOGICA', 'NEUROCIRURGIA',
           'OBSTETRICIA / PRE NATAL', 'ORTOPEDIA E TRAUMATOLOGIA',
           'CIRURGIA BUCO MAXILO FACIAL', 'CIRURGIA DE CABECA E PESCOCO',
           'CIRURGIA TORACICA'], dtype=object)




```python
prod_clean[prod_clean.duplicated(subset=['Unidade','Profissional'], keep=False)].sort_values(by = 'Profissional')
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unidade</th>
      <th>Especialidade</th>
      <th>Profissional</th>
      <th>Atendimento Produtividade</th>
      <th>Quantidade Horas Produtividade</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>106</th>
      <td>CLINICA SL</td>
      <td>NEUROCIRURGIA</td>
      <td>MEDICO DAF</td>
      <td>39</td>
      <td>3.169722</td>
    </tr>
    <tr>
      <th>112</th>
      <td>CLINICA SL</td>
      <td>NEUROLOGIA</td>
      <td>MEDICO DAF</td>
      <td>37</td>
      <td>6.821111</td>
    </tr>
    <tr>
      <th>107</th>
      <td>CLINICA SL</td>
      <td>NEUROCIRURGIA</td>
      <td>MEDICO JAP</td>
      <td>31</td>
      <td>3.958889</td>
    </tr>
    <tr>
      <th>113</th>
      <td>CLINICA SL</td>
      <td>NEUROLOGIA</td>
      <td>MEDICO JAP</td>
      <td>73</td>
      <td>8.685000</td>
    </tr>
    <tr>
      <th>108</th>
      <td>CLINICA SL</td>
      <td>NEUROCIRURGIA</td>
      <td>MEDICO MRF</td>
      <td>63</td>
      <td>5.450278</td>
    </tr>
    <tr>
      <th>116</th>
      <td>CLINICA SL</td>
      <td>NEUROLOGIA</td>
      <td>MEDICO MRF</td>
      <td>69</td>
      <td>6.539722</td>
    </tr>
    <tr>
      <th>88</th>
      <td>CLINICA SL</td>
      <td>CIRURGIA GINECOLOGICA</td>
      <td>MEDICO MVP</td>
      <td>148</td>
      <td>28.678889</td>
    </tr>
    <tr>
      <th>123</th>
      <td>CLINICA SL</td>
      <td>OBSTETRICIA / PRE NATAL</td>
      <td>MEDICO MVP</td>
      <td>122</td>
      <td>20.226389</td>
    </tr>
    <tr>
      <th>102</th>
      <td>CLINICA SL</td>
      <td>GINECOLOGIA CLINICA</td>
      <td>MEDICO RAC</td>
      <td>27</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>125</th>
      <td>CLINICA SL</td>
      <td>OBSTETRICIA / PRE NATAL</td>
      <td>MEDICO RAC</td>
      <td>23</td>
      <td>8.311667</td>
    </tr>
    <tr>
      <th>109</th>
      <td>CLINICA SL</td>
      <td>NEUROCIRURGIA</td>
      <td>MEDICO TTS</td>
      <td>63</td>
      <td>7.404722</td>
    </tr>
    <tr>
      <th>118</th>
      <td>CLINICA SL</td>
      <td>NEUROLOGIA</td>
      <td>MEDICO TTS</td>
      <td>81</td>
      <td>11.211667</td>
    </tr>
    <tr>
      <th>110</th>
      <td>CLINICA SL</td>
      <td>NEUROCIRURGIA</td>
      <td>MEDICO WJS</td>
      <td>29</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>119</th>
      <td>CLINICA SL</td>
      <td>NEUROLOGIA</td>
      <td>MEDICO WJS</td>
      <td>66</td>
      <td>10.533611</td>
    </tr>
  </tbody>
</table>
</div>




```python
prod_clean[prod_clean.duplicated(subset = ['Unidade', 'Especialidade','Profissional'], keep = False)].sort_values(by ='Profissional')
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unidade</th>
      <th>Especialidade</th>
      <th>Profissional</th>
      <th>Atendimento Produtividade</th>
      <th>Quantidade Horas Produtividade</th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>
</div>




```python
#prod_clean finalizado
```


```python
espera
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unidade</th>
      <th>Especialidade</th>
      <th>Médico</th>
      <th>% PCTE &gt; 30 MIN</th>
      <th>QTDE PCTE &gt; 30</th>
      <th>QTDE USUARIOS</th>
      <th>% PCTE &gt; 30 MIN.1</th>
      <th>QTDE PCTE &gt; 30.1</th>
      <th>QTDE USUARIOS.1</th>
      <th>% PCTE &gt; 30 MIN.2</th>
      <th>...</th>
      <th>QTDE USUARIOS.22</th>
      <th>% PCTE &gt; 30 MIN.23</th>
      <th>QTDE PCTE &gt; 30.23</th>
      <th>QTDE USUARIOS.23</th>
      <th>% PCTE &gt; 30 MIN.24</th>
      <th>QTDE PCTE &gt; 30.24</th>
      <th>QTDE USUARIOS.24</th>
      <th>% PCTE &gt; 30 MIN.25</th>
      <th>QTDE PCTE &gt; 30.25</th>
      <th>QTDE USUARIOS.25</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Total</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.405882</td>
      <td>69.0</td>
      <td>170.0</td>
      <td>0.357973</td>
      <td>431.0</td>
      <td>1204.0</td>
      <td>0.342105</td>
      <td>...</td>
      <td>898.0</td>
      <td>0.287690</td>
      <td>208.0</td>
      <td>723.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.336687</td>
      <td>6626</td>
      <td>19680</td>
    </tr>
    <tr>
      <th>1</th>
      <td>CLINICA JA</td>
      <td>Total</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.448680</td>
      <td>153.0</td>
      <td>341.0</td>
      <td>0.456522</td>
      <td>...</td>
      <td>95.0</td>
      <td>0.392857</td>
      <td>55.0</td>
      <td>140.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.366461</td>
      <td>1604</td>
      <td>4377</td>
    </tr>
    <tr>
      <th>2</th>
      <td>CLINICA JA</td>
      <td>CLINICA MÉDICA</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.100000</td>
      <td>14.0</td>
      <td>140.0</td>
      <td>0.050000</td>
      <td>...</td>
      <td>6.0</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>45.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.057735</td>
      <td>78</td>
      <td>1351</td>
    </tr>
    <tr>
      <th>3</th>
      <td>CLINICA JA</td>
      <td>CLINICA MÉDICA</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>...</td>
      <td>1.0</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>2.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.000000</td>
      <td>0</td>
      <td>25</td>
    </tr>
    <tr>
      <th>4</th>
      <td>CLINICA JA</td>
      <td>CLINICA MÉDICA</td>
      <td>MEDICO AKM</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.500000</td>
      <td>2</td>
      <td>4</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>422</th>
      <td>CLINICA DT</td>
      <td>PEDIATRIA</td>
      <td>MEDICO SMM</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.000000</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>423</th>
      <td>CLINICA DT</td>
      <td>PEDIATRIA</td>
      <td>MEDICO SVR</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.640000</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.737089</td>
      <td>157</td>
      <td>213</td>
    </tr>
    <tr>
      <th>424</th>
      <td>CLINICA DT</td>
      <td>PEDIATRIA</td>
      <td>MEDICO TDC</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.531250</td>
      <td>17.0</td>
      <td>32.0</td>
      <td>NaN</td>
      <td>...</td>
      <td>34.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.598394</td>
      <td>149</td>
      <td>249</td>
    </tr>
    <tr>
      <th>425</th>
      <td>CLINICA DT</td>
      <td>PEDIATRIA</td>
      <td>MEDICO VDS</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>28.0</td>
      <td>0.428571</td>
      <td>15.0</td>
      <td>35.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.319549</td>
      <td>85</td>
      <td>266</td>
    </tr>
    <tr>
      <th>426</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.405882</td>
      <td>69.0</td>
      <td>170.0</td>
      <td>0.320721</td>
      <td>534.0</td>
      <td>1665.0</td>
      <td>0.336182</td>
      <td>...</td>
      <td>1549.0</td>
      <td>0.328583</td>
      <td>415.0</td>
      <td>1263.0</td>
      <td>0.564103</td>
      <td>66.0</td>
      <td>117.0</td>
      <td>0.347708</td>
      <td>10764</td>
      <td>30957</td>
    </tr>
  </tbody>
</table>
<p>427 rows × 81 columns</p>
</div>




```python
espera_clean = espera[['Unidade', 'Especialidade', 'Médico', 'QTDE USUARIOS.25', 'QTDE PCTE > 30.25']]
espera_clean
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unidade</th>
      <th>Especialidade</th>
      <th>Médico</th>
      <th>QTDE USUARIOS.25</th>
      <th>QTDE PCTE &gt; 30.25</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Total</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>19680</td>
      <td>6626</td>
    </tr>
    <tr>
      <th>1</th>
      <td>CLINICA JA</td>
      <td>Total</td>
      <td>NaN</td>
      <td>4377</td>
      <td>1604</td>
    </tr>
    <tr>
      <th>2</th>
      <td>CLINICA JA</td>
      <td>CLINICA MÉDICA</td>
      <td>NaN</td>
      <td>1351</td>
      <td>78</td>
    </tr>
    <tr>
      <th>3</th>
      <td>CLINICA JA</td>
      <td>CLINICA MÉDICA</td>
      <td>NaN</td>
      <td>25</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>CLINICA JA</td>
      <td>CLINICA MÉDICA</td>
      <td>MEDICO AKM</td>
      <td>4</td>
      <td>2</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>422</th>
      <td>CLINICA DT</td>
      <td>PEDIATRIA</td>
      <td>MEDICO SMM</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>423</th>
      <td>CLINICA DT</td>
      <td>PEDIATRIA</td>
      <td>MEDICO SVR</td>
      <td>213</td>
      <td>157</td>
    </tr>
    <tr>
      <th>424</th>
      <td>CLINICA DT</td>
      <td>PEDIATRIA</td>
      <td>MEDICO TDC</td>
      <td>249</td>
      <td>149</td>
    </tr>
    <tr>
      <th>425</th>
      <td>CLINICA DT</td>
      <td>PEDIATRIA</td>
      <td>MEDICO VDS</td>
      <td>266</td>
      <td>85</td>
    </tr>
    <tr>
      <th>426</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>30957</td>
      <td>10764</td>
    </tr>
  </tbody>
</table>
<p>427 rows × 5 columns</p>
</div>




```python
espera_clean = espera_clean.rename(columns = {
    'Médico': 'Profissional',
    'QTDE USUARIOS.25': 'Usuários',
    'QTDE PCTE > 30.25': 'Espera > 30'
    })
espera_clean
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unidade</th>
      <th>Especialidade</th>
      <th>Profissional</th>
      <th>Usuários</th>
      <th>Espera &gt; 30</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Total</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>19680</td>
      <td>6626</td>
    </tr>
    <tr>
      <th>1</th>
      <td>CLINICA JA</td>
      <td>Total</td>
      <td>NaN</td>
      <td>4377</td>
      <td>1604</td>
    </tr>
    <tr>
      <th>2</th>
      <td>CLINICA JA</td>
      <td>CLINICA MÉDICA</td>
      <td>NaN</td>
      <td>1351</td>
      <td>78</td>
    </tr>
    <tr>
      <th>3</th>
      <td>CLINICA JA</td>
      <td>CLINICA MÉDICA</td>
      <td>NaN</td>
      <td>25</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>CLINICA JA</td>
      <td>CLINICA MÉDICA</td>
      <td>MEDICO AKM</td>
      <td>4</td>
      <td>2</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>422</th>
      <td>CLINICA DT</td>
      <td>PEDIATRIA</td>
      <td>MEDICO SMM</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>423</th>
      <td>CLINICA DT</td>
      <td>PEDIATRIA</td>
      <td>MEDICO SVR</td>
      <td>213</td>
      <td>157</td>
    </tr>
    <tr>
      <th>424</th>
      <td>CLINICA DT</td>
      <td>PEDIATRIA</td>
      <td>MEDICO TDC</td>
      <td>249</td>
      <td>149</td>
    </tr>
    <tr>
      <th>425</th>
      <td>CLINICA DT</td>
      <td>PEDIATRIA</td>
      <td>MEDICO VDS</td>
      <td>266</td>
      <td>85</td>
    </tr>
    <tr>
      <th>426</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>30957</td>
      <td>10764</td>
    </tr>
  </tbody>
</table>
<p>427 rows × 5 columns</p>
</div>




```python
espera_clean = espera_clean.dropna()
espera_clean.isnull().sum()
```




    Unidade          0
    Especialidade    0
    Profissional     0
    Usuários         0
    Espera > 30      0
    dtype: int64




```python
espera_clean.loc[(espera_clean['Especialidade'] == 'ORTOPEDIA E TRAUMATOLOGIA') & (espera_clean['Profissional'] == 'MEDICO AFL'), 'Profissional'] = 'MEDICO AFLJ'
```


```python
espera_clean[espera_clean.duplicated(subset=['Unidade','Profissional'], keep=False)].sort_values(by = 'Profissional')
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unidade</th>
      <th>Especialidade</th>
      <th>Profissional</th>
      <th>Usuários</th>
      <th>Espera &gt; 30</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>328</th>
      <td>CLINICA DT</td>
      <td>GINECOLOGIA CLÍNICA</td>
      <td>MEDICO ACD</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>411</th>
      <td>CLINICA DT</td>
      <td>PEDIATRIA</td>
      <td>MEDICO ACD</td>
      <td>451</td>
      <td>382</td>
    </tr>
    <tr>
      <th>297</th>
      <td>CLINICA DT</td>
      <td>CLÍNICA MÉDICA</td>
      <td>MEDICO AFL</td>
      <td>463</td>
      <td>27</td>
    </tr>
    <tr>
      <th>412</th>
      <td>CLINICA DT</td>
      <td>PEDIATRIA</td>
      <td>MEDICO AFL</td>
      <td>2</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>CLINICA JA</td>
      <td>CLINICA MÉDICA</td>
      <td>MEDICO AKM</td>
      <td>4</td>
      <td>2</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>425</th>
      <td>CLINICA DT</td>
      <td>PEDIATRIA</td>
      <td>MEDICO VDS</td>
      <td>266</td>
      <td>85</td>
    </tr>
    <tr>
      <th>324</th>
      <td>CLINICA DT</td>
      <td>DERMATOLOGIA CLÍNICA E CIRÚRGICA</td>
      <td>MEDICO WFA</td>
      <td>106</td>
      <td>1</td>
    </tr>
    <tr>
      <th>323</th>
      <td>CLINICA DT</td>
      <td>DERMATOLOGIA CLÍNICA E CIRÚRGICA</td>
      <td>MEDICO WFA</td>
      <td>15</td>
      <td>0</td>
    </tr>
    <tr>
      <th>246</th>
      <td>CLINICA SL</td>
      <td>NEUROLOGIA</td>
      <td>MEDICO WJS</td>
      <td>45</td>
      <td>32</td>
    </tr>
    <tr>
      <th>234</th>
      <td>CLINICA SL</td>
      <td>NEUROCIRURGIA</td>
      <td>MEDICO WJS</td>
      <td>34</td>
      <td>26</td>
    </tr>
  </tbody>
</table>
<p>300 rows × 5 columns</p>
</div>




```python
espera_clean.groupby(['Unidade', 'Profissional'], as_index =False).sum()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unidade</th>
      <th>Profissional</th>
      <th>Especialidade</th>
      <th>Usuários</th>
      <th>Espera &gt; 30</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>CLINICA DT</td>
      <td>MEDICO AAV</td>
      <td>GINECOLOGIA CLÍNICA</td>
      <td>114</td>
      <td>32</td>
    </tr>
    <tr>
      <th>1</th>
      <td>CLINICA DT</td>
      <td>MEDICO ACD</td>
      <td>GINECOLOGIA CLÍNICAPEDIATRIA</td>
      <td>452</td>
      <td>383</td>
    </tr>
    <tr>
      <th>2</th>
      <td>CLINICA DT</td>
      <td>MEDICO ADC</td>
      <td>GINECOLOGIA CLÍNICA</td>
      <td>91</td>
      <td>69</td>
    </tr>
    <tr>
      <th>3</th>
      <td>CLINICA DT</td>
      <td>MEDICO AFL</td>
      <td>CLÍNICA MÉDICAPEDIATRIA</td>
      <td>465</td>
      <td>27</td>
    </tr>
    <tr>
      <th>4</th>
      <td>CLINICA DT</td>
      <td>MEDICO AFLJ</td>
      <td>ORTOPEDIA E TRAUMATOLOGIA</td>
      <td>63</td>
      <td>18</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>161</th>
      <td>CLINICA SL</td>
      <td>MEDICO TDO</td>
      <td>CLINICA MEDICAGINECOLOGIA</td>
      <td>183</td>
      <td>14</td>
    </tr>
    <tr>
      <th>162</th>
      <td>CLINICA SL</td>
      <td>MEDICO TMP</td>
      <td>CLINICA MEDICA</td>
      <td>221</td>
      <td>58</td>
    </tr>
    <tr>
      <th>163</th>
      <td>CLINICA SL</td>
      <td>MEDICO TTS</td>
      <td>CLINICA MEDICANEUROCIRURGIANEUROLOGIAORTOPEDIA</td>
      <td>119</td>
      <td>19</td>
    </tr>
    <tr>
      <th>164</th>
      <td>CLINICA SL</td>
      <td>MEDICO WAS</td>
      <td>ORTOPEDIA</td>
      <td>37</td>
      <td>17</td>
    </tr>
    <tr>
      <th>165</th>
      <td>CLINICA SL</td>
      <td>MEDICO WJS</td>
      <td>NEUROCIRURGIANEUROLOGIA</td>
      <td>79</td>
      <td>58</td>
    </tr>
  </tbody>
</table>
<p>166 rows × 5 columns</p>
</div>




```python
espera_sem_dupli = espera_clean.groupby(['Unidade', 'Profissional'], as_index =False).sum()
```


```python
espera_sem_dupli[espera_sem_dupli.duplicated(subset=['Unidade','Profissional'], keep=False)].sort_values(by = 'Profissional')
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unidade</th>
      <th>Profissional</th>
      <th>Especialidade</th>
      <th>Usuários</th>
      <th>Espera &gt; 30</th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>
</div>




```python
espera_clean = espera_sem_dupli.drop(columns = ['Especialidade']).reset_index(drop = True)
espera_clean
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unidade</th>
      <th>Profissional</th>
      <th>Usuários</th>
      <th>Espera &gt; 30</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>CLINICA DT</td>
      <td>MEDICO AAV</td>
      <td>114</td>
      <td>32</td>
    </tr>
    <tr>
      <th>1</th>
      <td>CLINICA DT</td>
      <td>MEDICO ACD</td>
      <td>452</td>
      <td>383</td>
    </tr>
    <tr>
      <th>2</th>
      <td>CLINICA DT</td>
      <td>MEDICO ADC</td>
      <td>91</td>
      <td>69</td>
    </tr>
    <tr>
      <th>3</th>
      <td>CLINICA DT</td>
      <td>MEDICO AFL</td>
      <td>465</td>
      <td>27</td>
    </tr>
    <tr>
      <th>4</th>
      <td>CLINICA DT</td>
      <td>MEDICO AFLJ</td>
      <td>63</td>
      <td>18</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>161</th>
      <td>CLINICA SL</td>
      <td>MEDICO TDO</td>
      <td>183</td>
      <td>14</td>
    </tr>
    <tr>
      <th>162</th>
      <td>CLINICA SL</td>
      <td>MEDICO TMP</td>
      <td>221</td>
      <td>58</td>
    </tr>
    <tr>
      <th>163</th>
      <td>CLINICA SL</td>
      <td>MEDICO TTS</td>
      <td>119</td>
      <td>19</td>
    </tr>
    <tr>
      <th>164</th>
      <td>CLINICA SL</td>
      <td>MEDICO WAS</td>
      <td>37</td>
      <td>17</td>
    </tr>
    <tr>
      <th>165</th>
      <td>CLINICA SL</td>
      <td>MEDICO WJS</td>
      <td>79</td>
      <td>58</td>
    </tr>
  </tbody>
</table>
<p>166 rows × 4 columns</p>
</div>




```python
df_merge = pd.merge(faltas_clean, prod_clean, on =['Unidade', 'Profissional', 'Especialidade'], how= 'outer')
df_merge = pd.merge(df_merge, espera_clean, on= ['Unidade', 'Profissional'], how = 'outer')
df_merge
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unidade</th>
      <th>Especialidade</th>
      <th>Profissional</th>
      <th>Consultas Efetivadas</th>
      <th>Faltas Médicas</th>
      <th>Faltas Paciente</th>
      <th>Remarcações Médicas</th>
      <th>Total de Consultas</th>
      <th>Atendimento Produtividade</th>
      <th>Quantidade Horas Produtividade</th>
      <th>Usuários</th>
      <th>Espera &gt; 30</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>CLINICA DT</td>
      <td>ANGIOLOGIA/CIRUR VASCULAR</td>
      <td>MEDICO NJV</td>
      <td>42.0</td>
      <td>0.0</td>
      <td>19.0</td>
      <td>0.0</td>
      <td>61.0</td>
      <td>42.0</td>
      <td>4.250000</td>
      <td>43.0</td>
      <td>25.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>CLINICA DT</td>
      <td>CARDIOLOGIA</td>
      <td>MEDICO AGH</td>
      <td>57.0</td>
      <td>0.0</td>
      <td>19.0</td>
      <td>0.0</td>
      <td>76.0</td>
      <td>57.0</td>
      <td>9.392500</td>
      <td>57.0</td>
      <td>9.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>CLINICA DT</td>
      <td>CARDIOLOGIA</td>
      <td>MEDICO BGA</td>
      <td>76.0</td>
      <td>11.0</td>
      <td>42.0</td>
      <td>0.0</td>
      <td>129.0</td>
      <td>76.0</td>
      <td>8.108333</td>
      <td>79.0</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>CLINICA DT</td>
      <td>CARDIOLOGIA</td>
      <td>MEDICO FER</td>
      <td>71.0</td>
      <td>0.0</td>
      <td>25.0</td>
      <td>0.0</td>
      <td>97.0</td>
      <td>71.0</td>
      <td>9.903611</td>
      <td>71.0</td>
      <td>13.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>CLINICA DT</td>
      <td>CARDIOLOGIA</td>
      <td>MEDICO FFD</td>
      <td>31.0</td>
      <td>0.0</td>
      <td>17.0</td>
      <td>0.0</td>
      <td>65.0</td>
      <td>22.0</td>
      <td>1.809167</td>
      <td>31.0</td>
      <td>30.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>173</th>
      <td>CLINICA SL</td>
      <td>ORTOPEDIA E TRAUMATOLOGIA</td>
      <td>MEDICO MMB</td>
      <td>325.0</td>
      <td>0.0</td>
      <td>211.0</td>
      <td>0.0</td>
      <td>544.0</td>
      <td>325.0</td>
      <td>61.434167</td>
      <td>291.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>174</th>
      <td>CLINICA SL</td>
      <td>ORTOPEDIA E TRAUMATOLOGIA</td>
      <td>MEDICO WAS</td>
      <td>41.0</td>
      <td>0.0</td>
      <td>26.0</td>
      <td>0.0</td>
      <td>67.0</td>
      <td>41.0</td>
      <td>10.063889</td>
      <td>37.0</td>
      <td>17.0</td>
    </tr>
    <tr>
      <th>175</th>
      <td>CLINICA JA</td>
      <td>NaN</td>
      <td>MEDICO DAD</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>176</th>
      <td>CLINICA LV</td>
      <td>NaN</td>
      <td>MEDICO MCM</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>177</th>
      <td>CLINICA SL</td>
      <td>NaN</td>
      <td>MEDICO JPL</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
<p>178 rows × 12 columns</p>
</div>




```python
df_merge.dropna(subset = ['Especialidade'], inplace = True)
df_merge
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unidade</th>
      <th>Especialidade</th>
      <th>Profissional</th>
      <th>Consultas Efetivadas</th>
      <th>Faltas Médicas</th>
      <th>Faltas Paciente</th>
      <th>Remarcações Médicas</th>
      <th>Total de Consultas</th>
      <th>Atendimento Produtividade</th>
      <th>Quantidade Horas Produtividade</th>
      <th>Usuários</th>
      <th>Espera &gt; 30</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>CLINICA DT</td>
      <td>ANGIOLOGIA/CIRUR VASCULAR</td>
      <td>MEDICO NJV</td>
      <td>42.0</td>
      <td>0.0</td>
      <td>19.0</td>
      <td>0.0</td>
      <td>61.0</td>
      <td>42.0</td>
      <td>4.250000</td>
      <td>43.0</td>
      <td>25.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>CLINICA DT</td>
      <td>CARDIOLOGIA</td>
      <td>MEDICO AGH</td>
      <td>57.0</td>
      <td>0.0</td>
      <td>19.0</td>
      <td>0.0</td>
      <td>76.0</td>
      <td>57.0</td>
      <td>9.392500</td>
      <td>57.0</td>
      <td>9.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>CLINICA DT</td>
      <td>CARDIOLOGIA</td>
      <td>MEDICO BGA</td>
      <td>76.0</td>
      <td>11.0</td>
      <td>42.0</td>
      <td>0.0</td>
      <td>129.0</td>
      <td>76.0</td>
      <td>8.108333</td>
      <td>79.0</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>CLINICA DT</td>
      <td>CARDIOLOGIA</td>
      <td>MEDICO FER</td>
      <td>71.0</td>
      <td>0.0</td>
      <td>25.0</td>
      <td>0.0</td>
      <td>97.0</td>
      <td>71.0</td>
      <td>9.903611</td>
      <td>71.0</td>
      <td>13.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>CLINICA DT</td>
      <td>CARDIOLOGIA</td>
      <td>MEDICO FFD</td>
      <td>31.0</td>
      <td>0.0</td>
      <td>17.0</td>
      <td>0.0</td>
      <td>65.0</td>
      <td>22.0</td>
      <td>1.809167</td>
      <td>31.0</td>
      <td>30.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>170</th>
      <td>CLINICA SL</td>
      <td>ORTOPEDIA E TRAUMATOLOGIA</td>
      <td>MEDICO FCC</td>
      <td>157.0</td>
      <td>1.0</td>
      <td>101.0</td>
      <td>45.0</td>
      <td>307.0</td>
      <td>157.0</td>
      <td>25.308056</td>
      <td>145.0</td>
      <td>62.0</td>
    </tr>
    <tr>
      <th>171</th>
      <td>CLINICA SL</td>
      <td>ORTOPEDIA E TRAUMATOLOGIA</td>
      <td>MEDICO JGS</td>
      <td>529.0</td>
      <td>102.0</td>
      <td>331.0</td>
      <td>49.0</td>
      <td>1018.0</td>
      <td>529.0</td>
      <td>106.409444</td>
      <td>492.0</td>
      <td>8.0</td>
    </tr>
    <tr>
      <th>172</th>
      <td>CLINICA SL</td>
      <td>ORTOPEDIA E TRAUMATOLOGIA</td>
      <td>MEDICO JHC</td>
      <td>529.0</td>
      <td>0.0</td>
      <td>291.0</td>
      <td>27.0</td>
      <td>860.0</td>
      <td>529.0</td>
      <td>86.376389</td>
      <td>476.0</td>
      <td>61.0</td>
    </tr>
    <tr>
      <th>173</th>
      <td>CLINICA SL</td>
      <td>ORTOPEDIA E TRAUMATOLOGIA</td>
      <td>MEDICO MMB</td>
      <td>325.0</td>
      <td>0.0</td>
      <td>211.0</td>
      <td>0.0</td>
      <td>544.0</td>
      <td>325.0</td>
      <td>61.434167</td>
      <td>291.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>174</th>
      <td>CLINICA SL</td>
      <td>ORTOPEDIA E TRAUMATOLOGIA</td>
      <td>MEDICO WAS</td>
      <td>41.0</td>
      <td>0.0</td>
      <td>26.0</td>
      <td>0.0</td>
      <td>67.0</td>
      <td>41.0</td>
      <td>10.063889</td>
      <td>37.0</td>
      <td>17.0</td>
    </tr>
  </tbody>
</table>
<p>175 rows × 12 columns</p>
</div>




```python
df_merge = df_merge.fillna(0).reset_index(drop = True)
```


```python
df_merge.to_excel('df_anon.xlsx', index = False)
```

