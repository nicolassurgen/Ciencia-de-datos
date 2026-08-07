---
titulo: NumPy - Ufuncs y operaciones vectorizadas
materia: NumPy
tipo: apunte
tags:
  - numpy
  - tecnologias
  - python
  - tema/vectorizacion
fuente: "NumPy — Universal functions (numpy.org/doc/stable/reference/ufuncs.html); Python Data Science Handbook (Jake VanderPlas) — Parte II"
---

# Ufuncs y operaciones vectorizadas

## El problema: los loops de Python son lentos

Si tenés un array y querés aplicarle una operación a cada elemento, la forma "obvia" (heredada de listas comunes) sería un `for`:

```python
def inversos(valores):
    salida = np.empty(len(valores))
    for i in range(len(valores)):
        salida[i] = 1.0 / valores[i]
    return salida
```

Esto funciona, pero es **lento** sobre arrays grandes: cada vuelta del loop paga el costo de que Python es un lenguaje interpretado (chequea tipos, resuelve el método a llamar, etc.) en cada iteración.

## La solución: ufuncs (*universal functions*)

> [!definition] Ufunc
> Una función de NumPy que aplica una operación **elemento a elemento** sobre un array completo, ejecutando el loop en código compilado (no en Python). Es la forma **vectorizada** de escribir lo mismo:

```python
1.0 / valores    # hace exactamente lo mismo que la función de arriba, pero mucho más rápido
```

> [!important] Regla de oro en NumPy (y en Pandas)
> Si te encontrás escribiendo un `for` para recorrer un array elemento por elemento, **probablemente hay una ufunc que hace lo mismo, vectorizada**. Buscarla vale la pena: la diferencia de velocidad crece con el tamaño de los datos, y en Data Science los datos son grandes.

## Los operadores aritméticos comunes son ufuncs

Todo esto ya es vectorizado — no hace falta ningún import ni sintaxis especial:

```python
x = np.arange(4)   # array([0, 1, 2, 3])

x + 5    # array([5, 6, 7, 8])
x - 5    # array([-5, -4, -3, -2])
x * 2    # array([0, 2, 4, 6])
x / 2    # array([0. , 0.5, 1. , 1.5])
x ** 2   # array([0, 1, 4, 9])
x % 2    # array([0, 1, 0, 1])
```

Cada operador de Python (`+`, `-`, `*`, `/`) es en realidad un atajo para una ufunc de NumPy (`np.add`, `np.subtract`, `np.multiply`, `np.divide`). Escribir `x + 5` o `np.add(x, 5)` da exactamente el mismo resultado.

## Ufuncs comunes

```python
x = np.array([1, 4, 9, 16])

np.abs(np.array([-2, -1, 0, 1]))   # array([2, 1, 0, 1])
np.sqrt(x)                          # array([1., 2., 3., 4.])
np.exp(np.array([0, 1, 2]))         # array([1.        , 2.71828183, 7.3890561 ])
np.log(x)                           # array([0.        , 1.38629436, 2.19722458, 2.77258872])
```

## Especificar dónde va el resultado

Para ahorrar memoria con arrays grandes, se puede escribir el resultado directo en un array existente en vez de crear uno nuevo:

```python
y = np.empty(4)
np.multiply(x, 10, out=y)
print(y)   # [ 10.  40.  90. 160.]  -> escribió directo en y, sin crear un array nuevo
```

## Relacionado
- [[01 - Introduccion y arrays]]
- [[04 - Agregaciones y estadistica descriptiva]]
- [[05 - Broadcasting]]
