---
titulo: "Listas, tuplas, diccionarios y conjuntos"
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

# Listas, tuplas, diccionarios y conjuntos

Las cuatro **estructuras de datos** básicas de Python: formas organizadas de guardar varios valores, cada una con sus propias reglas de acceso y modificación.

## Resumen comparativo

| Estructura | Sintaxis | ¿Ordenada? | ¿Modificable? | ¿Repetidos? | Uso típico |
|---|---|:---:|:---:|:---:|---|
| **Lista** | `[1, 2, 3]` | Sí | Sí | Sí | Una columna, una secuencia |
| **Tupla** | `(1, 2, 3)` | Sí | **No** | Sí | Un registro fijo, una coordenada |
| **Diccionario** | `{"a": 1}` | Sí (por inserción) | Sí | Claves no | Un registro con campos nombrados |
| **Conjunto** | `{1, 2, 3}` | **No** | Sí | **No** | Valores únicos, pertenencia rápida |

## Lista — secuencial y mutable

Pensala como una **columna de una tabla**. Se accede por [[indexado y slicing|posición]] y es [[mutabilidad e inmutabilidad|mutable]]: `m[0] = 38.0`, `m.append(x)`, `m.remove(x)`, `m.pop()`.

## Tupla — secuencial e inmutable

Como una lista, pero no se puede modificar tras crearla. Sirve para un **registro con campos fijos** (p. ej. una coordenada) y, por ser inmutable, puede usarse como **clave de un diccionario** — cosa que una lista no puede. Permite **desempaquetado**: `especie, isla, pico, masa = pinguino`.

## Diccionario — pares clave → valor

Resuelve el problema de acceder "por posición" (`tabla[2][3]`, hay que recordar qué es la columna 3): en un diccionario se accede **por nombre** (`pinguino["masa_g"]`). Las claves deben ser **únicas e inmutables** (ver [[hashing y hashabilidad]]); los valores pueden ser cualquier cosa. `.get()` es la forma segura de acceder sin arriesgarse a un `KeyError`.

## Conjunto — sin orden y sin repetidos

El conjunto matemático de siempre: `set(columna)` da los valores únicos de una lista. Preguntar "¿está este elemento?" en un conjunto es **inmediato** (ver [[complejidad O(1) vs O(n)]]), a diferencia de recorrer una lista entera. Soporta operaciones de conjunto (`|` unión, `&` intersección, `-` diferencia, `^` diferencia simétrica), la base conceptual de los *joins* entre tablas.

## La estructura estrella: lista de diccionarios

Combinando lista y diccionario se obtiene la representación estándar de un **dataset**: una **lista** (las filas) de **diccionarios** (los campos de cada fila). Ver [[lista de diccionarios y JSON]].

## Puente con Tecnologías

Cada una de estas cuatro tiene su "versión con superpoderes" más adelante: la **lista** se convierte en un `array` de NumPy cuando todos sus elementos son del mismo tipo (ver [[01 - Introduccion y arrays]]); el **diccionario** se convierte en una `Series` de Pandas cuando le agregás un índice explícito (ver [[01 - Introduccion a Series y DataFrame]]); y las operaciones de **conjunto** (`|`, `&`, `-`) son la base conceptual de `concat`/`merge` entre DataFrames (ver [[05 - Combinar datasets (concat, merge, join)]]).

## Relacionado
- [[01 - Introduccion a la programacion]]
- [[indexado y slicing]]
- [[mutabilidad e inmutabilidad]]
- [[hashing y hashabilidad]]
- [[lista de diccionarios y JSON]]
- [[01 - Introduccion y arrays]]
- [[01 - Introduccion a Series y DataFrame]]
- [[05 - Combinar datasets (concat, merge, join)]]
