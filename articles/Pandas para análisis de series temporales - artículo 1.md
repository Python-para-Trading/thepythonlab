
## Pandas nos hace la vida un poco mas facil.

Muchos estamos familiarizados con Excel y con sus hojas de calculos pues son ampliamente utilizadas para almacenar y manipular datos, especialmente numericos, y hacer cálculos.

En Python tenemos varias librerias para manipular todo tipo de datos, pero una es especialmente eficiente para las series temporales, **Pandas**. 

Pandas tiene dos objetos básicos las series, que son vectores indexados y los dataframes, que son matrices n-dimensionales indexadas.  Podemos pensar en un dataframe como una hoja de calculo de Excel supervitaminada.

Una **serie temporal** es una secuencia de datos tomados en determinados momentos ordenados cronológicamente. Por ejemplo la cotización de cierre de una acción, tenemos una sucesión de valores medidos al final de la sesión de cada día. En análisis financiero practicamente tratamos con series temporales casí todo el tiempo, y Pandas nos hace la vida mucho mas facil.

De hecho Pandas fue desarrollada incialmente por **Wes McKinney** cuando trabajaba en un hedge found, AQR Capital Management, y posteriormente liberada como open source.

Esta librería tiene un gran número de funciones para realizar cálculos y manipulaciones de series y dataframes, y se ha originado un ecosistema al ser usada como base por otras librerias de terceros, que hacen uso de estos objetos y sus funciones.

Si has instalado Anaconda para usar Python, el módulo de Pandas ya viene preinstalado. Si no es así puedes instalarlo usando *conda*, basta con ejecutar en el terminal de comandos:

`conda install pandas`

o bien usando *pip*:

`pip install pandas`

---

## Dataframes

Un **DataFrame** de Pandas es una matriz ordenada que puede contener cualquier tipo de datos. Se ordena en columnas, que deben contener siempre un mismo tipo de dato, y en filas que generan un indice.

Para practicar con los dataframes vamos a usar series temporales de cotizaciones diarias de acciones. Para lo cual nos descargaremos los datos históricos.

**Pandas Datareader** es un módulo asociado a Pandas que permite descargar datos desde distintas fuentes.

Sin embargo, debido a que Yahoo descontinuó su API para datos financieros, para poder descarga desde Yahoo Finance correctamente, utilizaremos el módulo **Fix Yahoo Finance**. Si no lo tienes instalado puedes instalarlo con :

`pip install fix-yahoo-finance`

Vamos a comenzar importando esos dos módulos. Importamos **Pandas** y para simplificar le asignamos el nombre **pd**, igual hacemos con **Fix Yahoo Finance**.


```python
import pandas as pd
import fix_yahoo_finance as yf
```

Descargaremos el histórico diario de Santander y BBVA desde principios de 2008 hasta final de 2018, once años.
Para ello pasaremos como parámetros los tickers de los valores y las fechas de inicio y fin. Los tickers para otros valores se pueden localizar en la página de Yahoo Finance.

En un futuro artículo hablaremos sobre las fuentes de datos financieros y sus API, pero de de momento nos bastará con saber como bajar los datos que necesitamos para estudiar los dataframe de Pandas.


```python
start = '2008-01-01'
end = '2018-12-31'
tickers=['SAN.MC', 'BBVA.MC']
```


```python
san = yf.download(tickers[0], start=start, end=end)
```

    [*********************100%***********************]  1 of 1 downloaded



```python
bbva = yf.download(tickers[1], start=start, end=end)
```

    [*********************100%***********************]  1 of 1 downloaded


Lo que recibimos en la variable __san__ es un **DataFrame** de Pandas, una matriz de dos dimensiones, como dijimos algo similar al un hoja de calculo de Excel.

Vamos a ver usando el método **head()** las cinco primeras lineas del dataframe **san**.


```python
san.head()
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
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Adj Close</th>
      <th>Volume</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2008-01-02</th>
      <td>13.2489</td>
      <td>13.3302</td>
      <td>13.0953</td>
      <td>13.1766</td>
      <td>5.868722</td>
      <td>103998100</td>
    </tr>
    <tr>
      <th>2008-01-03</th>
      <td>13.1405</td>
      <td>13.2037</td>
      <td>12.9689</td>
      <td>13.0502</td>
      <td>5.812426</td>
      <td>113222703</td>
    </tr>
    <tr>
      <th>2008-01-04</th>
      <td>13.0050</td>
      <td>13.0863</td>
      <td>12.7070</td>
      <td>12.8605</td>
      <td>5.727935</td>
      <td>100543802</td>
    </tr>
    <tr>
      <th>2008-01-07</th>
      <td>12.8154</td>
      <td>12.9057</td>
      <td>12.6889</td>
      <td>12.7793</td>
      <td>5.691768</td>
      <td>71995342</td>
    </tr>
    <tr>
      <th>2008-01-08</th>
      <td>12.7883</td>
      <td>12.8063</td>
      <td>12.4993</td>
      <td>12.5806</td>
      <td>5.603270</td>
      <td>83100401</td>
    </tr>
  </tbody>
</table>
</div>



Y con **tail()** las cinco últimas de **bbva**.


```python
bbva.tail()
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
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Adj Close</th>
      <th>Volume</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-12-21</th>
      <td>4.6330</td>
      <td>4.6600</td>
      <td>4.5340</td>
      <td>4.6185</td>
      <td>4.484022</td>
      <td>96489872</td>
    </tr>
    <tr>
      <th>2018-12-24</th>
      <td>4.5745</td>
      <td>4.5990</td>
      <td>4.5425</td>
      <td>4.5580</td>
      <td>4.425283</td>
      <td>5652399</td>
    </tr>
    <tr>
      <th>2018-12-27</th>
      <td>4.6000</td>
      <td>4.6380</td>
      <td>4.4765</td>
      <td>4.5450</td>
      <td>4.412662</td>
      <td>32726196</td>
    </tr>
    <tr>
      <th>2018-12-28</th>
      <td>4.5585</td>
      <td>4.6480</td>
      <td>4.5500</td>
      <td>4.6410</td>
      <td>4.505866</td>
      <td>20924025</td>
    </tr>
    <tr>
      <th>2018-12-31</th>
      <td>4.6350</td>
      <td>4.6635</td>
      <td>4.6200</td>
      <td>4.6355</td>
      <td>4.500526</td>
      <td>6885185</td>
    </tr>
  </tbody>
</table>
</div>



Vamos a usar la función de Pandas **describe()**, que nos dara un resumen estadistico de los datos contenidos en el dataframe. Lo que este método nos devuelve es un nuevo dataframe con los datos agregados.


```python
san.describe()
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
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Adj Close</th>
      <th>Volume</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>2810.000000</td>
      <td>2810.000000</td>
      <td>2810.000000</td>
      <td>2810.000000</td>
      <td>2810.000000</td>
      <td>2.810000e+03</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>6.646034</td>
      <td>6.736354</td>
      <td>6.539929</td>
      <td>6.641825</td>
      <td>4.465291</td>
      <td>9.608371e+07</td>
    </tr>
    <tr>
      <th>std</th>
      <td>2.121196</td>
      <td>2.148194</td>
      <td>2.085775</td>
      <td>2.120126</td>
      <td>0.873586</td>
      <td>7.419585e+07</td>
    </tr>
    <tr>
      <th>min</th>
      <td>3.117870</td>
      <td>3.327370</td>
      <td>3.098200</td>
      <td>3.245730</td>
      <td>1.878404</td>
      <td>7.377082e+06</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>5.216290</td>
      <td>5.280958</td>
      <td>5.134370</td>
      <td>5.203502</td>
      <td>3.782240</td>
      <td>5.309241e+07</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>6.019360</td>
      <td>6.091000</td>
      <td>5.920515</td>
      <td>6.028705</td>
      <td>4.549748</td>
      <td>7.453013e+07</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>7.740327</td>
      <td>7.832793</td>
      <td>7.634295</td>
      <td>7.738860</td>
      <td>5.212689</td>
      <td>1.127219e+08</td>
    </tr>
    <tr>
      <th>max</th>
      <td>13.248900</td>
      <td>13.330200</td>
      <td>13.095300</td>
      <td>13.176600</td>
      <td>6.157157</td>
      <td>9.092368e+08</td>
    </tr>
  </tbody>
</table>
</div>




```python
bbva.describe()
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
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Adj Close</th>
      <th>Volume</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>2810.000000</td>
      <td>2810.000000</td>
      <td>2810.000000</td>
      <td>2810.000000</td>
      <td>2810.000000</td>
      <td>2.810000e+03</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>7.973480</td>
      <td>8.078099</td>
      <td>7.849524</td>
      <td>7.968902</td>
      <td>5.647123</td>
      <td>5.260945e+07</td>
    </tr>
    <tr>
      <th>std</th>
      <td>2.116239</td>
      <td>2.133773</td>
      <td>2.090441</td>
      <td>2.113349</td>
      <td>1.128175</td>
      <td>4.675970e+07</td>
    </tr>
    <tr>
      <th>min</th>
      <td>4.400000</td>
      <td>4.540000</td>
      <td>4.275310</td>
      <td>4.430000</td>
      <td>2.550083</td>
      <td>5.217450e+06</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>6.381500</td>
      <td>6.465500</td>
      <td>6.287000</td>
      <td>6.375000</td>
      <td>4.757789</td>
      <td>2.698997e+07</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>7.609500</td>
      <td>7.699500</td>
      <td>7.472000</td>
      <td>7.597500</td>
      <td>5.642354</td>
      <td>3.900200e+07</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>9.042500</td>
      <td>9.157500</td>
      <td>8.911750</td>
      <td>9.040450</td>
      <td>6.657778</td>
      <td>6.072695e+07</td>
    </tr>
    <tr>
      <th>max</th>
      <td>16.102100</td>
      <td>16.159700</td>
      <td>15.852300</td>
      <td>15.929100</td>
      <td>8.330698</td>
      <td>6.009019e+08</td>
    </tr>
  </tbody>
</table>
</div>



Vemos que tanto en este caso, como al usar **head()** y **tail()** no hemos aplicado la función y pasado entre parentesis el dataframe como un parámetros, sino que tras el nombre del dataframe con un punto pasamos la función. Esto es debido a que **describe()** es un método del objeto dataframe, y ya lo toma como parámetro. Es especialmente útil y permite el encadenado de métodos, es decir ir agregando funciones que toman el resultado de la anterior como parámetro.

Otro método que nos proporciona información resumida es **info()**.


```python
san.info()
```

    <class 'pandas.core.frame.DataFrame'>
    DatetimeIndex: 2810 entries, 2008-01-02 to 2018-12-31
    Data columns (total 6 columns):
    Open         2810 non-null float64
    High         2810 non-null float64
    Low          2810 non-null float64
    Close        2810 non-null float64
    Adj Close    2810 non-null float64
    Volume       2810 non-null int64
    dtypes: float64(5), int64(1)
    memory usage: 153.7 KB



```python
bbva.info()
```

    <class 'pandas.core.frame.DataFrame'>
    DatetimeIndex: 2810 entries, 2008-01-02 to 2018-12-31
    Data columns (total 6 columns):
    Open         2810 non-null float64
    High         2810 non-null float64
    Low          2810 non-null float64
    Close        2810 non-null float64
    Adj Close    2810 non-null float64
    Volume       2810 non-null int64
    dtypes: float64(5), int64(1)
    memory usage: 153.7 KB


Revisamos las dimensiones de cada dataframe, vemos que tienen dos dimensiones, que reflejan las filas y las columnas. 

2810 filas correspondientes a los días de cotización, y 6 columnas para los distintos datos.

Para ello usamos **shape**, que como vemos no lleva parentesis detrás, esto es debido a que es una propiedad del dataframe y no un método del mismo.


```python
san.shape
```




    (2810, 6)




```python
bbva.shape
```




    (2810, 6)



Podemos extraer el índice y las columnas de un dataframe usando **index** y **columns** respectivamente. 

El índice de nuestros dataframe son las fechas de los días cotizados.


```python
san.index
```




    DatetimeIndex(['2008-01-02', '2008-01-03', '2008-01-04', '2008-01-07',
                   '2008-01-08', '2008-01-09', '2008-01-10', '2008-01-11',
                   '2008-01-14', '2008-01-15',
                   ...
                   '2018-12-14', '2018-12-17', '2018-12-18', '2018-12-19',
                   '2018-12-20', '2018-12-21', '2018-12-24', '2018-12-27',
                   '2018-12-28', '2018-12-31'],
                  dtype='datetime64[ns]', name='Date', length=2810, freq=None)



Mientras que las columnas recogen los distintos valores de cada día cotizado.


```python
san.columns
```




    Index(['Open', 'High', 'Low', 'Close', 'Adj Close', 'Volume'], dtype='object')



Observamos como en ambos casos nos muestra 6 columnas y 5 filas. Las columna **Open** por ejemplo contiene todos los precios de apertura de cada acción. Y las filas están precedidas por una fecha que es el índice de nuestro dataframe. Así podemos obtener datos llamandolos por su columna, su índice o por una combinación de ambos.

## Extracción de datos.

Puede ser que nos interese solo una columna y podemos extraerla del dataframe, lo que nos devuelve es un objeto Serie de Pandas.


```python
san['Close']
```




    Date
    2008-01-02    13.1766
    2008-01-03    13.0502
    2008-01-04    12.8605
    2008-01-07    12.7793
    2008-01-08    12.5806
    2008-01-09    12.3277
    2008-01-10    12.1832
    2008-01-11    12.3819
    2008-01-14    12.2103
    2008-01-15    11.7407
    2008-01-16    11.6052
    2008-01-17    11.5149
    2008-01-18    11.2349
    2008-01-21    10.2234
    2008-01-22    10.6930
    2008-01-23    10.1782
    2008-01-24    10.8466
    2008-01-25    10.9188
    2008-01-28    10.8285
    2008-01-29    10.8917
    2008-01-30    10.8466
    2008-01-31    10.6840
    2008-02-01    10.9007
    2008-02-04    10.8285
    2008-02-05    10.2505
    2008-02-06    10.4763
    2008-02-07    10.4763
    2008-02-08    10.5034
    2008-02-11    10.3227
    2008-02-12    10.7111
                   ...   
    2018-11-16     4.2200
    2018-11-19     4.2030
    2018-11-20     4.0800
    2018-11-21     4.1530
    2018-11-22     4.0855
    2018-11-23     4.0875
    2018-11-26     4.2055
    2018-11-27     4.1985
    2018-11-28     4.2245
    2018-11-29     4.2135
    2018-11-30     4.1850
    2018-12-03     4.2720
    2018-12-04     4.1675
    2018-12-05     4.1390
    2018-12-06     3.9800
    2018-12-07     3.9790
    2018-12-10     3.8730
    2018-12-11     3.8790
    2018-12-12     4.0105
    2018-12-13     4.0710
    2018-12-14     4.0595
    2018-12-17     4.0270
    2018-12-18     3.9900
    2018-12-19     4.0415
    2018-12-20     3.9780
    2018-12-21     3.9305
    2018-12-24     3.8915
    2018-12-27     3.8620
    2018-12-28     3.9450
    2018-12-31     3.9730
    Name: Close, Length: 2810, dtype: float64



O bien solo nos interese una fecha en concreto.


```python
bbva.loc['2018-12-31']
```




    Open         4.635000e+00
    High         4.663500e+00
    Low          4.620000e+00
    Close        4.635500e+00
    Adj Close    4.500526e+00
    Volume       6.885185e+06
    Name: 2018-12-31 00:00:00, dtype: float64



Vemos que para extraer una columna solo necesitamos pasar su nombre entre corchetes pero para un índice usamos el metodo **loc**. Pandas tiene diversas formas de extraer la información en función de como queramos hacerlo. Así el método **loc** extrae en base a la etiqueta del índice o columna, y el método **iloc** lo hace en función del numero ordinal que ocupa dicho índice o columna.


```python
san.iloc[0]
```




    Open         1.324890e+01
    High         1.333020e+01
    Low          1.309530e+01
    Close        1.317660e+01
    Adj Close    5.868722e+00
    Volume       1.039981e+08
    Name: 2008-01-02 00:00:00, dtype: float64



Aunque para hacer una extracción por número de orden de varias filas no necesitamos usar **iloc** podemos hacerlo diréctamente.


```python
san[100:106]
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
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Adj Close</th>
      <th>Volume</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2008-05-26</th>
      <td>12.0387</td>
      <td>12.0387</td>
      <td>11.8400</td>
      <td>11.9122</td>
      <td>5.491112</td>
      <td>57912101</td>
    </tr>
    <tr>
      <th>2008-05-27</th>
      <td>11.9122</td>
      <td>11.9935</td>
      <td>11.7858</td>
      <td>11.8129</td>
      <td>5.445339</td>
      <td>53285353</td>
    </tr>
    <tr>
      <th>2008-05-28</th>
      <td>11.8129</td>
      <td>12.1019</td>
      <td>11.8129</td>
      <td>11.9664</td>
      <td>5.516099</td>
      <td>51351373</td>
    </tr>
    <tr>
      <th>2008-05-29</th>
      <td>11.9664</td>
      <td>12.1200</td>
      <td>11.8219</td>
      <td>11.9664</td>
      <td>5.516099</td>
      <td>43426708</td>
    </tr>
    <tr>
      <th>2008-05-30</th>
      <td>11.9664</td>
      <td>12.1200</td>
      <td>11.9664</td>
      <td>12.0929</td>
      <td>5.574409</td>
      <td>40694225</td>
    </tr>
    <tr>
      <th>2008-06-02</th>
      <td>12.0929</td>
      <td>12.0929</td>
      <td>11.7677</td>
      <td>11.8219</td>
      <td>5.449489</td>
      <td>45788834</td>
    </tr>
  </tbody>
</table>
</div>



Si es útil cuando queremos hacer una extracción tanto de filas como de columnas.


```python
san.iloc[:2,:2]
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
      <th>Open</th>
      <th>High</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2008-01-02</th>
      <td>13.2489</td>
      <td>13.3302</td>
    </tr>
    <tr>
      <th>2008-01-03</th>
      <td>13.1405</td>
      <td>13.2037</td>
    </tr>
  </tbody>
</table>
</div>



Ahora veamos el cierre ajustado y el volumen desde el 1 al 10 de noviembre de 2015.


```python
san.loc['2015-11-01':'2015-11-10', 'Adj Close':'Volume'] 
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
      <th>Adj Close</th>
      <th>Volume</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2015-11-02</th>
      <td>4.374040</td>
      <td>57910508</td>
    </tr>
    <tr>
      <th>2015-11-03</th>
      <td>4.416542</td>
      <td>148301916</td>
    </tr>
    <tr>
      <th>2015-11-04</th>
      <td>4.483690</td>
      <td>105920463</td>
    </tr>
    <tr>
      <th>2015-11-05</th>
      <td>4.425892</td>
      <td>87484985</td>
    </tr>
    <tr>
      <th>2015-11-06</th>
      <td>4.509184</td>
      <td>86906806</td>
    </tr>
    <tr>
      <th>2015-11-09</th>
      <td>4.413992</td>
      <td>71676192</td>
    </tr>
    <tr>
      <th>2015-11-10</th>
      <td>4.398687</td>
      <td>39123436</td>
    </tr>
  </tbody>
</table>
</div>



Si tenemos en cuenta que lo se devuelve simpre es un dataframe o una serie, podemos encadenar varias formas de hacer extracciones.

Así por ejemplo podemos tomar primero 3 columnas por su nombre y despues las diez últimas filas. En este caso no necesitamos usar **iloc**.


```python
san[['Close', 'Low', 'Volume']][-10:]
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
      <th>Close</th>
      <th>Low</th>
      <th>Volume</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-12-14</th>
      <td>4.0595</td>
      <td>3.9755</td>
      <td>65754616</td>
    </tr>
    <tr>
      <th>2018-12-17</th>
      <td>4.0270</td>
      <td>4.0250</td>
      <td>39823249</td>
    </tr>
    <tr>
      <th>2018-12-18</th>
      <td>3.9900</td>
      <td>3.9900</td>
      <td>44570803</td>
    </tr>
    <tr>
      <th>2018-12-19</th>
      <td>4.0415</td>
      <td>4.0080</td>
      <td>52444592</td>
    </tr>
    <tr>
      <th>2018-12-20</th>
      <td>3.9780</td>
      <td>3.9465</td>
      <td>58014374</td>
    </tr>
    <tr>
      <th>2018-12-21</th>
      <td>3.9305</td>
      <td>3.8815</td>
      <td>212350900</td>
    </tr>
    <tr>
      <th>2018-12-24</th>
      <td>3.8915</td>
      <td>3.8745</td>
      <td>15720836</td>
    </tr>
    <tr>
      <th>2018-12-27</th>
      <td>3.8620</td>
      <td>3.8000</td>
      <td>51788055</td>
    </tr>
    <tr>
      <th>2018-12-28</th>
      <td>3.9450</td>
      <td>3.8630</td>
      <td>35454221</td>
    </tr>
    <tr>
      <th>2018-12-31</th>
      <td>3.9730</td>
      <td>3.9065</td>
      <td>16730575</td>
    </tr>
  </tbody>
</table>
</div>



O tomar dos columnas y usar el método **head()**. Por ejemplo para tomar los 5 primeros mínimos y máximos


```python
san[['High','Low']].head()
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
      <th>High</th>
      <th>Low</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2008-01-02</th>
      <td>13.3302</td>
      <td>13.0953</td>
    </tr>
    <tr>
      <th>2008-01-03</th>
      <td>13.2037</td>
      <td>12.9689</td>
    </tr>
    <tr>
      <th>2008-01-04</th>
      <td>13.0863</td>
      <td>12.7070</td>
    </tr>
    <tr>
      <th>2008-01-07</th>
      <td>12.9057</td>
      <td>12.6889</td>
    </tr>
    <tr>
      <th>2008-01-08</th>
      <td>12.8063</td>
      <td>12.4993</td>
    </tr>
  </tbody>
</table>
</div>



Además **loc** cuando lo usamos sobre un índice de fechas (*datetime*) permite extraer usando periodos. Así si queremos extraer los datos de mayo de 2018 podemos hacer lo siguiente.


```python
san.loc['2018-05']
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
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Adj Close</th>
      <th>Volume</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-05-02</th>
      <td>5.359</td>
      <td>5.415</td>
      <td>5.3570</td>
      <td>5.3980</td>
      <td>5.202323</td>
      <td>320982382</td>
    </tr>
    <tr>
      <th>2018-05-03</th>
      <td>5.390</td>
      <td>5.416</td>
      <td>5.3150</td>
      <td>5.3360</td>
      <td>5.142571</td>
      <td>260700006</td>
    </tr>
    <tr>
      <th>2018-05-04</th>
      <td>5.328</td>
      <td>5.379</td>
      <td>5.3010</td>
      <td>5.3760</td>
      <td>5.181121</td>
      <td>34640717</td>
    </tr>
    <tr>
      <th>2018-05-07</th>
      <td>5.387</td>
      <td>5.405</td>
      <td>5.3560</td>
      <td>5.3800</td>
      <td>5.184977</td>
      <td>94307179</td>
    </tr>
    <tr>
      <th>2018-05-08</th>
      <td>5.378</td>
      <td>5.423</td>
      <td>5.3250</td>
      <td>5.3840</td>
      <td>5.188831</td>
      <td>68881042</td>
    </tr>
    <tr>
      <th>2018-05-09</th>
      <td>5.390</td>
      <td>5.449</td>
      <td>5.3850</td>
      <td>5.4350</td>
      <td>5.237983</td>
      <td>64844626</td>
    </tr>
    <tr>
      <th>2018-05-10</th>
      <td>5.456</td>
      <td>5.486</td>
      <td>5.4120</td>
      <td>5.4860</td>
      <td>5.287134</td>
      <td>37895987</td>
    </tr>
    <tr>
      <th>2018-05-11</th>
      <td>5.490</td>
      <td>5.528</td>
      <td>5.4740</td>
      <td>5.5180</td>
      <td>5.317974</td>
      <td>45371092</td>
    </tr>
    <tr>
      <th>2018-05-14</th>
      <td>5.514</td>
      <td>5.537</td>
      <td>5.4760</td>
      <td>5.5060</td>
      <td>5.306409</td>
      <td>32216377</td>
    </tr>
    <tr>
      <th>2018-05-15</th>
      <td>5.491</td>
      <td>5.526</td>
      <td>5.4320</td>
      <td>5.4670</td>
      <td>5.268823</td>
      <td>39260950</td>
    </tr>
    <tr>
      <th>2018-05-16</th>
      <td>5.437</td>
      <td>5.460</td>
      <td>5.3120</td>
      <td>5.3290</td>
      <td>5.135825</td>
      <td>54683384</td>
    </tr>
    <tr>
      <th>2018-05-17</th>
      <td>5.338</td>
      <td>5.363</td>
      <td>5.3070</td>
      <td>5.3520</td>
      <td>5.157991</td>
      <td>43080699</td>
    </tr>
    <tr>
      <th>2018-05-18</th>
      <td>5.336</td>
      <td>5.343</td>
      <td>5.1880</td>
      <td>5.2060</td>
      <td>5.017283</td>
      <td>90424536</td>
    </tr>
    <tr>
      <th>2018-05-21</th>
      <td>5.242</td>
      <td>5.247</td>
      <td>5.1560</td>
      <td>5.1690</td>
      <td>4.981625</td>
      <td>29991460</td>
    </tr>
    <tr>
      <th>2018-05-22</th>
      <td>5.194</td>
      <td>5.287</td>
      <td>5.1660</td>
      <td>5.2580</td>
      <td>5.067399</td>
      <td>35987383</td>
    </tr>
    <tr>
      <th>2018-05-23</th>
      <td>5.249</td>
      <td>5.249</td>
      <td>5.1250</td>
      <td>5.1600</td>
      <td>4.972951</td>
      <td>44558462</td>
    </tr>
    <tr>
      <th>2018-05-24</th>
      <td>5.170</td>
      <td>5.193</td>
      <td>5.0960</td>
      <td>5.1260</td>
      <td>4.940184</td>
      <td>41132419</td>
    </tr>
    <tr>
      <th>2018-05-25</th>
      <td>5.150</td>
      <td>5.150</td>
      <td>4.8965</td>
      <td>4.9900</td>
      <td>4.809114</td>
      <td>91746984</td>
    </tr>
    <tr>
      <th>2018-05-28</th>
      <td>5.051</td>
      <td>5.069</td>
      <td>4.8700</td>
      <td>4.8880</td>
      <td>4.710812</td>
      <td>54201863</td>
    </tr>
    <tr>
      <th>2018-05-29</th>
      <td>4.780</td>
      <td>4.780</td>
      <td>4.5570</td>
      <td>4.6225</td>
      <td>4.454936</td>
      <td>149494992</td>
    </tr>
    <tr>
      <th>2018-05-30</th>
      <td>4.678</td>
      <td>4.738</td>
      <td>4.5740</td>
      <td>4.6740</td>
      <td>4.504569</td>
      <td>106712823</td>
    </tr>
    <tr>
      <th>2018-05-31</th>
      <td>4.739</td>
      <td>4.809</td>
      <td>4.5385</td>
      <td>4.6000</td>
      <td>4.433251</td>
      <td>110356744</td>
    </tr>
  </tbody>
</table>
</div>



Existe otro método que es mas específico como es **xs**, aunque es más utilizado para los dataframe multi índices. Los cuales dejaremos para mas adelante.


```python
bbva.xs('2018-05', axis=0)
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
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Adj Close</th>
      <th>Volume</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-05-02</th>
      <td>6.718</td>
      <td>6.782</td>
      <td>6.718</td>
      <td>6.765</td>
      <td>6.443224</td>
      <td>13089722</td>
    </tr>
    <tr>
      <th>2018-05-03</th>
      <td>6.760</td>
      <td>6.760</td>
      <td>6.638</td>
      <td>6.666</td>
      <td>6.348933</td>
      <td>21502091</td>
    </tr>
    <tr>
      <th>2018-05-04</th>
      <td>6.680</td>
      <td>6.752</td>
      <td>6.630</td>
      <td>6.742</td>
      <td>6.421319</td>
      <td>15853284</td>
    </tr>
    <tr>
      <th>2018-05-07</th>
      <td>6.770</td>
      <td>6.812</td>
      <td>6.753</td>
      <td>6.788</td>
      <td>6.465130</td>
      <td>13997103</td>
    </tr>
    <tr>
      <th>2018-05-08</th>
      <td>6.791</td>
      <td>6.817</td>
      <td>6.730</td>
      <td>6.756</td>
      <td>6.434652</td>
      <td>14733147</td>
    </tr>
    <tr>
      <th>2018-05-09</th>
      <td>6.768</td>
      <td>6.810</td>
      <td>6.735</td>
      <td>6.806</td>
      <td>6.482275</td>
      <td>13014601</td>
    </tr>
    <tr>
      <th>2018-05-10</th>
      <td>6.820</td>
      <td>6.852</td>
      <td>6.789</td>
      <td>6.852</td>
      <td>6.526086</td>
      <td>11695143</td>
    </tr>
    <tr>
      <th>2018-05-11</th>
      <td>6.852</td>
      <td>6.885</td>
      <td>6.838</td>
      <td>6.854</td>
      <td>6.527991</td>
      <td>10440243</td>
    </tr>
    <tr>
      <th>2018-05-14</th>
      <td>6.845</td>
      <td>6.886</td>
      <td>6.796</td>
      <td>6.833</td>
      <td>6.507990</td>
      <td>11957980</td>
    </tr>
    <tr>
      <th>2018-05-15</th>
      <td>6.828</td>
      <td>6.855</td>
      <td>6.669</td>
      <td>6.729</td>
      <td>6.408937</td>
      <td>23286596</td>
    </tr>
    <tr>
      <th>2018-05-16</th>
      <td>6.708</td>
      <td>6.743</td>
      <td>6.558</td>
      <td>6.620</td>
      <td>6.305121</td>
      <td>26357238</td>
    </tr>
    <tr>
      <th>2018-05-17</th>
      <td>6.640</td>
      <td>6.708</td>
      <td>6.610</td>
      <td>6.707</td>
      <td>6.387983</td>
      <td>21490061</td>
    </tr>
    <tr>
      <th>2018-05-18</th>
      <td>6.700</td>
      <td>6.706</td>
      <td>6.546</td>
      <td>6.580</td>
      <td>6.267024</td>
      <td>32373083</td>
    </tr>
    <tr>
      <th>2018-05-21</th>
      <td>6.610</td>
      <td>6.623</td>
      <td>6.489</td>
      <td>6.508</td>
      <td>6.198449</td>
      <td>25198841</td>
    </tr>
    <tr>
      <th>2018-05-22</th>
      <td>6.526</td>
      <td>6.649</td>
      <td>6.513</td>
      <td>6.615</td>
      <td>6.300359</td>
      <td>16624150</td>
    </tr>
    <tr>
      <th>2018-05-23</th>
      <td>6.572</td>
      <td>6.572</td>
      <td>6.392</td>
      <td>6.467</td>
      <td>6.159399</td>
      <td>35696613</td>
    </tr>
    <tr>
      <th>2018-05-24</th>
      <td>6.484</td>
      <td>6.524</td>
      <td>6.347</td>
      <td>6.386</td>
      <td>6.082252</td>
      <td>20716064</td>
    </tr>
    <tr>
      <th>2018-05-25</th>
      <td>6.408</td>
      <td>6.416</td>
      <td>6.124</td>
      <td>6.208</td>
      <td>5.912718</td>
      <td>38816362</td>
    </tr>
    <tr>
      <th>2018-05-28</th>
      <td>6.307</td>
      <td>6.338</td>
      <td>6.090</td>
      <td>6.134</td>
      <td>5.842238</td>
      <td>25479382</td>
    </tr>
    <tr>
      <th>2018-05-29</th>
      <td>6.070</td>
      <td>6.087</td>
      <td>5.850</td>
      <td>5.878</td>
      <td>5.598414</td>
      <td>49828929</td>
    </tr>
    <tr>
      <th>2018-05-30</th>
      <td>5.950</td>
      <td>6.022</td>
      <td>5.825</td>
      <td>5.916</td>
      <td>5.634607</td>
      <td>38820861</td>
    </tr>
    <tr>
      <th>2018-05-31</th>
      <td>5.981</td>
      <td>6.066</td>
      <td>5.783</td>
      <td>5.839</td>
      <td>5.561269</td>
      <td>54235540</td>
    </tr>
  </tbody>
</table>
</div>



Pandas tambien permiter hacer una extracción (slice) usando saltos, es decir tomando los valores de cada N filas. Por ejemplo podemos tomar cada 15 filas. En este caso despues usamos **tail()** para limitar lo que se muestra a solo los 8 últimos seleccionados por facilitar la visualización.


```python
san[::15].tail(8)
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
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Adj Close</th>
      <th>Volume</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-07-27</th>
      <td>4.7795</td>
      <td>4.8520</td>
      <td>4.7650</td>
      <td>4.8180</td>
      <td>4.643349</td>
      <td>51335277</td>
    </tr>
    <tr>
      <th>2018-08-17</th>
      <td>4.3955</td>
      <td>4.3955</td>
      <td>4.3110</td>
      <td>4.3395</td>
      <td>4.239388</td>
      <td>42357176</td>
    </tr>
    <tr>
      <th>2018-09-07</th>
      <td>4.2425</td>
      <td>4.2550</td>
      <td>4.1400</td>
      <td>4.1780</td>
      <td>4.081614</td>
      <td>53997610</td>
    </tr>
    <tr>
      <th>2018-09-28</th>
      <td>4.4335</td>
      <td>4.4345</td>
      <td>4.2520</td>
      <td>4.3355</td>
      <td>4.235480</td>
      <td>69807695</td>
    </tr>
    <tr>
      <th>2018-10-19</th>
      <td>4.1100</td>
      <td>4.1685</td>
      <td>4.0270</td>
      <td>4.1250</td>
      <td>4.063220</td>
      <td>92057905</td>
    </tr>
    <tr>
      <th>2018-11-09</th>
      <td>4.2545</td>
      <td>4.2690</td>
      <td>4.1955</td>
      <td>4.2390</td>
      <td>4.175512</td>
      <td>35140481</td>
    </tr>
    <tr>
      <th>2018-11-30</th>
      <td>4.2270</td>
      <td>4.2300</td>
      <td>4.1515</td>
      <td>4.1850</td>
      <td>4.122321</td>
      <td>38399674</td>
    </tr>
    <tr>
      <th>2018-12-21</th>
      <td>3.9600</td>
      <td>3.9955</td>
      <td>3.8815</td>
      <td>3.9305</td>
      <td>3.871633</td>
      <td>212350900</td>
    </tr>
  </tbody>
</table>
</div>



Esto puede ser utilizado incluso para invertir el orden del índice, usando un paso negativo.


```python
bbva[::-1].head(6)
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
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Adj Close</th>
      <th>Volume</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-12-31</th>
      <td>4.6350</td>
      <td>4.6635</td>
      <td>4.6200</td>
      <td>4.6355</td>
      <td>4.500526</td>
      <td>6885185</td>
    </tr>
    <tr>
      <th>2018-12-28</th>
      <td>4.5585</td>
      <td>4.6480</td>
      <td>4.5500</td>
      <td>4.6410</td>
      <td>4.505866</td>
      <td>20924025</td>
    </tr>
    <tr>
      <th>2018-12-27</th>
      <td>4.6000</td>
      <td>4.6380</td>
      <td>4.4765</td>
      <td>4.5450</td>
      <td>4.412662</td>
      <td>32726196</td>
    </tr>
    <tr>
      <th>2018-12-24</th>
      <td>4.5745</td>
      <td>4.5990</td>
      <td>4.5425</td>
      <td>4.5580</td>
      <td>4.425283</td>
      <td>5652399</td>
    </tr>
    <tr>
      <th>2018-12-21</th>
      <td>4.6330</td>
      <td>4.6600</td>
      <td>4.5340</td>
      <td>4.6185</td>
      <td>4.484022</td>
      <td>96489872</td>
    </tr>
    <tr>
      <th>2018-12-20</th>
      <td>4.6500</td>
      <td>4.7150</td>
      <td>4.6230</td>
      <td>4.6540</td>
      <td>4.518487</td>
      <td>27462924</td>
    </tr>
  </tbody>
</table>
</div>



## Indexación booleana

Otra forma de extraer datos es usando una condición y solo nos devolverá la filas que cumplan dicha condición. Así por ejemplo podemos extraer las filas en las que el cierre de Santander supero los 13 euros, comrobando que solo fueron dos.


```python
san[san['Close']>13]
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
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Adj Close</th>
      <th>Volume</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2008-01-02</th>
      <td>13.2489</td>
      <td>13.3302</td>
      <td>13.0953</td>
      <td>13.1766</td>
      <td>5.868722</td>
      <td>103998100</td>
    </tr>
    <tr>
      <th>2008-01-03</th>
      <td>13.1405</td>
      <td>13.2037</td>
      <td>12.9689</td>
      <td>13.0502</td>
      <td>5.812426</td>
      <td>113222703</td>
    </tr>
  </tbody>
</table>
</div>



La condición puede ser tan compleja como queramos, pudiendo usar los operadores lógicos para encadenar distintos condicionales.


```python
bbva[(bbva.Open>15) & (bbva.Volume>10**8)]
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
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Adj Close</th>
      <th>Volume</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2008-01-04</th>
      <td>15.7946</td>
      <td>15.7946</td>
      <td>15.3239</td>
      <td>15.4680</td>
      <td>8.089549</td>
      <td>138136794</td>
    </tr>
    <tr>
      <th>2008-01-09</th>
      <td>15.2374</td>
      <td>15.2374</td>
      <td>14.9972</td>
      <td>15.0452</td>
      <td>7.868430</td>
      <td>107909320</td>
    </tr>
  </tbody>
</table>
</div>



Vemos además como en el ejemplo anterior hemos llamado las columnas **Open** y **Volume** sin usar los corchetes ni las comillas. Y es que si el nombre de la columna es una sola palabra (no contiene espacios) podemos llamarla usando solo un punto, como si de una propiedad del objeto dataframe se tratara.

Esto mismo tambien es posible hacerlo usando el método **query()**. Obtendremos exactamente el mismo resultado, solo que usando una expresión contenida en una cadena de texto para realizar la busqueda.


```python
bbva.query('Open>15 and Volume>10**8')
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
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Adj Close</th>
      <th>Volume</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2008-01-04</th>
      <td>15.7946</td>
      <td>15.7946</td>
      <td>15.3239</td>
      <td>15.4680</td>
      <td>8.089549</td>
      <td>138136794</td>
    </tr>
    <tr>
      <th>2008-01-09</th>
      <td>15.2374</td>
      <td>15.2374</td>
      <td>14.9972</td>
      <td>15.0452</td>
      <td>7.868430</td>
      <td>107909320</td>
    </tr>
  </tbody>
</table>
</div>



Dado que los dataframes **san** y **bbva** tienen el mismo tamaño (de hecho el mismo índice por cotizar en el mismo mercado), podemos usar una condición aplicada Santander para extraer valores del BBVA. Así por ejemplo podemos ver como cotizaba BBVA cuando Santander superó los 13 euros en su precio de cierre.


```python
bbva[san.Close>13]
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
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Adj Close</th>
      <th>Volume</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2008-01-02</th>
      <td>16.1021</td>
      <td>16.1597</td>
      <td>15.8523</td>
      <td>15.9291</td>
      <td>8.330698</td>
      <td>98910228</td>
    </tr>
    <tr>
      <th>2008-01-03</th>
      <td>15.9291</td>
      <td>15.9291</td>
      <td>15.6986</td>
      <td>15.7946</td>
      <td>8.260358</td>
      <td>90699092</td>
    </tr>
  </tbody>
</table>
</div>





Si quieres ampliar información la propia documentación oficial de Pandas explica muy detalladamente estos métodos de extracción y algún otro.
