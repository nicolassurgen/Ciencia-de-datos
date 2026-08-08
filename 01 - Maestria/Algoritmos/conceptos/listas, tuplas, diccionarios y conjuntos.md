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

`.count(valor)` cuenta cuántas veces aparece un valor — funciona igual en listas y tuplas (`(1, 2, 2, 3).count(2)` → `2`).

> [!tip] Desempaquetado con "el resto": `*rest`
> Cuando solo importan los primeros valores y el resto se quiere agrupar en una lista, `*` captura "todo lo que sobra":
> ```python
> primero, segundo, *resto = [10, 20, 30, 40, 50]
> print(primero, segundo, resto)   # 10 20 [30, 40, 50]
> ```
> Por convención, cuando ese resto no importa y solo se quiere "descartarlo", se usa `_` como nombre: `primero, segundo, *_ = valores`. *Fuente: [[Python-for-Data-Analysis]], cap. 3.*

## Diccionario — pares clave → valor

Resuelve el problema de acceder "por posición" (`tabla[2][3]`, hay que recordar qué es la columna 3): en un diccionario se accede **por nombre** (`pinguino["masa_g"]`). Las claves deben ser **únicas e inmutables** (ver [[hashing y hashabilidad]]); los valores pueden ser cualquier cosa. `.get()` es la forma segura de acceder sin arriesgarse a un `KeyError`.

`dict(zip(claves, valores))` construye un diccionario a partir de dos listas paralelas — el mismo `zip()` ya visto para recorrer dos secuencias a la vez, aplicado a construir en vez de iterar:
```python
especies = ["Adelie", "Gentoo", "Chinstrap"]
conteos = [152, 124, 68]
dict(zip(especies, conteos))   # {'Adelie': 152, 'Gentoo': 124, 'Chinstrap': 68}
```

> [!tip] `setdefault()`: una línea en vez de `if`/`else`
> El patrón "acumular en un diccionario, inicializando la clave la primera vez que aparece" (el `group by` a mano que ya apareció en la clase 1) suele escribirse así:
> ```python
> if especie not in conteo:
>     conteo[especie] = []
> conteo[especie].append(pico_mm)
> ```
> `setdefault(clave, valor_si_no_existe)` hace lo mismo en una línea: devuelve el valor de la clave si ya existe, o lo crea con el valor por defecto (y lo devuelve) si no:
> ```python
> conteo.setdefault(especie, []).append(pico_mm)
> ```
> Si el acumulador se usa mucho, `collections.defaultdict` va un paso más allá: ni siquiera hace falta `setdefault`, el diccionario crea la clave automáticamente la primera vez que se la usa:
> ```python
> from collections import defaultdict
> conteo = defaultdict(list)          # cada clave nueva arranca con una lista vacía
> for p in pinguinos:
>     conteo[p["especie"]].append(p["pico_mm"])   # sin chequear si la clave ya existe
> ```
> *Fuente: [[Python-for-Data-Analysis]], cap. 3.*

## Conjunto — sin orden y sin repetidos

El conjunto matemático de siempre: `set(columna)` da los valores únicos de una lista. Preguntar "¿está este elemento?" en un conjunto es **inmediato** (ver [[complejidad O(1) vs O(n)]]), a diferencia de recorrer una lista entera. Soporta operaciones de conjunto (`|` unión, `&` intersección, `-` diferencia, `^` diferencia simétrica), la base conceptual de los *joins* entre tablas.

| Método | Qué hace |
|---|---|
| `s.issubset(t)` / `s <= t` | ¿todos los elementos de `s` están en `t`? |
| `s.issuperset(t)` / `s >= t` | ¿`s` contiene a todos los elementos de `t`? |
| `s.isdisjoint(t)` | ¿no comparten ningún elemento? |
| `s.discard(x)` | Elimina `x` si está — a diferencia de `s.remove(x)`, no lanza error si no está |
| `s.pop()` | Saca y devuelve un elemento arbitrario (los conjuntos no tienen orden) |
| `s.clear()` | Vacía el conjunto |

> [!info] `frozenset`: la versión inmutable de un conjunto
> Un `set` es mutable — y por eso, igual que una lista, **no puede** ser clave de diccionario ni elemento de otro conjunto (ver [[hashing y hashabilidad]]). `frozenset({1, 2, 3})` es la versión inmutable: mismas operaciones de conjunto, pero al ser hasheable, sí puede usarse como clave o guardarse dentro de otro `set`. Es a `set` lo que la tupla es a la lista. *Fuente: [[Data Structures and Algorithms with Python]], cap. 5.*

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
