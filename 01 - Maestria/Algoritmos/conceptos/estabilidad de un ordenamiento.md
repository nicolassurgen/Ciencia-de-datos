---
titulo: "Estabilidad de un ordenamiento"
materia: Algoritmos
tipo: concepto
tags:
  - algoritmos
  - maestria
  - python
  - tema/busqueda-y-ordenamiento
fecha: 2026-08-22
---

# Estabilidad de un ordenamiento

Pensá en una planilla de ventas ya cargada en el orden en que ocurrieron, del 1º al 31 de marzo, y ahora la ordenás por vendedor para ver el total de cada uno. Dentro del grupo de un mismo vendedor, ¿las filas quedan en el mismo orden de fecha en que estaban antes de ordenar por vendedor? La respuesta depende de una propiedad del algoritmo de ordenamiento que se usó, y esa propiedad tiene nombre: **estabilidad**.

## El problema

Cuando dos elementos **empatan** en el criterio de orden (dos ventas del mismo vendedor, dos pingüinos de la misma especie), un algoritmo de ordenamiento tiene que decidir en qué orden dejarlos entre sí — y no todos deciden lo mismo.

> [!definition] Ordenamiento estable
> Un ordenamiento es estable si, cuando dos elementos tienen el mismo valor según el criterio de orden, **conservan entre sí el orden relativo que tenían antes de ordenar**. "A stable sorting algorithm is one that maintains the original relative positioning of equivalent values. For example, suppose a program is sorting Car objects by their Cost properties and Car objects A and B have the same Cost values. If object A initially comes before object B in the array, then in a stable sorting algorithm, object A still comes before object B in the sorted array." *Fuente: [[Essential Algorithms A Practical Approach to Computer Algorithms]], cap. 6.*

Un ordenamiento **inestable**, en cambio, no da esa garantía: puede dejar a A antes de B, después de B, o mezclarlos de cualquier forma — el resultado sigue estando "bien ordenado" según el criterio pedido, pero el orden interno entre los empatados queda librado al funcionamiento interno del algoritmo, no a lo que había antes.

## Por qué importa: permite ordenar "en etapas"

> [!important] La consecuencia práctica de la estabilidad
> "If the items you are sorting are value types such as integers, dates, or strings, then two entries with the same values are equivalent, so it doesn't matter if the sort is stable [...] In contrast, you might care if [registros] are rearranged unnecessarily. A stable sort lets you sort the array multiple times to get a result that is sorted on multiple keys." *Fuente: [[Essential Algorithms A Practical Approach to Computer Algorithms]], cap. 6.*

Esto significa que, con un ordenamiento estable, se puede lograr un "ordenar por columna A y, dentro de cada A, por columna B" de **dos formas equivalentes**:

```python
# Forma 1: una sola pasada, con una tupla como clave
ordenado = sorted(pinguinos, key=lambda p: (p["especie"], -p["masa_g"]))

# Forma 2: dos pasadas, en el orden inverso al de importancia
paso1 = sorted(pinguinos, key=lambda p: p["masa_g"], reverse=True)
paso2 = sorted(paso1, key=lambda p: p["especie"])
```

Verificado en este entorno, sobre los 342 registros reales del dataset de pingüinos: **ambas formas dan exactamente el mismo resultado, dato por dato**. Eso solo es posible porque `sorted()` de Python es estable — el segundo `sorted()` (por especie) ordena por especie, pero como el ordenamiento es estable, dentro de cada especie **conserva** el orden por masa que ya había dejado el primer `sorted()`. Si `sorted()` fuera inestable, la segunda pasada podría "revolver" el orden por masa dentro de cada especie, y las dos formas darían resultados distintos.

> [!warning] Sin estabilidad, este truco no funciona
> Es la razón por la que, en general, no se puede asumir que "ordenar en dos pasadas" equivale a ordenar con una tupla — solo es cierto **si** el algoritmo usado es estable. Con un ordenamiento inestable, la única forma confiable de ordenar por varias claves es hacerlo de una sola vez, comparando todas las claves relevantes en el mismo paso (por ejemplo, con una tupla).

## Qué algoritmos son estables

| Algoritmo | ¿Estable? |
|---|:---:|
| Burbuja | Sí |
| Selección | **No** |
| Inserción | Sí |
| Mergesort | Sí |
| Quicksort | No |
| Heapsort | No |
| **Timsort (Python)** | **Sí** |

*Fuente: [[Algorithms-4th-Edition-By-Robert Sedgewick and Kevin Wayne]], cap. 2.5, y [[Essential Algorithms A Practical Approach to Computer Algorithms]], cap. 6.*

> [!tip] Por qué selección es inestable (y burbuja/inserción no)
> Selection sort busca el mínimo de todo el resto de la lista y lo **intercambia** con la posición actual — ese intercambio puede saltar por encima de elementos empatados y cambiar su orden relativo. Burbuja e inserción, en cambio, solo intercambian elementos **adyacentes**, y nunca intercambian dos elementos que ya están en el orden correcto entre sí (incluyendo el caso de empate) — por eso preservan el orden original de los empatados.

> [!important] Por qué esto no es un detalle académico
> Es, ni más ni menos, el motivo por el que se elige un algoritmo estable para una biblioteca estándar de uso general: "Mergesort is easy to implement as a stable sort [...] so it is used by Java's Arrays.sort library method." *Fuente: [[Essential Algorithms A Practical Approach to Computer Algorithms]], cap. 6.* Python hizo la misma elección de fondo con Timsort — es estable a propósito, precisamente para que el patrón de "ordenar por varias columnas, una pasada a la vez" funcione de manera predecible.

## A dónde reaparece

> [!info] El mismo concepto en Pandas
> Esta propiedad no es exclusiva de la búsqueda y ordenamiento "a mano" — es lo que garantiza que `DataFrame.sort_values()` de Pandas se comporte como se espera cuando se lo aplica dos veces seguidas sobre distintas columnas, o al pasarle una lista de columnas de una sola vez. El razonamiento es idéntico al de esta nota: sin estabilidad, encadenar ordenamientos dejaría de ser confiable.

## Relacionado
- [[ordenamiento burbuja, selección e inserción]]
- [[ordenar con key, lambda y criterios múltiples]]
- [[04 - Busqueda y ordenamiento]]
- [[notación Big O y familias de complejidad]]
