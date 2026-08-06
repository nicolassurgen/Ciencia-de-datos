---
titulo: Pandas - Datos faltantes
materia: Pandas
tipo: apunte
tags:
  - pandas
  - tecnologias
  - python
  - tema/datos-faltantes
fuente: "Python Data Science Handbook (Jake VanderPlas) — Parte III"
---

# Datos faltantes

Ya viste esto "a mano" en Algoritmos con [[datos faltantes y None|None]] y en R/Python con [[tratamiento primario]] de Estadística. Pandas trae herramientas dedicadas para exactamente este problema, porque en datasets reales los faltantes son la norma, no la excepción.

## `None` vs `NaN`: dos formas de "no hay dato", y por qué importa la diferencia

```python
pd.Series([1, np.nan, 3, None])
# 0    1.0
# 1    NaN
# 2    3.0
# 3    NaN
# dtype: float64
```

> [!important] Pandas convierte `None` a `NaN` automáticamente en columnas numéricas
> `None` es el objeto de [[datos faltantes y None|Python puro]] que ya conocés; `NaN` (*Not a Number*) es un valor especial de punto flotante (viene de NumPy/IEEE 754, ver [[tipos primitivos en Python]]). Cuando metés un `None` en una columna numérica, Pandas lo convierte a `NaN` — y de paso, **sube el tipo de toda la columna a `float64`**, incluso si originalmente era de enteros. Es la misma lógica de *upcasting* que ya viste en [[01 - Introduccion y arrays]] de NumPy.
>
> Consecuencia práctica: una columna de enteros con un solo faltante deja de "verse" como enteros (`4.0` en vez de `4`). No es un bug, es Pandas evitando inventar un tipo "entero nulificable" por vos.

## Detectar faltantes

```python
df.isnull()          # DataFrame de True/False, mismo shape que df
df.isnull().sum()    # cantidad de faltantes POR COLUMNA -> lo primero que hay que mirar en cualquier dataset nuevo
df.notnull()          # el opuesto
```

`df.isnull().sum()` es, en la práctica, el primer comando que corrés después de un `pd.read_csv()`. Te da, columna por columna, exactamente lo que en Algoritmos calculabas con `sum(1 for p in pinguinos if p["masa_g"] is None)` — pero para todas las columnas a la vez, sin loop.

## Eliminar filas o columnas con faltantes

```python
df.dropna()                    # elimina toda FILA que tenga al menos un NaN
df.dropna(axis='columns')       # elimina toda COLUMNA que tenga al menos un NaN
df.dropna(thresh=3)              # solo elimina filas con MENOS de 3 valores no nulos
```

> [!warning] `dropna()` por defecto es agresivo
> Si una sola columna de 20 tiene un faltante en una fila, esa fila entera desaparece. En un dataset real esto puede borrarte la mayoría de las filas sin que te des cuenta. Mirá siempre `df.isnull().sum()` **antes** de decidir si `dropna()` es realmente lo que querés, o si conviene `fillna()` en su lugar.

## Rellenar faltantes en vez de eliminarlos

```python
df.fillna(0)                        # rellena con un valor fijo
df['col'].fillna(df['col'].mean())  # rellena con la media de la columna (ver [[medidas de posición]])
df.fillna(method='ffill')            # propaga el último valor válido hacia adelante (típico en series de tiempo)
```

> [!important] Qué hacer con los faltantes es una decisión del analista, no de la herramienta
> Mismo principio que ya viste en Algoritmos: **nunca** reemplaces un faltante por 0 "porque sí" si en realidad significa "no medido" — el promedio te va a quedar sesgado exactamente como en el ejemplo de `masa_g` de los pingüinos. La opción correcta (eliminar, imputar con la media/mediana, propagar el valor anterior) depende de **por qué** falta el dato, no de cuál es más fácil de escribir.

## Relacionado
- [[datos faltantes y None]]
- [[tratamiento primario]]
- [[01 - Introduccion a Series y DataFrame]]
- [[medidas de posición]]
