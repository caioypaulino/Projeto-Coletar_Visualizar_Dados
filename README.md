# **Projeto: Pipeline de Análise de Dados (Python to Tableau)**

## **Stack**
Python (pandas, zipfile, kaggle), Excel (export to .xlsx), Tableau

## **Sobre**
Projeto de pipeline de análise de dados, importando um dataset via "Open API Kaggle", manipulando os dados com "Python pandas", exportando em planilha "Excel .xlsx" e criando um dashboard com "Tableau".

## **Sobre os Dados**
Os dados foram retirados do seguinte Dataset Kaggle: https://www.kaggle.com/datasets/hmavrodiev/london-bike-sharing-dataset.

## **Python**
<div class="cell code" execution_count="18"
ExecuteTime="{&quot;end_time&quot;:&quot;2024-01-30T16:14:16.855752600Z&quot;,&quot;start_time&quot;:&quot;2024-01-30T16:14:16.845236400Z&quot;}"
collapsed="true">

``` python
import pandas as pd
import zipfile
import kaggle
```

</div>

<div class="cell code" execution_count="19"
ExecuteTime="{&quot;end_time&quot;:&quot;2024-01-30T16:14:18.419025700Z&quot;,&quot;start_time&quot;:&quot;2024-01-30T16:14:16.859754Z&quot;}"
collapsed="false">

``` python
# api kaggle para download do dataset
!kaggle datasets download -d hmavrodiev/london-bike-sharing-dataset
```

<div class="output stream stdout">

    Downloading london-bike-sharing-dataset.zip to s:/Projeto-Coletar_Visualizar_Dados
    100%|████████████████████████████████████████| 165k/165k [00:00<00:00, 1.44MB/s]]
    100%|████████████████████████████████████████| 165k/165k [00:00<00:00, 1.43MB/s]

</div>

</div>

<div class="cell code" execution_count="20"
ExecuteTime="{&quot;end_time&quot;:&quot;2024-01-30T16:14:18.441941400Z&quot;,&quot;start_time&quot;:&quot;2024-01-30T16:14:18.417025500Z&quot;}"
collapsed="false">

``` python
# extraindo arquivo da pasta .zip baixada
with zipfile.ZipFile('london-bike-sharing-dataset.zip', 'r') as file:
    file.extractall()
```

</div>

<div class="cell code" execution_count="21"
ExecuteTime="{&quot;end_time&quot;:&quot;2024-01-30T16:14:18.475852Z&quot;,&quot;start_time&quot;:&quot;2024-01-30T16:14:18.427939600Z&quot;}"
collapsed="false">

``` python
# criando um dataframe com pandas a partir do arquivo csv
bikes = pd.read_csv("london_merged.csv")
```

</div>

<div class="cell code" execution_count="22"
ExecuteTime="{&quot;end_time&quot;:&quot;2024-01-30T16:14:18.477856600Z&quot;,&quot;start_time&quot;:&quot;2024-01-30T16:14:18.446724300Z&quot;}"
collapsed="false">

``` python
# explorando os dados
bikes.info()
```

<div class="output stream stdout">

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 17414 entries, 0 to 17413
    Data columns (total 10 columns):
     #   Column        Non-Null Count  Dtype  
    ---  ------        --------------  -----  
     0   timestamp     17414 non-null  object 
     1   cnt           17414 non-null  int64  
     2   t1            17414 non-null  float64
     3   t2            17414 non-null  float64
     4   hum           17414 non-null  float64
     5   wind_speed    17414 non-null  float64
     6   weather_code  17414 non-null  float64
     7   is_holiday    17414 non-null  float64
     8   is_weekend    17414 non-null  float64
     9   season        17414 non-null  float64
    dtypes: float64(8), int64(1), object(1)
    memory usage: 1.3+ MB

</div>

</div>

<div class="cell code" execution_count="23"
ExecuteTime="{&quot;end_time&quot;:&quot;2024-01-30T16:14:18.478853Z&quot;,&quot;start_time&quot;:&quot;2024-01-30T16:14:18.456970100Z&quot;}"
collapsed="false">

``` python
# rows & columns || linhas & colunas
bikes.shape
```

<div class="output execute_result" execution_count="23">

    (17414, 10)

</div>

</div>

<div class="cell code" execution_count="24"
ExecuteTime="{&quot;end_time&quot;:&quot;2024-01-30T16:14:18.532345900Z&quot;,&quot;start_time&quot;:&quot;2024-01-30T16:14:18.461876400Z&quot;}"
collapsed="false">

``` python
bikes.head(100)
```

<div class="output execute_result" execution_count="24">

                  timestamp  cnt    t1    t2    hum  wind_speed  weather_code  \
    0   2015-01-04 00:00:00  182   3.0   2.0   93.0         6.0           3.0   
    1   2015-01-04 01:00:00  138   3.0   2.5   93.0         5.0           1.0   
    2   2015-01-04 02:00:00  134   2.5   2.5   96.5         0.0           1.0   
    3   2015-01-04 03:00:00   72   2.0   2.0  100.0         0.0           1.0   
    4   2015-01-04 04:00:00   47   2.0   0.0   93.0         6.5           1.0   
    ..                  ...  ...   ...   ...    ...         ...           ...   
    95  2015-01-08 00:00:00  123  11.0  11.0   82.0        26.0           4.0   
    96  2015-01-08 01:00:00   56  11.5  11.5   85.0        24.0           3.0   
    97  2015-01-08 02:00:00   51  12.0  12.0   82.0        25.0           3.0   
    98  2015-01-08 03:00:00   33  12.0  12.0   85.0        22.0           3.0   
    99  2015-01-08 04:00:00   32  12.0  12.0   88.0        20.5           7.0   

        is_holiday  is_weekend  season  
    0          0.0         1.0     3.0  
    1          0.0         1.0     3.0  
    2          0.0         1.0     3.0  
    3          0.0         1.0     3.0  
    4          0.0         1.0     3.0  
    ..         ...         ...     ...  
    95         0.0         0.0     3.0  
    96         0.0         0.0     3.0  
    97         0.0         0.0     3.0  
    98         0.0         0.0     3.0  
    99         0.0         0.0     3.0  

    [100 rows x 10 columns]

</div>

</div>

<div class="cell code" execution_count="25"
ExecuteTime="{&quot;end_time&quot;:&quot;2024-01-30T16:14:18.534352800Z&quot;,&quot;start_time&quot;:&quot;2024-01-30T16:14:18.476852400Z&quot;}"
collapsed="false">

``` python
bikes['weather_code'].value_counts()
```

<div class="output execute_result" execution_count="25">

    weather_code
    1.0     6150
    2.0     4034
    3.0     3551
    7.0     2141
    4.0     1464
    26.0      60
    10.0      14
    Name: count, dtype: int64

</div>

</div>

<div class="cell code" execution_count="26"
ExecuteTime="{&quot;end_time&quot;:&quot;2024-01-30T16:14:18.535353400Z&quot;,&quot;start_time&quot;:&quot;2024-01-30T16:14:18.486301700Z&quot;}"
collapsed="false">

``` python
bikes['season'].value_counts()
```

<div class="output execute_result" execution_count="26">

    season
    0.0    4394
    1.0    4387
    3.0    4330
    2.0    4303
    Name: count, dtype: int64

</div>

</div>

<div class="cell code" execution_count="27"
ExecuteTime="{&quot;end_time&quot;:&quot;2024-01-30T16:14:18.560612500Z&quot;,&quot;start_time&quot;:&quot;2024-01-30T16:14:18.494655200Z&quot;}"
collapsed="false">

``` python
# renomeando colunas com dicionário personalizado
new_columns = {
    'timestamp':'time', 
    'cnt':'count', 
    't1':'temp_real_C', 
    't2':'temp_feels_like_C', 
    'hum':'humidity_percent', 
    'wind_speed':'wind_speed_kph', 
    'weather_code':'weather', 
    'is_holiday':'is_holiday', 
    'is_weekend':'is_weekend', 
    'season':'season'    
}

bikes.rename(new_columns, axis=1, inplace=True)
    
```

</div>

<div class="cell code" execution_count="28"
ExecuteTime="{&quot;end_time&quot;:&quot;2024-01-30T16:14:18.600629300Z&quot;,&quot;start_time&quot;:&quot;2024-01-30T16:14:18.500033600Z&quot;}"
collapsed="false">

``` python
# checando o nome das colunas alteradas
bikes.columns.values
```

<div class="output execute_result" execution_count="28">

    array(['time', 'count', 'temp_real_C', 'temp_feels_like_C',
           'humidity_percent', 'wind_speed_kph', 'weather', 'is_holiday',
           'is_weekend', 'season'], dtype=object)

</div>

</div>

<div class="cell code" execution_count="29"
ExecuteTime="{&quot;end_time&quot;:&quot;2024-01-30T16:14:18.601631Z&quot;,&quot;start_time&quot;:&quot;2024-01-30T16:14:18.508547Z&quot;}"
collapsed="false">

``` python
# alterando valores de humidade para percentual
bikes['humidity_percent'] = bikes['humidity_percent']/100
```

</div>

<div class="cell code" execution_count="30"
ExecuteTime="{&quot;end_time&quot;:&quot;2024-01-30T16:14:18.602636900Z&quot;,&quot;start_time&quot;:&quot;2024-01-30T16:14:18.516966700Z&quot;}"
collapsed="false">

``` python
# criando um dicionário personalizado para alterar os valores int de 'season' para str conforme escrito na documentação
season_dict = {
    '0.0':'Spring',
    '1.0':'Summer',
    '2.0':'Autumn',
    '3.0':'Winter'
}

# criando um dicionário personalizado para alterar os valores int de 'weather' para str conforme escrito na documentação
weather_dict = {
    '1.0':'Clear',
    '2.0':'Scattered clouds',
    '3.0':'Broken clouds',
    '4.0':'Cloudy',
    '7.0':'Rain',
    '10.0':'Rain with thunderstorm',
    '26.0':'Snowfall'
}

# mudando tipo de dados para string e atualizando valores
bikes['season'] = bikes['season'].astype('str')
bikes['season']  = bikes['season'].map(season_dict)

# mudando tipo de dados para string e atualizando valores
bikes['weather'] = bikes['weather'].astype('str')
bikes['weather'] = bikes['weather'].map(weather_dict)
```

</div>

<div class="cell code" execution_count="31"
ExecuteTime="{&quot;end_time&quot;:&quot;2024-01-30T16:14:18.604630700Z&quot;,&quot;start_time&quot;:&quot;2024-01-30T16:14:18.535353400Z&quot;}"
collapsed="false">

``` python
bikes.head()
```

<div class="output execute_result" execution_count="31">

                      time  count  temp_real_C  temp_feels_like_C  \
    0  2015-01-04 00:00:00    182          3.0                2.0   
    1  2015-01-04 01:00:00    138          3.0                2.5   
    2  2015-01-04 02:00:00    134          2.5                2.5   
    3  2015-01-04 03:00:00     72          2.0                2.0   
    4  2015-01-04 04:00:00     47          2.0                0.0   

       humidity_percent  wind_speed_kph        weather  is_holiday  is_weekend  \
    0             0.930             6.0  Broken clouds         0.0         1.0   
    1             0.930             5.0          Clear         0.0         1.0   
    2             0.965             0.0          Clear         0.0         1.0   
    3             1.000             0.0          Clear         0.0         1.0   
    4             0.930             6.5          Clear         0.0         1.0   

       season  
    0  Winter  
    1  Winter  
    2  Winter  
    3  Winter  
    4  Winter  

</div>

</div>

<div class="cell code" execution_count="32"
ExecuteTime="{&quot;end_time&quot;:&quot;2024-01-30T16:14:21.418236300Z&quot;,&quot;start_time&quot;:&quot;2024-01-30T16:14:18.544608900Z&quot;}"
collapsed="false">

``` python
# exportando versão final DataFrame para arquivo .xlsx
bikes.to_excel('london_bikes_final.xlsx', sheet_name = 'Data')
```

</div>

## **Tableau**
Além de todo o trabalho de coleta, manipulação e exportação dos dados, foram feitos processos de análise com Tableau e a montagem de um dashboard simples.

### **Moving Average (Média Móvel):**
Soma Contagem de "Rides" ao Longo do Tempo.

![Moving Average](https://github.com/caioypaulino/Projeto-Coletar_Visualizar_Dados/blob/main/Dashboard%20Images/Moving%20Average.png)

### **Total "Rides":**
Soma Contagem de "Rides" no Período de Tempo Selecionado (In Range).

![Total Rides](https://github.com/caioypaulino/Projeto-Coletar_Visualizar_Dados/blob/main/Dashboard%20Images/Total%20Rides.png)

### **Heatmap (Mapa de Calor):**
Temperatura (ºC) X Velocidade do Vento (Km/h) no Período de Tempo Selecionado.

![Heatmap](https://github.com/caioypaulino/Projeto-Coletar_Visualizar_Dados/blob/main/Dashboard%20Images/Heatmap.png)

### **Dashboard:**
Dashboard Final com todas as análises.

![Dashboard](https://github.com/caioypaulino/Projeto-Coletar_Visualizar_Dados/blob/main/Dashboard%20Images/Dashboard.gif)
