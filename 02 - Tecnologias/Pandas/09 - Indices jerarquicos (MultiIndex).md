---
titulo: "Pandas - Índices jerárquicos (MultiIndex)"
materia: Pandas
tipo: apunte
tags:
  - pandas
  - tecnologias
  - python
  - tema/indexado
fuente: "pandas — MultiIndex / advanced indexing (pandas.pydata.org/docs/user_guide/advanced.html); Python Data Science Handbook (Jake VanderPlas) — Parte III"
---

# Índices jerárquicos (MultiIndex)

## El problema: más de dos variables para identificar cada fila

Un `DataFrame` común tiene un `Index` de un solo nivel (ver [[01 - Introduccion a Series y DataFrame]]). Pero a veces cada fila se identifica naturalmente por **más de una** variable — por ejemplo, población por (estado, año):

```python
indice = pd.MultiIndex.from_tuples([
    ('California', 2010), ('California', 2020),
    ('Texas', 2010), ('Texas', 2020),
])
poblacion = pd.Series([37253956, 39538223, 25145561, 29145505], index=indice)
```

```
California  2010    37253956
            2020    39538223
Texas       2010    25145561
            2020    29145505
```

> [!definition] MultiIndex
> Un índice con **varios niveles**. Permite representar datos de 3 o más dimensiones (estado × año × valor) dentro de la estructura 2D de un DataFrame, sin tener que aplanar todo a una sola columna combinada tipo `"California-2010"`.

## De dónde suele salir un MultiIndex (casi siempre, sin buscarlo)

No hace falta construirlo a mano casi nunca — aparece solo cuando agrupás por más de una columna:

```python
df.groupby(['sexo', 'clase'])['sobrevivio'].mean()   # el resultado YA tiene un MultiIndex (sexo, clase)
```

Es exactamente el resultado que viste en [[07 - Tablas dinamicas (pivot_table)|la nota anterior]], antes de "aplanarlo" con `pivot_table`.

## Indexar un MultiIndex

```python
poblacion['California']
# 2010    37253956
# 2020    39538223
# dtype: int64

poblacion['California', 2010]    # 37253956  -> una celda puntual

poblacion[:, 2010]                # todos los estados, solo el año 2010
# California    37253956
# Texas         25145561
# dtype: int64
```

## `unstack()` / `stack()`: pasar de "apilado" a "en grilla" y viceversa

```python
poblacion.unstack()
#             2010      2020
# California  37253956  39538223
# Texas       25145561  29145505
```

`unstack()` toma el **último nivel del índice** y lo convierte en columnas — es el mismo movimiento que hace `pivot_table` por dentro. `stack()` hace el camino inverso: vuelve a "apilar" columnas dentro del índice.

> [!tip] Regla mental
> Si tenés un MultiIndex y te resulta incómodo de leer, probá `.unstack()`: casi siempre convierte la tabla "apilada" en algo que se parece más a la matriz de datos de toda la vida (filas = una variable, columnas = otra).

## Nombrar los niveles

```python
poblacion.index.names = ['estado', 'año']
```

Le pone nombre a cada nivel, para no tener que acordarte "el nivel 0 es el estado" — se vuelve autoexplicativo al imprimir la Series/DataFrame, igual que nombrar bien una variable en [[tipos primitivos en Python|Python]] en vez de usar `x1`, `x2`.

## Relacionado
- [[01 - Introduccion a Series y DataFrame]]
- [[06 - Agregacion y groupby]]
- [[07 - Tablas dinamicas (pivot_table)]]
