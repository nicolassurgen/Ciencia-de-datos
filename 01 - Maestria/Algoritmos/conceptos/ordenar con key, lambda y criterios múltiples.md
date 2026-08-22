---
titulo: "Ordenar con key, lambda y criterios múltiples"
materia: Algoritmos
tipo: concepto
tags:
  - algoritmos
  - maestria
  - python
  - tema/busqueda-y-ordenamiento
fecha: 2026-08-22
---

# Ordenar con key, lambda y criterios múltiples

`sorted([3, 1, 2])` alcanza cuando lo que hay que ordenar son números sueltos. Pero en la práctica casi nunca se ordenan números sueltos — se ordenan **registros**: filas de una planilla, comprobantes, clientes, cada uno con varios campos. La pregunta deja de ser "¿cuál es más chico?" y pasa a ser "¿más chico **según qué campo**?". Esta nota es sobre cómo Python responde esa pregunta.

## El problema

**Dada una lista de registros (por ejemplo, diccionarios) y un campo, ordenarlos según ese campo** — y, muchas veces, según más de uno a la vez (por vendedor y, dentro de cada vendedor, por fecha).

## El parámetro `key`: decirle a `sorted()` qué mirar

```python
pinguinos = [{"especie": "Adelie", "masa_g": 3700}, {"especie": "Gentoo", "masa_g": 5000}, ...]

por_masa = sorted(pinguinos, key=lambda p: p["masa_g"])
```

`sorted()` no sabe, por sí solo, cómo comparar dos diccionarios — un diccionario no tiene un "menor que" natural. El parámetro `key` resuelve exactamente eso: recibe una **función**, se la aplica a cada elemento antes de comparar, y ordena según lo que esa función devuelve, no según el elemento completo.

> [!definition] `key` en `sorted()` / `.sort()`
> "One is the ability to pass a secondary sort key — that is, a function that produces a value to use to sort the objects." *Fuente: [[Python-for-Data-Analysis]], cap. 3.* Internamente, Python llama a la función `key` **una vez por cada elemento** (no en cada comparación), guarda los resultados, y compara esos resultados en vez de los elementos originales — por eso ordenar con `key` no es más lento que ordenar los valores ya extraídos directamente.

### `lambda`: una función sin nombre, para usar una sola vez

`lambda p: p["masa_g"]` es una **función anónima** (desarrollada en profundidad en [[funciones, parametros y alcance]]): equivale a escribir

```python
def obtener_masa(p):
    return p["masa_g"]
```

pero sin el paso de ponerle un nombre a algo que solo se va a usar en ese único lugar. `lambda` no admite `if`/`for` completos ni varias líneas — solo una expresión que se evalúa y se devuelve.

> [!tip] Cuando la clave ya es una función que existe, no hace falta `lambda`
> Si lo que se necesita como clave es directamente el resultado de una función ya definida —incluso una incorporada al lenguaje—, se la puede pasar tal cual, sin envolverla: `sorted(palabras, key=len)` ordena strings por longitud usando la función `len` directamente, sin necesidad de escribir `key=lambda p: len(p)`. Ejemplo real: `["saw", "small", "He", "foxes", "six"]` ordenado con `key=len` da `['He', 'saw', 'six', 'small', 'foxes']`. *Fuente: [[Python-for-Data-Analysis]], cap. 3.*

> [!warning] Una limitación práctica de `lambda`, útil al depurar
> Las funciones `lambda` no tienen nombre propio — en un traceback de error aparecen literalmente como `<lambda>`, lo que puede dificultar identificar cuál de varios lambdas del código causó el problema. Para lógica que se reutiliza en más de un lugar, o que es difícil de leer en una sola línea, conviene una función con `def` y nombre propio en lugar de un `lambda`. *Fuente: [[Python-for-Data-Analysis]], cap. 10.*

## Orden descendente

```python
mas_pesados = sorted(pinguinos, key=lambda p: p["masa_g"], reverse=True)
```

`reverse=True` invierte el sentido de la comparación completa — no requiere invertir manualmente el signo ni escribir una función distinta.

> [!info] A futuro: el top-k sin ordenar todo
> Cuando solo interesan los primeros `k` elementos (un top 10, por ejemplo), ordenar la lista **completa** para después quedarse con una porción es más trabajo del necesario: `sorted(...)` es O(n log n) sobre **todos** los elementos. El módulo `heapq` de la biblioteca estándar de Python ofrece `heapq.nlargest(k, lista, key=...)` y `heapq.nsmallest(k, lista, key=...)`, que resuelven el mismo problema en O(n log k) — con `k` chico frente a `n`, la diferencia es real. (Pandas resuelve el mismo problema con `Series.nlargest()`/`nsmallest()`, una API distinta para la misma idea. *Fuente: [[Python-for-Data-Analysis]], cap. 10.*)

## Ordenar por varias claves: una tupla como `key`

```python
ordenado = sorted(pinguinos, key=lambda p: (p["especie"], -p["masa_g"]))
```

Python compara tuplas **elemento a elemento**: primero compara el primer valor de cada tupla; si empatan, recién ahí pasa a comparar el segundo. Es la misma lógica con la que se comparan fechas escritas como `(año, mes, día)`, o con la que una planilla de cálculo ordena "primero por columna A, después por columna B".

> [!tip] Antecedente de esta idea en la bibliografía
> El mismo mecanismo —dejar que Python compare tuplas directamente, sin necesidad de una función `key`— aparece para resolver el problema de encontrar el top-N de una categoría por conteo: se arma una lista de tuplas `(conteo, categoría)` y se la ordena tal cual, aprovechando que comparar tuplas ya hace "primero por conteo, y ante empate, por categoría" sin ningún código adicional. *Fuente: [[Python-for-Data-Analysis]], cap. 13.*

El truco de `-p["masa_g"]` en el ejemplo de arriba invierte el orden de **ese campo únicamente**, dejando el resto de la tupla con su orden normal — aprovecha que invertir el signo de un número invierte su orden de comparación. Funciona con números; para invertir el orden de un campo de texto dentro de una tupla hace falta otro recurso (por ejemplo, ordenar dos veces por separado, apoyándose en que `sorted()` es estable — ver [[estabilidad de un ordenamiento]]).

## Por qué esto depende de la estabilidad

> [!important] Ordenar "en etapas" solo funciona porque `sorted()` es estable
> Ordenar primero por masa y **después** por especie da el mismo resultado que ordenar de una sola vez con la tupla `(especie, -masa)`. Eso no es una casualidad de este ejemplo puntual — es una consecuencia directa de que `sorted()` de Python es un ordenamiento **estable**: la segunda pasada (por especie) no altera el orden por masa que ya quedó establecido dentro de cada especie. El desarrollo completo, con la verificación de que ambas formas dan el mismo resultado sobre datos reales, está en [[estabilidad de un ordenamiento]].

## Relacionado
- [[funciones, parametros y alcance]]
- [[estabilidad de un ordenamiento]]
- [[ordenamiento burbuja, selección e inserción]]
- [[búsqueda lineal y búsqueda binaria]]
- [[04 - Busqueda y ordenamiento]]
