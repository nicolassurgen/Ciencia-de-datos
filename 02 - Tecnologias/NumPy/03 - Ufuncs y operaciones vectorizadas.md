---
titulo: NumPy - Ufuncs y operaciones vectorizadas
materia: NumPy
tipo: apunte
tags:
  - numpy
  - tecnologias
  - python
  - tema/vectorizacion
fuente: "Python Data Science Handbook (Jake VanderPlas) — Parte II"
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
x = np.arange(4)
x + 5    # array([5, 6, 7, 8])
x - 5
x * 2
x / 2
x ** 2
x % 2
```

Cada operador de Python (`+`, `-`, `*`, `/`) es en realidad un atajo para una ufunc de NumPy (`np.add`, `np.subtract`, `np.multiply`, `np.divide`). Escribir `x + 5` o `np.add(x, 5)` da exactamente el mismo resultado.

## Ufuncs comunes

```python
np.abs(x)          # valor absoluto
np.sqrt(x)         # raíz cuadrada
np.exp(x)          # e^x
np.log(x)          # logaritmo natural
np.sin(x), np.cos(x), np.tan(x)   # trigonométricas
```

## Especificar dónde va el resultado

Para ahorrar memoria con arrays grandes, se puede escribir el resultado directo en un array existente en vez de crear uno nuevo:

```python
y = np.empty(5)
np.multiply(x, 10, out=y)
```

## Relacionado
- [[01 - Introduccion y arrays]]
- [[04 - Agregaciones y estadistica descriptiva]]
- [[05 - Broadcasting]]
