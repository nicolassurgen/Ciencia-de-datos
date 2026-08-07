---
titulo: "NumPy - Indexado, slicing y forma de los arrays"
materia: NumPy
tipo: apunte
tags:
  - numpy
  - tecnologias
  - python
  - tema/indexado
fuente: "NumPy — Indexing on ndarrays (numpy.org/doc/stable/user/basics.indexing.html); Python Data Science Handbook (Jake VanderPlas) — Parte II"
---

# Indexado, slicing y forma de los arrays

## Acceder a un elemento

Igual que en una lista de Python (ver [[indexado y slicing]] de Algoritmos), con la diferencia de que en un array multidimensional se indexan **todas las dimensiones a la vez**, separadas por coma:

```python
x2 = np.array([[3, 5, 2, 4], [7, 6, 8, 8], [1, 6, 7, 7]])

x2[0, 0]     # 3   -> fila 0, columna 0
x2[2, -1]    # 7   -> última fila, última columna
x2[0, 0] = 12  # también se puede modificar así
```

> [!warning] `x2[0][0]` funciona, pero `x2[0, 0]` es la forma de NumPy
> Las dos dan el mismo resultado, pero `x2[0][0]` primero saca la fila 0 completa (creando un array intermedio) y después indexa esa fila. `x2[0, 0]` accede directo. Con arrays grandes, la diferencia de performance importa.

## Slicing: subarrays

Misma sintaxis `inicio:fin:paso` que en listas (ver [[indexado y slicing]]), extendida a cada dimensión:

```python
x2[:2, :3]     # las primeras 2 filas, las primeras 3 columnas
x2[:, 0]       # la columna 0 completa
x2[0, :]       # la fila 0 completa (equivalente a x2[0])
x2[::-1, ::-1] # invierte filas y columnas
```

> [!important] Las vistas de NumPy NO son copias
> Esta es **la** trampa más importante de este tema, y es la contracara de la [[mutabilidad e inmutabilidad|trampa de la copia compartida]] de listas en Algoritmos, pero más sutil: en una lista de Python, `lista[:]` sí crea una copia. En un array de NumPy, **no**.
>
> ```python
> sub = x2[:2, :2]   # esto es una VISTA, no una copia
> sub[0, 0] = 99
> print(x2[0, 0])    # 99  -> ¡x2 también cambió!
> ```
>
> Es una decisión de diseño a propósito: con arrays grandes (millones de elementos), copiar en cada slice sería carísimo. Si necesitás una copia real, pedila explícitamente:
> ```python
> sub_copia = x2[:2, :2].copy()
> ```

## Reshape: cambiar la forma sin cambiar los datos

```python
grid = np.arange(1, 10).reshape((3, 3))
# array([[1, 2, 3],
#        [4, 5, 6],
#        [7, 8, 9]])
```

El array resultante debe tener la **misma cantidad total de elementos** que el original (`reshape` no inventa ni descarta datos, solo reorganiza cómo se "leen"). Un `-1` en alguna dimensión le dice a NumPy "calculá vos este tamaño":

```python
np.arange(12).reshape(3, -1)   # NumPy calcula que la otra dimensión es 4
# array([[ 0,  1,  2,  3],
#        [ 4,  5,  6,  7],
#        [ 8,  9, 10, 11]])
```

## Concatenar y dividir arrays

```python
x = np.array([1, 2, 3])
y = np.array([4, 5, 6])

np.concatenate([x, y])          # array([1, 2, 3, 4, 5, 6])

grid = np.array([[1, 2, 3], [4, 5, 6]])
np.concatenate([grid, grid])            # apila por filas (axis=0, default)
np.concatenate([grid, grid], axis=1)    # apila por columnas
```

Para 2D específicamente, `np.vstack` (apilar verticalmente) y `np.hstack` (horizontalmente) suelen ser más legibles que acordarse del `axis`:

```python
np.vstack([x, grid])    # agrega x como una fila nueva arriba
# array([[1, 2, 3],
#        [1, 2, 3],
#        [4, 5, 6]])
```

`np.split()` (y las variantes `np.hsplit`, `np.vsplit`) hacen la operación inversa: cortar un array en varios.

## Relacionado
- [[01 - Introduccion y arrays]]
- [[indexado y slicing]]
- [[mutabilidad e inmutabilidad]]
- [[05 - Broadcasting]]
