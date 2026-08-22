---
titulo: "Ordenamiento burbuja, selección e inserción"
materia: Algoritmos
tipo: concepto
tags:
  - algoritmos
  - maestria
  - python
  - tema/busqueda-y-ordenamiento
fecha: 2026-08-22
---

# Ordenamiento burbuja, selección e inserción

Pensá en tres formas distintas de ordenar una pila de facturas por monto, a mano, sin ninguna herramienta más que tus propios ojos y manos:

- **Comparar vecinas y cambiarlas de lugar si están al revés**, una y otra vez, hasta que ya no haga falta cambiar ninguna más.
- **Buscar la factura más chica de todo el montón** y ponerla primera; buscar la más chica de lo que queda y ponerla segunda; y así.
- **Ir tomando una factura a la vez del montón desordenado** e insertarla en el lugar que le corresponde dentro del montón ya ordenado que se va armando al lado.

Esas tres formas son, exactamente, burbuja, selección e inserción — los tres ordenamientos elementales. Ninguno es rápido para volúmenes grandes (los tres son O(n²)), pero cada uno enseña una idea de diseño de algoritmos distinta, y entenderlos es lo que permite después apreciar **por qué** el ordenamiento real de Python (Timsort, desarrollado al final de esta nota) es tan superior.

## El problema

**Dada una lista, reorganizar sus elementos según un criterio de orden** (de menor a mayor, alfabético, por fecha). Ordenar habilita la [[búsqueda lineal y búsqueda binaria|búsqueda binaria]], permite calcular medianas y percentiles, agrupar valores iguales y construir rankings.

## Burbuja (*bubble sort*)

> [!definition] Ordenamiento burbuja
> Recorrer la lista comparando cada par de elementos adyacentes; si están en el orden incorrecto, intercambiarlos. Repetir pasadas completas hasta que una pasada entera no necesite ningún intercambio. "Bubblesort uses the fairly obvious fact that, if an array is not sorted, it must contain two adjacent elements that are out of order [...] The fact that item [...] seems to slowly bubble up to its correct position gives the bubblesort algorithm its name." *Fuente: [[Essential Algorithms A Practical Approach to Computer Algorithms]], cap. 6.*

```python
def burbuja(lista):
    a = lista.copy()
    n = len(a)
    for i in range(n):
        for j in range(n - 1 - i):
            if a[j] > a[j + 1]:
                a[j], a[j + 1] = a[j + 1], a[j]
    return a
```

Cada pasada completa "empuja" el elemento más grande de lo que queda hasta el final — de ahí que, después de la pasada `i`, los últimos `i` elementos ya estén en su posición definitiva y no haga falta volver a mirarlos (`range(n - 1 - i)`).

**Análisis:** peor caso (lista al revés) y caso promedio hacen `n(n-1)/2` comparaciones → **O(n²)**. El mejor caso (ya ordenada), en esta versión, también da todas las vueltas igual → sigue siendo O(n²), aunque no haga ningún intercambio.

> [!important] La optimización que cambia todo: cortar cuando ya está ordenada
> Agregando una sola bandera que registre si hubo algún intercambio en la pasada, se puede cortar apenas una pasada completa no encuentre nada para intercambiar — señal inequívoca de que la lista ya quedó ordenada. Con esa única línea de más, el **mejor caso** pasa de O(n²) a **O(n)**. El peor caso sigue siendo O(n²), pero en datos parcialmente ordenados —muy comunes en la práctica— el ahorro es enorme: medido en este entorno, sobre 3.000 elementos ya ordenados, la versión optimizada tardó unas 1.250 veces menos que la simple.

```python
def burbuja_optimizada(lista):
    a = lista.copy()
    n = len(a)
    for i in range(n):
        hubo_intercambio = False
        for j in range(n - 1 - i):
            if a[j] > a[j + 1]:
                a[j], a[j + 1] = a[j + 1], a[j]
                hubo_intercambio = True
        if not hubo_intercambio:
            break
    return a
```

> [!warning] La bibliografía no coincide en si vale la pena enseñarlo
> Es un dato interesante en sí mismo: **Sedgewick & Wayne no mencionan la burbuja ni una sola vez** en todo su libro — los únicos "ordenamientos elementales" que desarrollan son selección e inserción. *Essential Algorithms*, en cambio, sí la cubre en profundidad y hasta la defiende para listas chicas, con datos concretos de mejora al optimizarla (2,50 s → 0,69 s sobre 10.000 elementos) y describe una variante bidireccional —alternar el sentido de cada pasada— que resuelve el problema del elemento chico ubicado al final que tarda muchísimas pasadas en llegar al principio (se lo apoda la "tortuga"). Esa variante bidireccional es, precisamente, el **cocktail sort**. *Fuente: [[Essential Algorithms A Practical Approach to Computer Algorithms]], cap. 6.* No hay que leer esto como que un libro "tiene razón" y el otro no: es un recordatorio de que incluso la bibliografía técnica tiene preferencias pedagógicas propias.

## Selección (*selection sort*)

> [!definition] Ordenamiento por selección
> Buscar el elemento más chico de toda la lista y ponerlo en la primera posición; buscar el más chico de lo que queda y ponerlo en la segunda; repetir hasta el final. "The basic idea is to search the input list for the largest item it contains and then add it to the end of a growing sorted list. Alternatively, the algorithm can find the smallest item and move it to the beginning of the growing list." *Fuente: [[Essential Algorithms A Practical Approach to Computer Algorithms]], cap. 6.*

```python
def seleccion(lista):
    a = lista.copy()
    n = len(a)
    for i in range(n):
        pos_min = i
        for j in range(i + 1, n):
            if a[j] < a[pos_min]:
                pos_min = j
        a[i], a[pos_min] = a[pos_min], a[i]
    return a
```

**Análisis:** siempre hace `n(n-1)/2` comparaciones, **sin importar el orden de entrada** — peor caso, promedio y mejor caso son los tres O(n²). No admite la optimización de "cortar antes" que sí tiene la burbuja.

> [!important] Dos propiedades que la distinguen, aunque comparta la misma Big O que las otras
> "Running time is insensitive to input [...] Data movement is minimal": tarda exactamente igual con una lista ya ordenada que con una completamente al azar (a diferencia de inserción, que sí varía), y hace como máximo `n − 1` **intercambios** en total — muchos menos que la burbuja, que puede necesitar cientos. Si mover cada elemento fuera costoso (por ejemplo, si cada uno fuera un registro grande en vez de un número suelto), la selección resultaría preferible por esa sola razón, aunque las tres compartan la misma complejidad en el papel. *Fuente: [[Algorithms-4th-Edition-By-Robert Sedgewick and Kevin Wayne]], cap. 2.1 (Proposición A).*

## Inserción (*insertion sort*)

> [!definition] Ordenamiento por inserción
> Tomar cada elemento, uno a la vez, e insertarlo en la posición que le corresponde dentro de la parte de la lista que ya está ordenada — como ordenar cartas en la mano. "The basic idea is to take an item from the input list and insert it into the proper position in the sorted output list (which initially starts empty)." *Fuente: [[Essential Algorithms A Practical Approach to Computer Algorithms]], cap. 6.*

```python
def insercion(lista):
    a = lista.copy()
    for i in range(1, len(a)):
        actual = a[i]
        j = i - 1
        while j >= 0 and a[j] > actual:
            a[j + 1] = a[j]
            j -= 1
        a[j + 1] = actual
    return a
```

**Análisis:** peor caso (al revés) → **O(n²)**; caso promedio → **O(n²)**; mejor caso (ya ordenada, el `while` nunca entra) → **O(n)**. La cifra exacta ya está desarrollada en [[notación Big O y familias de complejidad]]: mejor caso $n-1$ comparaciones, promedio $\sim n^2/4$, peor caso $\sim n^2/2$.

> [!important] Por qué inserción es "el mejor de los tres" en la práctica: las inversiones
> La cantidad de intercambios que hace insertion sort es exactamente igual a la cantidad de **inversiones** de la lista de entrada — pares de elementos que están fuera de orden entre sí (por ejemplo, en `[3, 1, 2]`, el par `(3,1)` y el par `(3,2)` son inversiones, dos en total). Una lista con pocas inversiones se llama **parcialmente ordenada**, y son extremadamente comunes con datos reales: una tabla que ya viene casi ordenada de otra fuente, un archivo al que solo se le agregaron unas pocas filas nuevas al final. Sobre ese tipo de datos, insertion sort la ordena casi al costo de recorrerla una vez, muy lejos de su peor caso teórico. *Fuente: [[Algorithms-4th-Edition-By-Robert Sedgewick and Kevin Wayne]], cap. 2.1 (Proposición C).*

## Comparación directa

| | Peor caso | Promedio | Mejor caso | Intercambios | ¿Sensible al orden de entrada? |
|---|---|---|---|---|---|
| Burbuja | O(n²) | O(n²) | O(n)* | Muchos | Solo con la optimización |
| Selección | O(n²) | O(n²) | O(n²) | Pocos (máx. n−1) | No |
| Inserción | O(n²) | O(n²) | O(n) | Depende de las inversiones | Sí |

\* solo con la versión que detecta pasadas sin intercambios.

> [!tip] Misma Big O, comportamiento distinto — la lección de fondo
> Los tres son O(n²) en el peor caso, y sin embargo, medido en este entorno sobre datos reales (ver [[04 - Busqueda y ordenamiento]]), se comportan de forma muy distinta según cómo vengan los datos: la selección tarda igual siempre, la inserción y la burbuja optimizada son casi instantáneas con datos ya ordenados. **La notación Big O describe el crecimiento en el peor caso, no todos los matices del comportamiento real** — dos algoritmos con la misma Big O pueden ser muy distintos en la práctica.

## El ordenamiento real: Timsort

Ninguno de los tres elementales es lo que usa Python. `sorted()` y `list.sort()` corren **Timsort**, diseñado por Tim Peters en 2002 para CPython — hoy también lo usan Java, Android, Swift y V8.

> [!definition] Timsort
> Algoritmo **híbrido** que combina mergesort (que garantiza O(n log n) siempre) con insertion sort (que es muy rápido en tramos chicos y en datos casi ordenados). Su rasgo distintivo es que **detecta tramos ya ordenados** en los datos reales (llamados *runs*) y los aprovecha directamente, en vez de reordenarlos desde cero.

Es exactamente la propiedad de inserción sobre datos parcialmente ordenados —desarrollada arriba— la que Timsort explota a propósito: en vez de tratar toda la entrada como si viniera completamente al azar, primero busca tramos que ya están ordenados (algo habitual en datos reales: registros con fecha, tablas que ya vienen ordenadas de otra fuente) y usa inserción para pulir esos tramos chicos, mergesort para combinarlos entre sí garantizando el límite de O(n log n).

> [!warning] Una fuente de la bibliografía tiene un dato desactualizado
> *Data Structures and Algorithms with Python* afirma que el ordenamiento nativo de Python "is quicksort implemented in C" — es un dato **incorrecto**: CPython usa Timsort desde 2003 (versión 2.3), no quicksort. Vale la pena señalarlo explícitamente como ejemplo de por qué conviene contrastar más de una fuente antes de dar un dato técnico por sentado. *Fuente del error: [[Data Structures and Algorithms with Python]], cap. 9.*

| | Mejor | Promedio | Peor | ¿Estable? |
|---|---|---|---|---|
| Burbuja | O(n)* | O(n²) | O(n²) | Sí |
| Selección | O(n²) | O(n²) | O(n²) | No |
| Inserción | O(n) | O(n²) | O(n²) | Sí |
| **Timsort** | **O(n)** | **O(n log n)** | **O(n log n)** | **Sí** |

Qué significa la columna "estable" —y por qué no es un detalle menor— se desarrolla en [[estabilidad de un ordenamiento]].

> [!important] Por qué O(n log n) no es "buena suerte" del diseño
> Se puede demostrar matemáticamente (con un argumento de árbol de decisión, desarrollado en [[notación Big O y familias de complejidad]]) que **ningún** algoritmo que ordene comparando elementos de a pares puede hacerlo, en el peor caso, con menos de aproximadamente `n log n` comparaciones. Mergesort, quicksort y Timsort no son simplemente "buenos" — son **óptimos** dentro de lo matemáticamente alcanzable para esta clase de algoritmos. *Fuente: [[Algorithms-4th-Edition-By-Robert Sedgewick and Kevin Wayne]], cap. 2.2 (Proposición I y J).*

Medido en este entorno, sobre datos al azar, `sorted()` de Python resultó cientos de veces más rápido que los tres elementales, y esa ventaja **crece** con el volumen de datos (al duplicar `n`, inserción cuadruplica su tiempo — la firma de O(n²) — mientras `sorted()` apenas lo duplica). Desarrollo completo, con la tabla y el gráfico verificados, en [[04 - Busqueda y ordenamiento]].

> [!important] Conclusión práctica
> Implementar estos tres algoritmos a mano sirve para entender **cómo** ordenar y **por qué** unos comportamientos son mejores que otros — no para usarlos en un programa real. En cualquier trabajo con Python, la herramienta correcta es siempre `sorted()` o `.sort()`.

## Relacionado
- [[04 - Busqueda y ordenamiento]]
- [[notación Big O y familias de complejidad]]
- [[estabilidad de un ordenamiento]]
- [[búsqueda lineal y búsqueda binaria]]
- [[ordenar con key, lambda y criterios múltiples]]
