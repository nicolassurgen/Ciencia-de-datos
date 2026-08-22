---
titulo: "Búsqueda lineal y búsqueda binaria"
materia: Algoritmos
tipo: concepto
tags:
  - algoritmos
  - maestria
  - python
  - tema/busqueda-y-ordenamiento
fecha: 2026-08-22
---

# Búsqueda lineal y búsqueda binaria

Imaginate dos formas de buscar el comprobante del 14 de marzo. En la primera, tenés una caja con comprobantes tirados sin ningún orden, y no queda otra que sacarlos uno por uno hasta encontrarlo (o hasta vaciar la caja y confirmar que no está). En la segunda, tenés una carpeta con los comprobantes ya archivados por fecha, y podés abrirla más o menos por la mitad, ver si te pasaste o te quedaste corto, y repetir el truco sobre la mitad que corresponda — en pocos intentos llegás. Esa diferencia —revisar todo vs. aprovechar un orden ya existente— es exactamente la diferencia entre búsqueda lineal y búsqueda binaria.

## El problema

**Dado un conjunto de datos y un valor, decidir si ese valor está presente y, si lo está, en qué posición.** Es una de las preguntas más frecuentes en cualquier programa: "¿este cliente ya existe?", "¿este ID ya fue procesado?", "¿dónde está el registro que necesito actualizar?".

## Búsqueda lineal: la estrategia que siempre funciona

> [!definition] Búsqueda lineal (sequential search)
> Recorrer los elementos uno por uno, en el orden en que están, comparando cada uno con el valor buscado, hasta encontrarlo o llegar al final. "As you may be able to guess, a linear or exhaustive search simply loops through the items in the array, looking for the target item." *Fuente: [[Essential Algorithms A Practical Approach to Computer Algorithms]], cap. 7.*

```python
def busqueda_lineal(lista, objetivo):
    """Devuelve la posición del objetivo, o -1 si no está."""
    for i in range(len(lista)):
        if lista[i] == objetivo:
            return i
    return -1
```

Su análisis de complejidad no tiene secretos: en el peor caso (el dato está al final, o no está) hay que revisar los `n` elementos → **O(n)**. En el caso promedio, si el dato está en una posición cualquiera, se revisan en promedio `n/2` elementos — que sigue siendo O(n), porque la notación Big O descarta constantes (ver [[notación Big O y familias de complejidad]]).

> [!important] Su virtud: no exige nada
> La búsqueda lineal funciona sobre **cualquier** colección de datos, estén ordenados o no, y hasta sobre estructuras donde "saltar" de una posición a otra no es posible (una lista enlazada, por ejemplo). Es la opción por defecto cuando no se puede garantizar ningún orden previo.

> [!tip] Un matiz que suele pasarse por alto: la lineal también se aprovecha de datos ordenados
> Si la lista **está** ordenada, la búsqueda lineal puede cortar antes de llegar al final: en cuanto encuentra un valor mayor al buscado, ya sabe que el dato no está (porque todo lo que sigue es todavía más grande) y puede devolver "no está" sin revisar el resto. Sigue siendo O(n) en el peor caso, pero ahorra trabajo en la práctica sin necesitar el algoritmo de búsqueda binaria completo. *Fuente: [[Essential Algorithms A Practical Approach to Computer Algorithms]], cap. 7.*

## Búsqueda binaria: aprovechar el orden

> [!definition] Búsqueda binaria (binary search)
> Sobre una lista **ordenada**, mirar el elemento del medio: si coincide con el buscado, listo; si el buscado es menor, descartar toda la mitad derecha y repetir sobre la izquierda; si es mayor, descartar la izquierda y repetir sobre la derecha. En cada paso el problema se reduce a la mitad. "The algorithm keeps track of the largest and smallest indices the target item might have in the array [...] The algorithm then calculates the index halfway between min and max [...] If the target is less than the array's value at mid, the algorithm resets max to search the left half of the array and starts over." *Fuente: [[Essential Algorithms A Practical Approach to Computer Algorithms]], cap. 7.*

```python
def busqueda_binaria(lista, objetivo):
    """Busca en una lista ORDENADA. Devuelve la posición, o -1 si no está."""
    izq, der = 0, len(lista) - 1
    while izq <= der:
        medio = (izq + der) // 2
        if lista[medio] == objetivo:
            return medio
        elif lista[medio] < objetivo:
            izq = medio + 1
        else:
            der = medio - 1
    return -1
```

### Por qué es logarítmica, paso a paso

Partiendo de `n` candidatos, cada paso descarta la mitad:

$$n \to \frac{n}{2} \to \frac{n}{4} \to \dots \to 1$$

La pregunta "¿cuántas veces se puede dividir `n` por 2 hasta llegar a 1?" es, literalmente, la definición de logaritmo en base 2 (ver [[04 - Funciones exponenciales y logaritmicas|Funciones exponenciales y logaritmicas]] de Matemática). De ahí sale la complejidad:

$$\text{Búsqueda binaria} = O(\log n)$$

> [!important] La demostración formal
> "Binary search in an ordered array with N keys uses no more than ⌊lg N⌋ + 1 compares for a search (successful or unsuccessful)." La prueba usa una recurrencia: si $C(N)$ son las comparaciones necesarias para $N$ elementos, entonces $C(N) \le C(\lfloor N/2 \rfloor) + 1$ — una comparación reduce el problema a la mitad. Resolviendo esa recurrencia por sustitución sucesiva se llega a $C(N) \approx \log_2 N$. *Fuente: [[Algorithms-4th-Edition-By-Robert Sedgewick and Kevin Wayne]], cap. 3.1 (Proposición B).*

Una tabla que da la dimensión real de la diferencia (verificado en este entorno, peor caso de cada estrategia):

| n | Lineal | Binaria |
|---:|---:|---:|
| 1.000 | 1.000 | 10 |
| 1.000.000 | 1.000.000 | 20 |
| 1.000.000.000 | 1.000.000.000 | 30 |

Para mil millones de elementos, la diferencia es entre mil millones de comparaciones y **30**. La bibliografía de referencia de la materia usa exactamente esta escala para ilustrar por qué "logarítmico" no es solo "mejor que lineal" sino "mejor por un margen casi incomprensible" cuando los datos crecen: *"After O(log N) steps, the section of the array that might hold the target contains only one item [...] That means the algorithm has O(log N) run time."* *Fuente: [[Essential Algorithms A Practical Approach to Computer Algorithms]], cap. 7*, con una tabla propia (Table 7-1) que muestra que buscar entre 1 billón (10¹²) de elementos toma alrededor de **40 pasos**.

## El requisito que no se puede saltear

> [!warning] Sin orden previo, no hay búsqueda binaria
> La búsqueda binaria **exige** que la lista esté ordenada. No es una optimización que se pueda aplicar "a veces sí, a veces no" sobre datos desordenados — sobre una lista sin ordenar, el algoritmo directamente da resultados incorrectos, porque descartar la mitad "izquierda" o "derecha" solo tiene sentido si esa mitad efectivamente contiene únicamente valores menores o mayores. Esa exigencia es la razón por la que existe la pregunta de [[muestreo y diseño muestral|¿conviene ordenar antes de buscar?]] — ordenar tiene un costo, y solo vale la pena pagarlo si se va a aprovechar.

## La versión recursiva

```python
def busqueda_binaria_rec(lista, objetivo, izq=0, der=None):
    if der is None:
        der = len(lista) - 1
    if izq > der:                    # CASO BASE: rango vacío, no está
        return -1
    medio = (izq + der) // 2
    if lista[medio] == objetivo:     # CASO BASE: lo encontré
        return medio
    elif lista[medio] < objetivo:
        return busqueda_binaria_rec(lista, objetivo, medio + 1, der)
    else:
        return busqueda_binaria_rec(lista, objetivo, izq, medio - 1)
```

> [!tip] Por qué esta recursión nunca se pasa de rosca
> La profundidad de la recursión es $\log_2 n$ — para mil millones de elementos, apenas 30 llamadas anidadas, muy lejos del límite de Python. Contrastá esto con Fibonacci recursivo sin memoizar (ver [[recursion y memoizacion]]), que se vuelve impracticable con `n` de solo unos pocos miles: **la recursión no es cara por ser recursión — es cara cuando el árbol de llamadas se ramifica en más de una rama por paso.** La búsqueda binaria nunca se ramifica: en cada llamada se descarta una mitad entera y se sigue con una sola.

## En código: `bisect`, búsqueda binaria de la biblioteca estándar

Python trae la búsqueda binaria ya implementada en el módulo `bisect`, para no tener que escribirla de nuevo cada vez:

```python
import bisect

masas = sorted(p["masa_g"] for p in pinguinos)  # tiene que estar ordenada

posicion = bisect.bisect_left(masas, 4000)   # primera posición donde podría insertarse 4000
```

`bisect.bisect_left(lista, valor)` devuelve la posición donde el valor **entraría** en la lista ordenada, manteniendo el orden — que, como efecto colateral útil, también dice **cuántos elementos son menores** a ese valor: es literalmente un percentil calculado en O(log n) en vez de recorrer toda la lista. Ver un uso real y verificado de esto, con el dataset de pingüinos, en [[04 - Busqueda y ordenamiento]].

> [!tip] La primera aparición de un valor repetido
> La búsqueda binaria básica encuentra **una** posición donde está el valor, pero si hay repetidos no garantiza que sea la primera. La forma de resolverlo sin perder la complejidad O(log n): cuando se encuentra una coincidencia, no cortar — guardar esa posición como la mejor candidata hasta ahora y seguir buscando en la mitad **izquierda**, por si hay una coincidencia todavía más temprana. Es exactamente lo que hace `bisect.bisect_left` internamente.

## Cuándo usar cada una

| | Búsqueda lineal | Búsqueda binaria |
|---|---|---|
| Requisito | Ninguno | Datos ordenados |
| Complejidad | O(n) | O(log n) |
| Funciona sobre listas enlazadas | Sí | No (necesita acceso directo a una posición) |
| Conviene cuando | Se busca una sola vez, o los datos cambian todo el tiempo | Se busca muchas veces sobre los mismos datos |

## Relacionado
- [[04 - Busqueda y ordenamiento]]
- [[notación Big O y familias de complejidad]]
- [[recursion y memoizacion]]
- [[ordenamiento burbuja, selección e inserción]]
- [[complejidad O(1) vs O(n)]]
