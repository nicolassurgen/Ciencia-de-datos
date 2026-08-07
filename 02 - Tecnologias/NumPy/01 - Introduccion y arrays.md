---
titulo: NumPy - Introducción y arrays
materia: NumPy
tipo: apunte
tags:
  - numpy
  - tecnologias
  - python
  - tema/introduccion
fuente: "NumPy — Array creation (numpy.org/doc/stable/user/basics.creation.html); Python Data Science Handbook (Jake VanderPlas) — Parte II"
---

# Introducción y arrays

> [!definition] NumPy
> La librería base del cómputo numérico en Python. Define el `ndarray` (*n-dimensional array*), una estructura de datos que guarda **muchos valores del mismo tipo** de forma compacta y permite operar sobre todos ellos a la vez, sin escribir loops. Prácticamente todo el ecosistema de Data Science en Python —Pandas, Matplotlib, scikit-learn— está construido **encima** de NumPy.

## Por qué no alcanza con listas de Python

Una lista de Python es flexible (puede mezclar tipos, crecer dinámicamente), pero esa flexibilidad tiene un costo: cada elemento es en realidad un objeto Python completo disperso en memoria, con su propio tipo, su contador de referencias, etc. Ver [[tipos primitivos en Python]] y [[mutabilidad e inmutabilidad]] de Algoritmos para la base de esto.

> [!important] La diferencia clave
> Un array de NumPy guarda todos sus elementos **del mismo tipo**, en un bloque de memoria **contiguo**, como los arrays de C. Eso permite que las operaciones sobre el array completo se ejecuten en código compilado (rápido) en vez de un loop de Python interpretado (lento) — a veces **cientos de veces más rápido** para el mismo cálculo sobre datos grandes.

## Importar NumPy

```python
import numpy as np
```

Convención universal, igual que `import matplotlib.pyplot as plt` (ver [[01 - Introduccion y primer grafico]] de Matplotlib).

## Crear arrays

**A partir de una lista de Python:**

```python
np.array([1, 4, 2, 5, 3])
# array([1, 4, 2, 5, 3])
```

> [!warning] NumPy fuerza un tipo único
> Si mezclás tipos en la lista de origen, NumPy va a convertir todo a un tipo común (*upcasting*): `np.array([1, 2, 3.14])` te da un array de `float64`, no una mezcla de `int` y `float`. Recordá la regla de [[tipos primitivos en Python]]: `int` es exacto, `float` es aproximado — mezclarlos "sube" todo a `float`.

**Desde cero, sin partir de una lista** (mucho más común en la práctica):

```python
np.zeros(10, dtype=int)
# array([0, 0, 0, 0, 0, 0, 0, 0, 0, 0])

np.arange(0, 20, 2)                  # como range() de Python, pero devuelve un array
# array([ 0,  2,  4,  6,  8, 10, 12, 14, 16, 18])

np.linspace(0, 1, 5)                 # 5 valores equiespaciados entre 0 y 1
# array([0.  , 0.25, 0.5 , 0.75, 1.  ])

np.eye(3)                            # matriz identidad 3x3 (ver [[02 - Matrices]] de Matemática)
# array([[1., 0., 0.],
#        [0., 1., 0.],
#        [0., 0., 1.]])
```

## Atributos de un array

```python
x = np.random.randint(10, size=(3, 4))

x.ndim      # 2  -> cantidad de dimensiones
x.shape     # (3, 4)  -> tamaño de cada dimensión
x.size      # 12  -> cantidad total de elementos
x.dtype     # dtype('int64')  -> tipo de dato de los elementos
```

`shape` es probablemente el atributo que más vas a mirar: la fuente **número 1** de errores en NumPy es no tener clara la forma (*shape*) del array con el que estás trabajando.

## Dimensiones: de vector a matriz

| Dimensiones | Nombre | Ejemplo |
|---|---|---|
| 1D | vector | `np.array([1, 2, 3])` — shape `(3,)` |
| 2D | matriz | `np.array([[1, 2], [3, 4]])` — shape `(2, 2)` |
| 3D+ | tensor | un array de matrices — shape `(n, filas, columnas)` |

Esto conecta directo con [[01 - Vectores]] y [[02 - Matrices]] de Matemática: un array 1D de NumPy **es** la representación computacional de un vector; un array 2D **es** la representación computacional de una matriz.

## Recorrido de estas notas

1. **Introducción y arrays** *(esta nota)*
2. [[02 - Indexado, slicing y forma de los arrays]] — acceder, recortar y reorganizar arrays.
3. [[03 - Ufuncs y operaciones vectorizadas]] — por qué NumPy es rápido, y cómo dejar de escribir loops.
4. [[04 - Agregaciones y estadistica descriptiva]] — sum, mean, std, axis: el puente directo con Estadística.
5. [[05 - Broadcasting]] — operar entre arrays de formas distintas.
6. [[06 - Comparaciones, mascaras y filtrado booleano]] — filtrar datos según una condición.
7. [[07 - Indexado fancy y ordenamiento]] — traer elementos puntuales, ordenar y `argsort`.

## Relacionado
- [[tipos primitivos en Python]]
- [[01 - Vectores]]
- [[02 - Indexado, slicing y forma de los arrays]]
- [[03 - Ufuncs y operaciones vectorizadas]]
