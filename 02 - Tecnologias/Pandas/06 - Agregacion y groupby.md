---
titulo: Pandas - Agregación y groupby
materia: Pandas
tipo: apunte
tags:
  - pandas
  - tecnologias
  - python
  - tema/agregacion
fuente: "pandas — Group by: split-apply-combine (pandas.pydata.org/docs/user_guide/groupby.html); Python Data Science Handbook (Jake VanderPlas) — Parte III"
---

# Agregación y groupby

Esta es, para el análisis de datos real, la herramienta más usada de todo Pandas. El nombre viene de SQL ("*group by*"), pero conviene pensarlo con el término que popularizó Hadley Wickham (el creador de `dplyr` en R): **split, apply, combine**.

## El concepto: split → apply → combine

> [!definition] Split, Apply, Combine
> - **Split**: separar los datos en grupos según el valor de una columna (la "clave").
> - **Apply**: calcular algo (típicamente una agregación) **dentro de cada grupo**, por separado.
> - **Combine**: juntar los resultados de todos los grupos en una única tabla de salida.

![[Split-apply-combine.png]]

```python
df = pd.DataFrame({'key': ['A', 'B', 'C', 'A', 'B', 'C'], 'data': range(6)})
df.groupby('key').sum()
#      data
# key
# A       3
# B       5
# C       7
```

> [!important] Esto es exactamente el "group by" del que hablamos en Algoritmos
> Compará con el patrón manual de [[lista de diccionarios y JSON]] (Algoritmos): un diccionario acumulador, un loop, sumando `masa_g` por especie. `df.groupby('key').sum()` hace **lo mismo**, pero en una línea, y evaluado de forma perezosa (*lazy*): `df.groupby('key')` todavía no calculó nada — recién cuando le pedís `.sum()`, `.mean()`, etc. hace el trabajo.

## Qué devuelve `.groupby()`

```python
df.groupby('key')
# <pandas.core.groupby.generic.DataFrameGroupBy object at ...>
```

No es un conjunto de DataFrames ni el resultado final — es un objeto `GroupBy`, una **vista** preparada para calcular, pero perezosa hasta que le aplicás una agregación.

## Agregaciones más comunes

```python
df.groupby('key').mean()      # ver [[medidas de posición]]
#      data
# key
# A     1.5
# B     2.5
# C     3.5

df.groupby('key')['data'].mean()   # agregación sobre UNA sola columna del grupo -> misma tabla, como Series
# key
# A    1.5
# B    2.5
# C    3.5
# Name: data, dtype: float64
```

## `.agg()`: varias agregaciones a la vez

```python
df.groupby('key').agg(['mean', 'std'])
#      data
#      mean       std
# key
# A     1.5  2.121320
# B     2.5  2.121320
# C     3.5  2.121320
```

También acepta un dict para aplicar una función **distinta por columna**: `df.groupby('key').agg({'data': 'sum', 'otra_columna': 'mean'})`.

## `.describe()` por grupo: el resumen de Estadística, agrupado

```python
df.groupby('key')['data'].describe()
```

Te da mínimo, cuartiles, media y desvío **para cada grupo por separado** — es la forma más rápida de comparar la [[medidas de posición|distribución]] de una variable entre categorías (exactamente lo que hacías al comparar Máquina 1 vs. Máquina 2 en [[02 - El estudio de la variabilidad|Estadística]], pero para cualquier cantidad de grupos a la vez).

## Filtrar grupos: `.filter()`

Para quedarte solo con los grupos que cumplen alguna condición **sobre el grupo entero** (no fila por fila):

```python
df.groupby('key').filter(lambda g: g['data'].std() > 1)
#   key  data
# 0   A     0
# 1   B     1
# 2   C     2
# 3   A     3
# 4   B     4
# 5   C     5
```

En este ejemplo los 3 grupos tienen `std() = 2.12 > 1`, así que `filter()` devuelve el DataFrame completo — la utilidad real aparece cuando **algunos** grupos no cumplen la condición y quedan afuera enteros (no fila por fila).

## Relacionado
- [[01 - Introduccion a Series y DataFrame]]
- [[medidas de posición]]
- [[medidas de dispersión]]
- [[07 - Tablas dinamicas (pivot_table)]]
