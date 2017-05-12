# Blaze Ecosystem
---
layout: default
---

# [](#header-2) Descripción del Trabajo

# [](#header-2) Resumen

# [](#header-2) Introducción

# [](#header-2) Motivo y Descarga de Responsabilidad

# [](#header-2) Blaze

	a)Split-Apply-combine-Grouping rogger
	b)Pandas to blaze briggette
	c)Sql to blaze victor



### Pandas a Blaze

Llevando los datos desde un Dataframe a Un objeto Blaze


```python
import numpy as np
import pandas as pd
from time import time
from odo import odo
from blaze import data,by,join,merge ,concat
```


```python
df1 = pd.DataFrame({
    'name':['Alice', 'Raquel','Jose','Raquel'],
    'monto':[100,200,300,400],
    'id':[1,2,3,4]
})
df_1=df1
df1

```



<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>monto</th>
      <th>name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>100</td>
      <td>Alice</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>200</td>
      <td>Raquel</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>300</td>
      <td>Jose</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>400</td>
      <td>Raquel</td>
    </tr>
  </tbody>
</table>
</div>




```python
type(df1)
```




    pandas.core.frame.DataFrame




```python
df2 = data(df1)
df_2=df2
df2
```




<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>monto</th>
      <th>name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>100</td>
      <td>Alice</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>200</td>
      <td>Raquel</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>300</td>
      <td>Jose</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>400</td>
      <td>Raquel</td>
    </tr>
  </tbody>
</table>




```python
type(df2)
```




    blaze.interactive._Data




```python
tiempo_inicial = time()
df1.monto*2
tiempo_final = time()
print(tiempo_final - tiempo_inicial)

tiempo_inicial = time()
df2.monto*2
tiempo_final = time()
print(tiempo_final - tiempo_inicial)
```

    0.0004684925079345703
    0.00023651123046875



```python
tiempo_inicial = time()
df1[['id','monto']]
tiempo_final = time()
print(tiempo_final - tiempo_inicial)

tiempo_inicial = time()
df2[['id','monto']]
tiempo_final = time()
print(tiempo_final - tiempo_inicial)
```

    0.0007827281951904297
    0.000118255615234375



```python
tiempo_inicial = time()
df1[df1.monto > 300]
tiempo_final = time()
print(tiempo_final - tiempo_inicial)

tiempo_inicial = time()
df2[df2.monto > 300]
tiempo_final = time()
print(tiempo_final - tiempo_inicial)
```

    0.0008072853088378906
    0.0003752708435058594



```python

tiempo_inicial = time()
df1.groupby('name').monto.mean()
df1.groupby(['name', 'id']).monto.mean()
tiempo_final = time()
print(tiempo_final - tiempo_inicial)

tiempo_inicial = time()
by(df2.monto, monto = df2.monto.mean())
by(merge(df2.monto,df2.id), monto = df2.monto.mean())
tiempo_final = time()
print(tiempo_final - tiempo_inicial)
```

    0.0026047229766845703
    0.0004889965057373047



```python
pd.merge(df1,df_1,on='name')
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id_x</th>
      <th>monto_x</th>
      <th>name</th>
      <th>id_y</th>
      <th>monto_y</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>100</td>
      <td>Alice</td>
      <td>1</td>
      <td>100</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>200</td>
      <td>Raquel</td>
      <td>2</td>
      <td>200</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>200</td>
      <td>Raquel</td>
      <td>4</td>
      <td>400</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>400</td>
      <td>Raquel</td>
      <td>2</td>
      <td>200</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>400</td>
      <td>Raquel</td>
      <td>4</td>
      <td>400</td>
    </tr>
    <tr>
      <th>5</th>
      <td>3</td>
      <td>300</td>
      <td>Jose</td>
      <td>3</td>
      <td>300</td>
    </tr>
  </tbody>
</table>
</div>




```python
join(df2, df_2, 'name')
```




<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>id_left</th>
      <th>monto_left</th>
      <th>id_right</th>
      <th>monto_right</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Alice</td>
      <td>1</td>
      <td>100</td>
      <td>1</td>
      <td>100</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Raquel</td>
      <td>2</td>
      <td>200</td>
      <td>2</td>
      <td>200</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Raquel</td>
      <td>2</td>
      <td>200</td>
      <td>4</td>
      <td>400</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Raquel</td>
      <td>4</td>
      <td>400</td>
      <td>2</td>
      <td>200</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Raquel</td>
      <td>4</td>
      <td>400</td>
      <td>4</td>
      <td>400</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Jose</td>
      <td>3</td>
      <td>300</td>
      <td>3</td>
      <td>300</td>
    </tr>
  </tbody>
</table>




```python
df1.monto.map(lambda x: x+ 1)
```




    0    101
    1    201
    2    301
    3    401
    Name: monto, dtype: int64




```python
df2.monto.map(lambda x: x+ 1,'int64')
```




<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>monto</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>101</td>
    </tr>
    <tr>
      <th>1</th>
      <td>201</td>
    </tr>
    <tr>
      <th>2</th>
      <td>301</td>
    </tr>
    <tr>
      <th>3</th>
      <td>401</td>
    </tr>
  </tbody>
</table>




```python
df1.rename(columns={'name': 'alias',
'monto': 'dollars'})
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>dollars</th>
      <th>alias</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>100</td>
      <td>Alice</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>200</td>
      <td>Raquel</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>300</td>
      <td>Jose</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>400</td>
      <td>Raquel</td>
    </tr>
  </tbody>
</table>
</div>




```python
df1.drop_duplicates()
df1.name.drop_duplicates()
```




    0     Alice
    1    Raquel
    2      Jose
    Name: name, dtype: object




```python
df2.distinct()
df2.name.distinct()
```




<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Alice</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Raquel</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Jose</td>
    </tr>
  </tbody>
</table>



## Usando CSV

Cargar una data grande requiere de mucho tiempo, mas aun que actualmente se trabaja con cantidades de datos que superan los gigas teras o petabytes


```python
tiempo_inicial = time()
df3 = pd.read_csv('2008.csv',index_col=)
tiempo_final = time()
print(tiempo_final - tiempo_inicial)

tiempo_inicial = time()
df4 = data('2008.csv')
tiempo_final = time()
print(tiempo_final - tiempo_inicial)
```

    180.35243368148804
    37.64379167556763



```python
df3.head
```




    <bound method NDFrame.head of          Year  Month  DayofMonth  DayOfWeek  DepTime  CRSDepTime  ArrTime  \
    0        2008      1           3          4   2003.0        1955   2211.0   
    1        2008      1           3          4    754.0         735   1002.0   
    2        2008      1           3          4    628.0         620    804.0   
    3        2008      1           3          4    926.0         930   1054.0   
    4        2008      1           3          4   1829.0        1755   1959.0   
    5        2008      1           3          4   1940.0        1915   2121.0   
    6        2008      1           3          4   1937.0        1830   2037.0   
    7        2008      1           3          4   1039.0        1040   1132.0   
    8        2008      1           3          4    617.0         615    652.0   
    9        2008      1           3          4   1620.0        1620   1639.0   
    10       2008      1           3          4    706.0         700    916.0   
    11       2008      1           3          4   1644.0        1510   1845.0   
    12       2008      1           3          4   1426.0        1430   1426.0   
    13       2008      1           3          4    715.0         715    720.0   
    14       2008      1           3          4   1702.0        1700   1651.0   
    15       2008      1           3          4   1029.0        1020   1021.0   
    16       2008      1           3          4   1452.0        1425   1640.0   
    17       2008      1           3          4    754.0         745    940.0   
    18       2008      1           3          4   1323.0        1255   1526.0   
    19       2008      1           3          4   1416.0        1325   1512.0   
    20       2008      1           3          4    706.0         705    807.0   
    21       2008      1           3          4   1657.0        1625   1754.0   
    22       2008      1           3          4   1900.0        1840   1956.0   
    23       2008      1           3          4   1039.0        1030   1133.0   
    24       2008      1           3          4    801.0         800    902.0   
    25       2008      1           3          4   1520.0        1455   1619.0   
    26       2008      1           3          4   1422.0        1255   1657.0   
    27       2008      1           3          4   1954.0        1925   2239.0   
    28       2008      1           3          4    636.0         635    921.0   
    29       2008      1           3          4    734.0         730    958.0   
    ...       ...    ...         ...        ...      ...         ...      ...   
    7009698  2008     12          13          6   1625.0        1635   1744.0   
    7009699  2008     12          13          6   1254.0        1221   1420.0   
    7009700  2008     12          13          6   1842.0        1845   1953.0   
    7009701  2008     12          13          6   1528.0        1500   1720.0   
    7009702  2008     12          13          6   1531.0        1522   1822.0   
    7009703  2008     12          13          6   1910.0        1910   2017.0   
    7009704  2008     12          13          6   1441.0        1445   1604.0   
    7009705  2008     12          13          6    921.0         830   1112.0   
    7009706  2008     12          13          6   1435.0        1440   1701.0   
    7009707  2008     12          13          6   1750.0        1755   2010.0   
    7009708  2008     12          13          6    706.0         710    850.0   
    7009709  2008     12          13          6   1552.0        1520   1735.0   
    7009710  2008     12          13          6   1250.0        1220   1617.0   
    7009711  2008     12          13          6   1033.0        1041   1255.0   
    7009712  2008     12          13          6    840.0         843   1025.0   
    7009713  2008     12          13          6    810.0         815   1504.0   
    7009714  2008     12          13          6    547.0         545    646.0   
    7009715  2008     12          13          6    848.0         850   1024.0   
    7009716  2008     12          13          6    936.0         936   1114.0   
    7009717  2008     12          13          6    657.0         600    904.0   
    7009718  2008     12          13          6   1007.0         847   1149.0   
    7009719  2008     12          13          6    638.0         640    808.0   
    7009720  2008     12          13          6    756.0         800   1032.0   
    7009721  2008     12          13          6    612.0         615    923.0   
    7009722  2008     12          13          6    749.0         750    901.0   
    7009723  2008     12          13          6   1002.0         959   1204.0   
    7009724  2008     12          13          6    834.0         835   1021.0   
    7009725  2008     12          13          6    655.0         700    856.0   
    7009726  2008     12          13          6   1251.0        1240   1446.0   
    7009727  2008     12          13          6   1110.0        1103   1413.0   

             CRSArrTime UniqueCarrier  FlightNum        ...         TaxiIn  \
    0              2225            WN        335        ...            4.0   
    1              1000            WN       3231        ...            5.0   
    2               750            WN        448        ...            3.0   
    3              1100            WN       1746        ...            3.0   
    4              1925            WN       3920        ...            3.0   
    5              2110            WN        378        ...            4.0   
    6              1940            WN        509        ...            3.0   
    7              1150            WN        535        ...            7.0   
    8               650            WN         11        ...            6.0   
    9              1655            WN        810        ...            3.0   
    10              915            WN        100        ...            5.0   
    11             1725            WN       1333        ...            6.0   
    12             1425            WN        829        ...            9.0   
    13              710            WN       1016        ...            7.0   
    14             1655            WN       1827        ...            4.0   
    15             1010            WN       2272        ...            6.0   
    16             1625            WN        675        ...            7.0   
    17              955            WN       1144        ...            5.0   
    18             1510            WN          4        ...            4.0   
    19             1435            WN         54        ...            2.0   
    20              810            WN         68        ...            3.0   
    21             1735            WN        623        ...            5.0   
    22             1950            WN        717        ...            2.0   
    23             1140            WN       1244        ...            2.0   
    24              910            WN       2101        ...            3.0   
    25             1605            WN       2553        ...            2.0   
    26             1610            WN        188        ...            6.0   
    27             2235            WN       1754        ...            3.0   
    28              945            WN       2275        ...            5.0   
    29             1020            WN        550        ...            2.0   
    ...             ...           ...        ...        ...            ...   
    7009698        1758            DL       1605        ...           12.0   
    7009699        1359            DL       1609        ...            9.0   
    7009700        2006            DL       1610        ...            8.0   
    7009701        1642            DL       1611        ...            4.0   
    7009702        1823            DL       1612        ...            9.0   
    7009703        2016            DL       1612        ...            5.0   
    7009704        1622            DL       1613        ...            8.0   
    7009705        1008            DL       1616        ...            8.0   
    7009706        1704            DL       1618        ...           20.0   
    7009707        2015            DL       1618        ...            7.0   
    7009708         837            DL       1619        ...           23.0   
    7009709        1718            DL       1620        ...            9.0   
    7009710        1552            DL       1621        ...            9.0   
    7009711        1303            DL       1622        ...            9.0   
    7009712        1021            DL       1624        ...            6.0   
    7009713        1526            DL       1625        ...            7.0   
    7009714         650            DL       1627        ...            8.0   
    7009715        1005            DL       1628        ...            4.0   
    7009716        1119            DL       1630        ...            4.0   
    7009717         749            DL       1631        ...           15.0   
    7009718        1010            DL       1631        ...            8.0   
    7009719         753            DL       1632        ...           14.0   
    7009720        1026            DL       1633        ...           23.0   
    7009721         907            DL       1635        ...            5.0   
    7009722         859            DL       1636        ...           20.0   
    7009723        1150            DL       1636        ...            6.0   
    7009724        1023            DL       1637        ...            5.0   
    7009725         856            DL       1638        ...           24.0   
    7009726        1437            DL       1639        ...           13.0   
    7009727        1418            DL       1641        ...            8.0   

             TaxiOut  Cancelled  CancellationCode  Diverted  CarrierDelay  \
    0            8.0          0               NaN         0           NaN   
    1           10.0          0               NaN         0           NaN   
    2           17.0          0               NaN         0           NaN   
    3            7.0          0               NaN         0           NaN   
    4           10.0          0               NaN         0           2.0   
    5           10.0          0               NaN         0           NaN   
    6            7.0          0               NaN         0          10.0   
    7            7.0          0               NaN         0           NaN   
    8           19.0          0               NaN         0           NaN   
    9            6.0          0               NaN         0           NaN   
    10          19.0          0               NaN         0           NaN   
    11           8.0          0               NaN         0           8.0   
    12          12.0          0               NaN         0           NaN   
    13          21.0          0               NaN         0           NaN   
    14          10.0          0               NaN         0           NaN   
    15           9.0          0               NaN         0           NaN   
    16           8.0          0               NaN         0           3.0   
    17          16.0          0               NaN         0           NaN   
    18           9.0          0               NaN         0           0.0   
    19           5.0          0               NaN         0          12.0   
    20           7.0          0               NaN         0           NaN   
    21           5.0          0               NaN         0           7.0   
    22           5.0          0               NaN         0           NaN   
    23           5.0          0               NaN         0           NaN   
    24           5.0          0               NaN         0           NaN   
    25           7.0          0               NaN         0           NaN   
    26           6.0          0               NaN         0          40.0   
    27           7.0          0               NaN         0           NaN   
    28          13.0          0               NaN         0           NaN   
    29           8.0          0               NaN         0           NaN   
    ...          ...        ...               ...       ...           ...   
    7009698     21.0          0               NaN         0           NaN   
    7009699     13.0          0               NaN         0           0.0   
    7009700     11.0          0               NaN         0           NaN   
    7009701     29.0          0               NaN         0          16.0   
    7009702     14.0          0               NaN         0           NaN   
    7009703     24.0          0               NaN         0           NaN   
    7009704     10.0          0               NaN         0           NaN   
    7009705     21.0          0               NaN         0          51.0   
    7009706     10.0          0               NaN         0           NaN   
    7009707     20.0          0               NaN         0           NaN   
    7009708     32.0          0               NaN         0           NaN   
    7009709      7.0          0               NaN         0           0.0   
    7009710     18.0          0               NaN         0           3.0   
    7009711     15.0          0               NaN         0           NaN   
    7009712     46.0          0               NaN         0           NaN   
    7009713     17.0          0               NaN         0           NaN   
    7009714     13.0          0               NaN         0           NaN   
    7009715     44.0          0               NaN         0           0.0   
    7009716     24.0          0               NaN         0           NaN   
    7009717     34.0          0               NaN         0           0.0   
    7009718     32.0          0               NaN         0           1.0   
    7009719     26.0          0               NaN         0           0.0   
    7009720     17.0          0               NaN         0           NaN   
    7009721     23.0          0               NaN         0           0.0   
    7009722     11.0          0               NaN         0           NaN   
    7009723     45.0          0               NaN         0           NaN   
    7009724     23.0          0               NaN         0           NaN   
    7009725     12.0          0               NaN         0           NaN   
    7009726     13.0          0               NaN         0           NaN   
    7009727     11.0          0               NaN         0           NaN   

            WeatherDelay NASDelay  SecurityDelay  LateAircraftDelay  
    0                NaN      NaN            NaN                NaN  
    1                NaN      NaN            NaN                NaN  
    2                NaN      NaN            NaN                NaN  
    3                NaN      NaN            NaN                NaN  
    4                0.0      0.0            0.0               32.0  
    5                NaN      NaN            NaN                NaN  
    6                0.0      0.0            0.0               47.0  
    7                NaN      NaN            NaN                NaN  
    8                NaN      NaN            NaN                NaN  
    9                NaN      NaN            NaN                NaN  
    10               NaN      NaN            NaN                NaN  
    11               0.0      0.0            0.0               72.0  
    12               NaN      NaN            NaN                NaN  
    13               NaN      NaN            NaN                NaN  
    14               NaN      NaN            NaN                NaN  
    15               NaN      NaN            NaN                NaN  
    16               0.0      0.0            0.0               12.0  
    17               NaN      NaN            NaN                NaN  
    18               0.0      0.0            0.0               16.0  
    19               0.0      0.0            0.0               25.0  
    20               NaN      NaN            NaN                NaN  
    21               0.0      0.0            0.0               12.0  
    22               NaN      NaN            NaN                NaN  
    23               NaN      NaN            NaN                NaN  
    24               NaN      NaN            NaN                NaN  
    25               NaN      NaN            NaN                NaN  
    26               0.0      0.0            0.0                7.0  
    27               NaN      NaN            NaN                NaN  
    28               NaN      NaN            NaN                NaN  
    29               NaN      NaN            NaN                NaN  
    ...              ...      ...            ...                ...  
    7009698          NaN      NaN            NaN                NaN  
    7009699          0.0      0.0            0.0               21.0  
    7009700          NaN      NaN            NaN                NaN  
    7009701          0.0     10.0            0.0               12.0  
    7009702          NaN      NaN            NaN                NaN  
    7009703          NaN      NaN            NaN                NaN  
    7009704          NaN      NaN            NaN                NaN  
    7009705          0.0     13.0            0.0                0.0  
    7009706          NaN      NaN            NaN                NaN  
    7009707          NaN      NaN            NaN                NaN  
    7009708          NaN      NaN            NaN                NaN  
    7009709          0.0      0.0            0.0               17.0  
    7009710          0.0      0.0            0.0               22.0  
    7009711          NaN      NaN            NaN                NaN  
    7009712          NaN      NaN            NaN                NaN  
    7009713          NaN      NaN            NaN                NaN  
    7009714          NaN      NaN            NaN                NaN  
    7009715          0.0     19.0            0.0                0.0  
    7009716          NaN      NaN            NaN                NaN  
    7009717         57.0     18.0            0.0                0.0  
    7009718          0.0     19.0            0.0               79.0  
    7009719          0.0     15.0            0.0                0.0  
    7009720          NaN      NaN            NaN                NaN  
    7009721          0.0     16.0            0.0                0.0  
    7009722          NaN      NaN            NaN                NaN  
    7009723          NaN      NaN            NaN                NaN  
    7009724          NaN      NaN            NaN                NaN  
    7009725          NaN      NaN            NaN                NaN  
    7009726          NaN      NaN            NaN                NaN  
    7009727          NaN      NaN            NaN                NaN  

    [7009728 rows x 29 columns]>




```python
df4.head
```




    <bound method head of <'CSV' data; _name='_6', dshape='var * {  Year: int64,  Month: int64,  DayofMonth: ...'>>




```python
tiempo_inicial = time()
df3.to_csv( 'output1.csv')
tiempo_final = time()
print(tiempo_final - tiempo_inicial)
```

    100.374751329422




# [](#header-4) Qué no hace Blaze:

1. Blaze de vez en cuando sufre de excesos. Los términos Big-Data y Pandas inevitablemente se confunden en la mente de la gente para convertirse en algo inalcanzable y llevarlos a la decepción. Blaze es limitado; aprender sus limitaciones puede dirigirle a una mayor productividad.
2.  Blaze no reemplaza a Pandas. Pandas siempre tendrá más herramientas y será más maduro que Blaze. Hay cosas que simplemente no puede hacer si desea generalizar fuera de la memoria.

**Recomendación:** Si sus datos se ajustan perfectamente a la memoria, utilice NumPy / Pandas. Sus datos probablemente encajen muy bien en la memoria.

# [](#header-2) Implemtación
# [](#header-2) Conclusiones

Text can be **bold**, _italic_, or ~~strikethrough~~.

[Link to another page](another-page).

There should be whitespace between paragraphs.

There should be whitespace between paragraphs. We recommend including a README, or a file with information about your project.

# [](#header-1)Header 1

This is a normal paragraph following a header. GitHub is a code hosting platform for version control and collaboration. It lets you and others work together on projects from anywhere.

## [](#header-2)Header 2

> This is a blockquote following a header.
>
> When something is important enough, you do it even if the odds are not in your favor.

### [](#header-3)Header 3

```js
// Javascript code with syntax highlighting.
var fun = function lang(l) {
  dateformat.i18n = require('./lang/' + l)
  return true;
}
```

```ruby
# Ruby code with syntax highlighting
GitHubPages::Dependencies.gems.each do |gem, version|
  s.add_dependency(gem, "= #{version}")
end
```

#### [](#header-4)Header 4

*   This is an unordered list following a header.
*   This is an unordered list following a header.
*   This is an unordered list following a header.

##### [](#header-5)Header 5

1.  This is an ordered list following a header.
2.  This is an ordered list following a header.
3.  This is an ordered list following a header.

###### [](#header-6)Header 6

| head1        | head two          | three |
|:-------------|:------------------|:------|
| ok           | good swedish fish | nice  |
| out of stock | good and plenty   | nice  |
| ok           | good `oreos`      | hmm   |
| ok           | good `zoute` drop | yumm  |

### There's a horizontal rule below this.

* * *

### Here is an unordered list:

*   Item foo
*   Item bar
*   Item baz
*   Item zip

### And an ordered list:

1.  Item one
1.  Item two
1.  Item three
1.  Item four

### And a nested list:

- level 1 item
  - level 2 item
  - level 2 item
    - level 3 item
    - level 3 item
- level 1 item
  - level 2 item
  - level 2 item
  - level 2 item
- level 1 item
  - level 2 item
  - level 2 item
- level 1 item

### Small image

![](https://assets-cdn.github.com/images/icons/emoji/octocat.png)

### Large image

![](https://guides.github.com/activities/hello-world/branching.png)


### Definition lists can be used with HTML syntax.

<dl>
<dt>Name</dt>
<dd>Godzilla</dd>
<dt>Born</dt>
<dd>1952</dd>
<dt>Birthplace</dt>
<dd>Japan</dd>
<dt>Color</dt>
<dd>Green</dd>
</dl>

```
Long, single-line code blocks should not wrap. They should horizontally scroll if they are too long. This line should be long enough to demonstrate this.
```

```
The final element.
```
