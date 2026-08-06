---
titulo: NumPy - Indexado fancy y ordenamiento
materia: NumPy
tipo: apunte
tags:
  - numpy
  - tecnologias
  - python
  - tema/indexado
fuente: "Python Data Science Handbook (Jake VanderPlas) — Parte II"
---

# Indexado fancy y ordenamiento

## Fancy indexing: indexar con una lista de posiciones

Ya conocés indexar con un número (`x[3]`) o un slice (`x[2:5]`, ver [[02 - Indexado, slicing y forma de los arrays]]). El *fancy indexing* es un tercer mecanismo: pasar una **lista o array de índices** para traer varios elementos puntuales, en cualquier orden, de una sola vez.

```python
x = np.array([51, 92, 14, 71, 60, 20, 82, 86, 74, 74])

indices = [3, 7, 2]
x[indices]     # array([71, 86, 14])  -> en ESE orden, no el original
```

A diferencia del slicing, **fancy indexing siempre devuelve una copia**, no una vista (repasá la trampa de las vistas en [[02 - Indexado, slicing y forma de los arrays]] — acá es al revés, y conviene tenerlo presente).

También funciona en 2D, y también sirve para **modificar** varios elementos puntuales a la vez:

```python
x[[0, 1, 2]] = 0   # pone en 0 las tres primeras posiciones, en un solo paso
```

## Combinar fancy indexing con máscaras booleanas

Fancy indexing y las [[06 - Comparaciones, mascaras y filtrado booleano|máscaras booleanas]] se combinan naturalmente:

```python
tabla = np.random.randint(100, size=(4, 3))
fila_mask = tabla[:, 0] > 50    # condición sobre la primera columna
tabla[fila_mask]                 # solo las filas que cumplen
```

Este es, básicamente, el mecanismo interno detrás de `df[df['columna'] > 50]` en Pandas — cuando llegues a la [[01 - Introduccion a Series y DataFrame|nota de Pandas]] vas a reconocer el mismo patrón.

## Ordenar arrays

```python
x = np.array([2, 1, 4, 3, 5])
np.sort(x)          # array([1, 2, 3, 4, 5])  -> devuelve una copia ordenada
x.sort()             # ordena x IN-PLACE (modifica el original, no devuelve nada)
```

Mismo par de comportamientos que ya viste con `sorted()` vs `.sort()` de listas en [[listas, tuplas, diccionarios y conjuntos|Python puro]] (Algoritmos): una versión no destructiva, una versión que modifica en el lugar.

### `argsort`: los índices que ordenarían el array

```python
x = np.array([2, 1, 4, 3, 5])
indices_orden = np.argsort(x)    # array([1, 0, 3, 2, 4])
x[indices_orden]                  # array([1, 2, 3, 4, 5])  -> mismo resultado que np.sort(x)
```

> [!important] ¿Para qué sirve `argsort` si `sort` ya ordena?
> `argsort` te da las **posiciones**, no los valores — lo que te permite ordenar **otro** array en función del orden de este. Ejemplo típico: tenés nombres y puntajes en dos arrays separados, y querés los nombres ordenados por puntaje:
> ```python
> nombres = np.array(['Ana', 'Bruno', 'Caro'])
> puntajes = np.array([85, 92, 78])
> orden = np.argsort(puntajes)
> nombres[orden]    # array(['Caro', 'Ana', 'Bruno'])  -> de menor a mayor puntaje
> ```

### Ordenar por filas o columnas

```python
tabla.sort(axis=0)   # ordena cada COLUMNA de forma independiente
tabla.sort(axis=1)   # ordena cada FILA de forma independiente
```

Mismo `axis` que ya viste en [[04 - Agregaciones y estadistica descriptiva]]: `axis=0` opera "hacia abajo" (columna por columna), `axis=1` opera "hacia el costado" (fila por fila).

## Relacionado
- [[02 - Indexado, slicing y forma de los arrays]]
- [[06 - Comparaciones, mascaras y filtrado booleano]]
- [[listas, tuplas, diccionarios y conjuntos]]
