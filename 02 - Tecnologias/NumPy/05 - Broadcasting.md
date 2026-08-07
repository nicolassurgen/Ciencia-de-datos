---
titulo: NumPy - Broadcasting
materia: NumPy
tipo: apunte
tags:
  - numpy
  - tecnologias
  - python
  - tema/vectorizacion
fuente: "NumPy — Broadcasting (numpy.org/doc/stable/user/basics.broadcasting.html); Python Data Science Handbook (Jake VanderPlas) — Parte II"
---

# Broadcasting

Ya viste que las [[03 - Ufuncs y operaciones vectorizadas|ufuncs]] operan elemento a elemento. La pregunta natural es: ¿qué pasa si los dos arrays **no tienen la misma forma**? La respuesta es *broadcasting*, y es una de las ideas que más partido le vas a sacar a NumPy una vez que la internalizás.

> [!definition] Broadcasting
> Un conjunto de reglas que le permite a NumPy operar entre arrays de **formas distintas**, "estirando" mentalmente el más chico para que encaje con el más grande — sin copiar datos de verdad en memoria.

## El caso más simple: array + escalar

Esto ya lo veías como algo natural:

```python
np.array([1, 2, 3]) + 5   # array([6, 7, 8])
```

En el fondo, es broadcasting: el `5` (shape `()`, un escalar) se "estira" para comportarse como `[5, 5, 5]` y así poder sumarse elemento a elemento. La gracia es que esto se generaliza a formas mucho más complejas.

![[Broadcasting.png]]

## Las 3 reglas

> [!important] Reglas de broadcasting
> 1. Si dos arrays difieren en la **cantidad de dimensiones**, se rellena con 1 a la izquierda la forma del que tiene menos.
> 2. Si en alguna dimensión las formas no coinciden pero una de ellas vale **1**, se "estira" esa dimensión hasta igualar a la otra.
> 3. Si en alguna dimensión no coinciden **y ninguna vale 1**, es un error: las formas son incompatibles.

Aplicado al ejemplo del diagrama: `M` tiene shape `(2, 3)`, `a` tiene shape `(3,)`.
- Regla 1: `a` tiene menos dimensiones → se rellena a `(1, 3)`.
- Regla 2: la primera dimensión de `a` es 1 y la de `M` es 2 → se estira: `a` pasa a comportarse como `(2, 3)`.
- Las formas ya coinciden → la operación es válida, y el resultado tiene shape `(2, 3)`.

## Cuando falla: formas incompatibles

```python
M = np.ones((3, 2))
a = np.arange(3)
M + a
# ValueError: operands could not be broadcast together with shapes (3,2) (3,)
```

Acá `a` (shape `(3,)`) se rellena a `(1, 3)` por la regla 1, y por la regla 2 se estira a `(3, 3)` — pero `M` es `(3, 2)`. Ninguna de esas dimensiones coincide ni vale 1, así que salta la regla 3: error.

> [!tip] Si te da un `ValueError` de shapes, mirá las formas primero
> Antes de cualquier otra cosa, hacé `print(array1.shape, array2.shape)`. El 90 % de las veces el error de broadcasting se entiende de inmediato mirando las dos formas una al lado de la otra y aplicando las 3 reglas a mano.

## ¿Por qué importa tanto?

Es lo que te permite, por ejemplo, **centrar datos** (restarle la media a cada columna) sin loops:

```python
medidas = np.array([[39.1, 18.7], [39.5, 17.4], [40.3, 18.0], [36.7, 19.3]])   # 4 pingüinos, 2 variables

medias = medidas.mean(axis=0)          # array([38.9 , 18.35])  -> una media por columna
medidas_centradas = medidas - medias   # broadcasting: resta la media de cada columna a toda la columna
# array([[ 0.2 ,  0.35],
#        [ 0.6 , -0.95],
#        [ 1.4 , -0.35],
#        [-2.2 ,  0.95]])
```

Esta es exactamente la operación detrás de estandarizar variables antes de un análisis (ver [[medidas de posición]] y [[medidas de dispersión]] de Estadística) — y gracias al broadcasting se escribe en una sola línea, sin recorrer filas a mano.

## Relacionado
- [[03 - Ufuncs y operaciones vectorizadas]]
- [[04 - Agregaciones y estadistica descriptiva]]
- [[02 - Indexado, slicing y forma de los arrays]]
