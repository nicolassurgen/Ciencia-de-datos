---
titulo: Indexado y slicing
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

# Indexado y slicing

> [!definition] Indexado
> Acceder a un elemento de una secuencia (`str`, lista, tupla) por su **posición**. En Python, **las posiciones empiezan en 0**, y los índices negativos cuentan desde el final.

```
lista:    [39.1,  39.5,  40.3,  36.7,  39.3,  38.9,  39.2]
índice:      0      1      2      3      4      5      6
negativo:   -7     -6     -5     -4     -3     -2     -1
```

```python
largos_pico = [39.1, 39.5, 40.3, 36.7, 39.3, 38.9, 39.2]
print(largos_pico[0])    # 39.1  -> primero
print(largos_pico[-1])   # 39.2  -> último (siempre)
print(largos_pico[7])    # IndexError: list index out of range
```

> [!definition] Slicing (rebanadas)
> Extraer un **subconjunto contiguo** de una secuencia con la sintaxis `secuencia[desde:hasta:paso]`.

```python
print(largos_pico[0:3])   # [39.1, 39.5, 40.3]  -> posiciones 0,1,2
print(largos_pico[:3])    # lo mismo (si arranca en 0 se omite)
print(largos_pico[2:])    # del tercero en adelante
print(largos_pico[-2:])   # los dos últimos
print(largos_pico[::2])   # uno de cada dos (el tercer número es el paso)
print(largos_pico[::-1])  # al revés (paso negativo)
```

> [!important] La convención más importante de Python: el final del rango NO se incluye
> `secuencia[0:4]` toma las posiciones 0, 1, 2, 3 — la posición 4 queda **afuera**. Vale para texto, listas, tuplas y, más adelante, para filas y columnas de un DataFrame de Pandas. Conviene que se vuelva automático, porque se repite en todo el lenguaje.

## También aplica a texto

```python
isla = "Torgersen"
print(isla[0])         # T  -> primer carácter
print(isla[-1])        # n  -> último carácter
print(isla[0:4])       # Torg  -> de la 0 a la 3 (la 4 NO se incluye)
```

## Puente con Tecnologías

Exactamente la misma sintaxis (`[desde:hasta:paso]`, final excluido) se usa en un array de NumPy — con la diferencia de que ahí se indexan **varias dimensiones a la vez**, separadas por coma: `array[fila, columna]` (ver [[02 - Indexado, slicing y forma de los arrays]]). En Pandas, `.iloc[]` es la versión "por posición" de esto mismo; `.loc[]` la versión "por etiqueta" (ver [[02 - Indexado y seleccion (loc, iloc)]]).

## Relacionado
- [[01 - Introduccion a la programacion]]
- [[listas, tuplas, diccionarios y conjuntos]]
- [[02 - Indexado, slicing y forma de los arrays]]
- [[02 - Indexado y seleccion (loc, iloc)]]
