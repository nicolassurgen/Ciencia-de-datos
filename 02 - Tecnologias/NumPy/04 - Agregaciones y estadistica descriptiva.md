---
titulo: NumPy - Agregaciones y estadística descriptiva
materia: NumPy
tipo: apunte
tags:
  - numpy
  - tecnologias
  - python
  - tema/estadistica-descriptiva
fuente: "Python Data Science Handbook (Jake VanderPlas) — Parte II"
---

# Agregaciones y estadística descriptiva

Esta nota es, en el fondo, el capítulo de [[02 - El estudio de la variabilidad|medidas de resumen de Estadística]] traducido a código. Cada medida que ya conocés tiene su función de NumPy.

## Las agregaciones básicas

```python
x = np.random.random(100)

np.sum(x)       # o x.sum()      -> suma total
np.min(x)       # o x.min()      -> mínimo
np.max(x)       # o x.max()      -> máximo
np.mean(x)      # o x.mean()     -> media (ver [[medidas de posición]])
np.median(x)                     # mediana
np.std(x)       # o x.std()      -> desvío estándar (ver [[medidas de dispersión]])
np.var(x)                        # varianza
np.percentile(x, 25)              # percentil 25 (= q1, ver [[medidas de posición]])
```

> [!warning] `np.std()` divide por $n$, no por $n-1$
> Esta es la trampa que ya viste en [[coeficiente de variación]] de Estadística: por defecto, `np.std()` y `np.var()` calculan la varianza **poblacional** (dividen por $n$). Para la varianza **muestral** (dividir por $n-1$, ver [[grados de libertad]]) hay que pasar `ddof=1` explícitamente:
> ```python
> np.std(x, ddof=1)   # ahora sí divide por n-1
> ```
> Si tu profesora te pasa un resultado calculado en R (donde `sd()` siempre usa $n-1$) y lo querés reproducir en Python, este parámetro es el que marca la diferencia.

> [!tip] `np.sum(x)` vs `sum(x)` (built-in de Python)
> Ambos existen y dan el mismo resultado, pero `np.sum()` es **mucho más rápido** sobre arrays de NumPy porque está vectorizado (ver [[03 - Ufuncs y operaciones vectorizadas]]). Usá siempre la versión de NumPy cuando ya estés trabajando con arrays.

## El parámetro más importante: `axis`

Con un array multidimensional, `axis` decide **sobre qué dimensión se colapsa** la agregación — y es la fuente de confusión número uno para quien recién arranca con NumPy.

```python
M = np.array([[1, 2, 3],
              [4, 5, 6]])   # shape (2, 3)

M.sum()             # 21  -> suma TODO, sin importar la forma
M.sum(axis=0)       # array([5, 7, 9])   -> suma "hacia abajo": colapsa las FILAS, queda 1 valor por columna
M.sum(axis=1)       # array([6, 15])     -> suma "hacia el costado": colapsa las COLUMNAS, queda 1 valor por fila
```

> [!important] Cómo pensarlo sin confundirse
> `axis=N` significa **"esta es la dimensión que desaparece"**, no "esta es la dimensión sobre la que recorro". `axis=0` colapsa filas (el resultado tiene tantos elementos como columnas tenía la matriz); `axis=1` colapsa columnas (el resultado tiene tantos elementos como filas). Si tenés un `DataFrame` de Pandas con observaciones en las filas y variables en las columnas (la [[01 - Como dar sentido a los datos|matriz de datos]] de Estadística), `axis=0` te da **un resultado por variable** — que es, en general, lo que querés.

## Todo junto: el resumen de 5 números

```python
print(f"Mínimo: {x.min()}")
print(f"Q1: {np.percentile(x, 25)}")
print(f"Mediana: {np.median(x)}")
print(f"Q3: {np.percentile(x, 75)}")
print(f"Máximo: {x.max()}")
```

Es exactamente el [[boxplot|five-number summary]] de Estadística — en Pandas esto se obtiene directo con `serie.describe()` (ver la nota de Pandas sobre [[01 - Introduccion a Series y DataFrame]]).

## Relacionado
- [[03 - Ufuncs y operaciones vectorizadas]]
- [[medidas de posición]]
- [[medidas de dispersión]]
- [[grados de libertad]]
