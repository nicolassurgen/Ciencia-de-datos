---
titulo: Lista de diccionarios y JSON
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

# Lista de diccionarios y JSON

> [!important] La estructura estrella de un dataset
> Una **lista** (las filas) de **diccionarios** (los campos de cada fila) es la representación estándar de un conjunto de datos tabular en Python puro, sin librerías.

```python
pinguinos = [
    {"especie": "Adelie", "isla": "Torgersen", "pico_mm": 39.1, "masa_g": 3750},
    {"especie": "Gentoo", "isla": "Biscoe",    "pico_mm": 46.1, "masa_g": 4500},
]
print(pinguinos[1]["especie"])   # Gentoo -> registro 1, campo especie
```

Cada corchete **baja un nivel** en la estructura: primero se elige la fila (posición, como en una [[listas, tuplas, diccionarios y conjuntos|lista]]), después el campo (nombre, como en un [[listas, tuplas, diccionarios y conjuntos|diccionario]]).

## Por qué esta forma y no listas de listas

Con `tabla[2][3]` (lista de listas) hay que **recordar** qué representa la columna 3. Con `pinguinos[2]["masa_g"]` el acceso **se autoexplica**. Ninguna posición numérica arbitraria que memorizar.

## De un CSV a lista de diccionarios

`csv.DictReader` construye exactamente esta estructura a partir de un archivo real, usando la primera fila como claves:

```python
import csv
filas = list(csv.DictReader(lineas))   # usa la 1ª fila como claves
print(filas[0])   # un diccionario por registro
```

## JSON: el mismo formato viajando por la web

Es la forma en que la información viaja habitualmente entre sistemas en la web (**JSON** — *JavaScript Object Notation*): una lista de objetos con pares clave-valor, estructuralmente idéntica a una lista de diccionarios de Python.

## La antesala del DataFrame

Esta estructura es el paso previo directo al **[[01 - Introduccion a Series y DataFrame|DataFrame de Pandas]]**: `pd.DataFrame(pinguinos)` convierte esta misma lista de diccionarios en un DataFrame directamente, sin transformar nada. Lo que en Python puro se resuelve "a mano" con listas, diccionarios y bucles (por ejemplo, un `group by` acumulando en diccionarios), en Pandas es una línea (`df.groupby("especie")["masa_g"].mean()`, ver [[06 - Agregacion y groupby]]). Escribirlo a mano una vez muestra cuánto trabajo esconde esa línea.

## Relacionado
- [[01 - Introduccion a la programacion]]
- [[listas, tuplas, diccionarios y conjuntos]]
- [[datos faltantes y None]]
- [[01 - Introduccion a Series y DataFrame]]
- [[06 - Agregacion y groupby]]
