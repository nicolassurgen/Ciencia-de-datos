---
titulo: Tipos primitivos en Python
materia: Algoritmos
tipo: concepto
tags:
  - algoritmos
  - maestria
  - concepto
  - python
  - tema/introduccion
fecha: 2026-08-03
---

# Tipos primitivos en Python

> [!definition] Tipo de dato
> Define **qué valores** puede tomar algo y **qué operaciones** tienen sentido sobre él. Tiene sentido sumar dos números; no tiene sentido dividir dos palabras.

## Los cinco primitivos

| Tipo | Python | Ejemplo | Para qué sirve | Variable estadística |
|---|---|---|---|---|
| Entero | `int` | `42`, `-7`, `0` | Contar (filas, edad, año) | Cuantitativa discreta |
| Real | `float` | `3.14`, `39.1` | Medir (peso, temperatura, precio) | Cuantitativa continua |
| Texto | `str` | `"Adelie"` | Nombres, categorías, etiquetas | Cualitativa |
| Lógico | `bool` | `True`, `False` | Respuestas sí/no | Binaria |
| Vacío | `NoneType` | `None` | "Acá no hay dato" | Dato faltante |

La función `type()` dice de qué tipo es un valor: `type(42)` → `int`, `type("Adelie")` → `str`, etc.

> [!tip] En Python, `int` no tiene límite de tamaño
> En muchos lenguajes (Java, C) un entero ocupa un tamaño fijo de memoria (por ejemplo 32 bits) y puede **desbordarse** (*overflow*) si el resultado de una cuenta supera ese límite, dando un resultado incorrecto sin avisar. El `int` de Python tiene **precisión arbitraria**: crece automáticamente para representar el número exacto, sin importar cuántos dígitos tenga.
> ```python
> print(17239871 ** 6)
> # 26254519291092456596965462913230729701102721  <- exacto, 44 dígitos, sin overflow
> ```
> Es una comodidad que se da por sentada trabajando solo en Python, pero no es universal — vale la pena saber que existe el problema en otros lenguajes. *Fuente: [[Algorithms-4th-Edition-By-Robert Sedgewick and Kevin Wayne]], cap. 1; [[Python-for-Data-Analysis]], cap. 2.*

## `int` vs `float`: por qué importa

Un `int` es **exacto**; un `float` es una **aproximación** (la máquina guarda los decimales en una cantidad finita de bits — estándar **IEEE 754**), y de ahí salen sorpresas:

```python
print(0.1 + 0.2)                     # 0.30000000000000004
print(0.1 + 0.2 == 0.3)              # False (!)
print(round(0.1 + 0.2, 10) == 0.3)   # True -> la forma correcta de comparar
```

> [!important] Regla práctica con reales
> **Nunca compares dos `float` con `==`.** Compará si su diferencia es menor a una tolerancia chica. Números como 0.1 no tienen representación exacta en base 2.

## Conversión de tipos (*casting*)

```python
numero = float("39.1")     # texto -> real
print(int(39.9))           # 39  <- int() TRUNCA hacia cero, NO redondea
print(round(39.9))         # 40  <- round() sí redondea
print(str(39.1) + " mm")   # número -> texto para concatenar
```

> [!warning] `int()` trunca, no redondea
> Confundir `int()` con `round()` genera **sesgos silenciosos** en un análisis. Además, `round()` en Python usa "redondeo bancario" (al par más cercano): `round(2.5)` da `2`, no `3`.

## `None`: el dato que no está

`None` representa **ausencia de información**; no es `0` ni texto vacío (`None == 0` y `None == ""` son ambos `False`). Ver [[datos faltantes y None]] para el tratamiento completo.

## Puente con Estadística

Los tipos primitivos se corresponden directo con los tipos de variable: `int`/`float` → cuantitativas (discreta/continua), `str` → cualitativas, `bool` → binarias, `None` → datos faltantes. Ver [[escalas de medición]] (Estadística).

## Puente con Tecnologías

Un array de NumPy lleva esta idea un paso más allá: en vez de que cada elemento "sepa" su propio tipo (como acá), **todo el array comparte un solo `dtype`** (ver [[01 - Introduccion y arrays]]) — por eso es tan compacto y rápido. La distinción `int` exacto / `float` aproximado se hereda tal cual: `np.array([1, 2, 3.14])` sube todo a `float64` por el mismo motivo que acá. En Pandas, `df.dtypes` muestra el tipo de cada columna con esta misma lógica.

## Relacionado
- [[01 - Introduccion a la programacion]]
- [[mutabilidad e inmutabilidad]]
- [[datos faltantes y None]]
- [[01 - Introduccion y arrays]]
- [[escalas de medición]]
