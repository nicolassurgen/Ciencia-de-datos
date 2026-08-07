---
titulo: Pandas - Introducción a Series y DataFrame
materia: Pandas
tipo: apunte
tags:
  - pandas
  - tecnologias
  - python
  - tema/introduccion
fuente: "pandas — Intro to data structures (pandas.pydata.org/docs/user_guide/dsintro.html); Python Data Science Handbook (Jake VanderPlas) — Parte III"
---

# Introducción a Series y DataFrame

> [!definition] Pandas
> La librería de manipulación de datos tabulares de Python. Se construye **sobre** [[01 - Introduccion y arrays|NumPy]] — por dentro, cada columna de Pandas es (esencialmente) un array de NumPy con una capa extra: **etiquetas** en vez de solo posiciones numéricas.

```python
import numpy as np
import pandas as pd
```

Este par de imports va a encabezar prácticamente todos tus notebooks de acá en adelante.

## Los tres objetos fundamentales

![[Anatomia de un DataFrame.png]]

### Series — un array con etiquetas

```python
poblacion = pd.Series([39538223, 29145505, 21538187],
                       index=['California', 'Texas', 'Florida'])
poblacion['California']    # 39538223
```

> [!important] La diferencia con un array de NumPy
> Un array de NumPy tiene un índice **implícito** (posiciones 0, 1, 2...). Una `Series` de Pandas tiene un índice **explícito**, que vos elegís — puede ser texto, fechas, números salteados, lo que sea. Es la misma idea de [[distribución de frecuencias|tabla de frecuencias]] de Estadística: cada valor está asociado a una etiqueta con significado, no a una posición arbitraria.

Una forma muy natural de pensar una `Series`: es como un **diccionario de Python** (ver [[listas, tuplas, diccionarios y conjuntos]] de Algoritmos), pero con superpoderes — mantiene orden, permite slicing, y todas las operaciones vectorizadas de NumPy funcionan sobre ella. De hecho, se puede construir directo de un dict:

```python
pd.Series({'California': 39538223, 'Texas': 29145505, 'Florida': 21538187})
# California    39538223
# Texas         29145505
# Florida       21538187
# dtype: int64
```

### DataFrame — varias Series que comparten el mismo Index

```python
area = pd.Series({'California': 423967, 'Texas': 695662, 'Florida': 170312})

estados = pd.DataFrame({'population': poblacion, 'area': area})
estados
#             population    area
# California    39538223  423967
# Texas         29145505  695662
# Florida       21538187  170312
```

Como muestra el diagrama: **cada columna de un DataFrame es una Series**, y todas comparten el mismo `Index` (las etiquetas de fila). Esto es exactamente la [[01 - Como dar sentido a los datos|matriz de datos]] de Estadística: individuos en las filas, variables en las columnas — con la diferencia de que acá las filas y columnas tienen **nombre**, no solo posición.

### Index — el objeto que hace posible todo esto

```python
estados.index      # Index(['California', 'Texas', 'Florida'])
estados.columns     # Index(['population', 'area'])
```

`Index` es, básicamente, un array **inmutable** (ver [[mutabilidad e inmutabilidad]] de Algoritmos) — no podés modificar sus elementos directamente, lo cual permite que Pandas lo comparta de forma segura entre varias Series sin riesgo de que una modificación en un lado rompa el índice de otra estructura.

## Crear un DataFrame: las formas más comunes

```python
pd.DataFrame({'population': poblacion, 'area': area})     # desde un dict de Series (o listas) -> el mismo resultado de arriba

pd.DataFrame(np.random.rand(3, 2), columns=['a', 'b'], index=['x', 'y', 'z'])  # desde un array de NumPy
#           a         b
# x  0.548814  0.715189
# y  0.602763  0.544883
# z  0.423655  0.645894

pd.read_csv('archivo.csv')     # desde un archivo — la forma más común en la práctica (el resultado depende del CSV)
```

## Primera exploración de un DataFrame

```python
estados.shape         # (3, 2)  -> (filas, columnas)
estados.columns       # Index(['population', 'area'], dtype='object')
estados.dtypes
# population    int64
# area          int64
# dtype: object
```

Sobre un `df` más grande (leído con `pd.read_csv`), además: `df.head()` (primeras 5 filas), `df.info()` (tipos y cantidad de no-nulos por columna) y `df.describe()` — resumen de 5 números + media + std de cada columna numérica de una sola vez (ver [[medidas de posición]]).

`df.describe()` es, en una sola línea, el resumen de [[medidas de posición]] y [[medidas de dispersión]] de Estadística aplicado a **todas** las columnas numéricas a la vez.

## Recorrido de estas notas

1. **Introducción a Series y DataFrame** *(esta nota)*
2. [[02 - Indexado y seleccion (loc, iloc)]] — acceder a filas, columnas y celdas sin ambigüedad.
3. [[03 - Operaciones y alineacion de datos]] — qué pasa cuando operás entre Series con índices distintos.
4. [[04 - Datos faltantes]] — `NaN`, `isnull()`, `dropna()`, `fillna()`.
5. [[05 - Combinar datasets (concat, merge, join)]] — juntar varias tablas.
6. [[06 - Agregacion y groupby]] — el "agrupar por" de SQL, en Python.
7. [[07 - Tablas dinamicas (pivot_table)]] — resúmenes cruzados de dos variables.
8. [[08 - Series de tiempo]] — trabajar con fechas.
9. [[09 - Indices jerarquicos (MultiIndex)]] — más de un nivel de índice.
10. [[10 - Operaciones de texto vectorizadas]] — limpiar y transformar columnas de texto.
11. [[11 - Alto rendimiento (eval y query)]] — evitar arrays intermedios en DataFrames grandes.

## Relacionado
- [[01 - Introduccion y arrays]]
- [[01 - Como dar sentido a los datos]]
- [[listas, tuplas, diccionarios y conjuntos]]
