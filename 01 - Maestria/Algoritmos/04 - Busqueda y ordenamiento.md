---
titulo: "Clase 4 — Algoritmos de búsqueda y ordenamiento"
materia: Algoritmos
tipo: apunte
clase: 4
fecha: 2026-08-22
tags:
  - algoritmos
  - maestria
  - python
  - busqueda-y-ordenamiento
  - tema/busqueda-y-ordenamiento
---

# Algoritmos · Clase 4 — Algoritmos de búsqueda y ordenamiento

> [!abstract] Idea central de la clase
> Buscar un dato y ordenar una lista son, seguramente, las dos operaciones que más veces por segundo se ejecutan en cualquier sistema de información del mundo — desde el buscador de un sistema contable hasta el motor de una base de datos. Hoy se abren esas dos "cajas negras": se implementan a mano los algoritmos clásicos, se predice matemáticamente cuánto van a tardar (con la notación Big O de la [[03 - Estructuras no lineales y complejidad algoritmica|clase pasada]]) y después se **mide** si la teoría se cumple.
>
> No se trata de que reemplaces `sorted()` de Python por tu propio código — Python ya ordena mejor de lo que vas a programar vos. Se trata de entender **por qué** `sorted()` es tan rápido, **cuándo** conviene ordenar antes de buscar, y **cómo** reconocer que un programa propio tiene un problema de diseño escondido.
>
> Dos ideas para llevarse:
> 1. **Ordenar es una inversión.** Cuesta trabajo hacerlo una vez, pero después cada búsqueda sale mucho más barata. Es exactamente la misma lógica que aplicás cuando archivás comprobantes por fecha antes de que te los pidan: el rato que tardás en ordenar el archivo se paga solo la primera vez que alguien te pide "el comprobante del 14 de marzo" y no tenés que revisar la pila entera.
> 2. **Misma complejidad no significa mismo comportamiento.** Vas a ver tres algoritmos igual de "malos" en el papel (los tres son O(n²)) comportándose de manera muy distinta según cómo vengan los datos. El análisis teórico es el punto de partida, no el final de la historia.

> [!note] Convención de esta nota
> Los callouts marcados **"ampliación"**, las conexiones con otras materias y las notas que dicen "verificado en este entorno" son agregados míos, con cita a la bibliografía de Algoritmos y Python del vault (Sedgewick & Wayne, *Data Structures and Algorithms with Python*, *Essential Algorithms* y *Python for Data Analysis*) — no las dio el profesor. El resto sigue de cerca la clase (`Clase4_Busqueda_y_ordenamiento.ipynb` y `Actividad_Clase4.ipynb`). Todos los números de esta nota —comparaciones, tiempos, resultados sobre datos reales— fueron **recalculados de manera independiente** en este entorno, no copiados de la notebook original (que no traía las salidas guardadas).

---

## 1. Búsqueda: encontrar un dato entre muchos

### El problema

**Dado un conjunto de datos y un valor, decidir si ese valor está — y en qué posición.** Es el equivalente a preguntar "¿este comprobante ya está cargado?" o "¿en qué fila de la planilla está el cliente 4521?". Ya lo hiciste sin nombrarlo: el `for` con `break` de la [[02 - Programacion imperativa|clase 2]] era exactamente esto.

### 1.1 Búsqueda lineal: revisar todo, en orden

La estrategia más obvia — y la única posible si los datos no tienen ningún orden particular — es mirar uno por uno, de principio a fin, hasta encontrarlo o terminar la lista. Es lo que hacés cuando revisás una pila de comprobantes sin ordenar buscando uno en particular: no hay atajo, hay que mirarlos todos si el que buscás resulta ser el último (o si no está).

```python
def busqueda_lineal(lista, objetivo):
    """Devuelve la posición del objetivo, o -1 si no está."""
    for i in range(len(lista)):
        if lista[i] == objetivo:
            return i          # lo encontré: corto acá
    return -1                 # recorrí todo y no estaba
```

> [!definition] Búsqueda lineal (sequential search)
> "As you may be able to guess, a linear or exhaustive search simply loops through the items in the array, looking for the target item." *Fuente: [[Essential Algorithms A Practical Approach to Computer Algorithms]], cap. 7.*

Instrumentando la función para contar cuántas comparaciones hace de verdad, sobre una lista de 1.000 números (verificado en este entorno):

| Buscar | Posición | Comparaciones |
|---:|---:|---:|
| 0 | 0 | 1 |
| 250 | 250 | 251 |
| 500 | 500 | 501 |
| 999 | 999 | 1.000 |
| 5.000 (no está) | -1 | 1.000 |

Se ve con claridad: encontrar el primero cuesta 1 comparación, el último cuesta 1.000, y uno que no está cuesta 1.000 también — **el costo depende de dónde esté el dato**, y en el peor caso hay que revisar la lista entera.

| Caso | Situación | Comparaciones | Complejidad |
|---|---|---|---|
| Mejor | Está en la primera posición | 1 | O(1) |
| Peor | Está al final, o no está | n | **O(n)** |
| Promedio | Está en una posición cualquiera | n/2 | **O(n)** |

Por convención se dice que la búsqueda lineal es **O(n)**: se toma el peor caso, y n/2 sigue siendo O(n) igual — las constantes se descartan (ver [[notación Big O y familias de complejidad]]).

> [!important] Su gran virtud: no exige nada
> La búsqueda lineal funciona sobre **cualquier** lista, ordenada o no. Es lenta, pero es universal — la comparación con la búsqueda binaria de abajo no es "una gana siempre", es "una exige una condición que la otra no exige".

### 1.2 Búsqueda binaria: aprovechar que los datos están ordenados

Ahora se agrega **una condición**: la lista está **ordenada**. Con esa sola condición se puede ser mucho más inteligente que revisar todo.

La idea: en vez de empezar por el principio, **mirar el elemento del medio**.
- Si es el que se busca, listo.
- Si el objetivo es **menor** que el del medio, tiene que estar en la mitad izquierda: se descarta la mitad derecha **entera**, sin mirarla.
- Si es **mayor**, se descarta la izquierda.

Y se repite sobre la mitad que quedó. En cada paso, **el problema se reduce a la mitad**. Es exactamente lo que hacés al buscar un apellido en una guía telefónica de papel, o una palabra en el diccionario: no arrancás por la A — abrís más o menos por la mitad y de ahí redirigís la búsqueda hacia adelante o hacia atrás.

```python
def busqueda_binaria(lista, objetivo):
    """Busca en una lista ORDENADA. Devuelve la posición, o -1 si no está."""
    izq = 0
    der = len(lista) - 1

    while izq <= der:
        medio = (izq + der) // 2

        if lista[medio] == objetivo:
            return medio
        elif lista[medio] < objetivo:
            izq = medio + 1        # descarto la mitad izquierda
        else:
            der = medio - 1        # descarto la mitad derecha

    return -1
```

> [!definition] Búsqueda binaria
> "The algorithm keeps track of the largest and smallest indices the target item might have in the array [...] The algorithm then calculates the index halfway between min and max [...] If the target is less than the array's value at mid, the algorithm resets max to search the left half of the array and starts over." *Fuente: [[Essential Algorithms A Practical Approach to Computer Algorithms]], cap. 7.*

Sobre una lista de 1.000 números buscando el 777 (verificado paso a paso en este entorno): **10 pasos**. La búsqueda lineal habría necesitado 778 comparaciones para el mismo dato.

### Análisis: por qué es logarítmica

En cada paso se descarta la mitad. Partiendo de `n` candidatos:

$$n \to \frac{n}{2} \to \frac{n}{4} \to \frac{n}{8} \to \dots \to 1$$

¿Cuántas veces se puede dividir `n` por 2 hasta llegar a 1? Exactamente $\log_2 n$ veces (qué es un logaritmo y por qué "deshace" una potencia, en [[04 - Funciones exponenciales y logaritmicas|Funciones exponenciales y logaritmicas]] de Matemática).

$$\text{Búsqueda binaria} = O(\log n)$$

> [!important] La demostración formal
> "Binary search in an ordered array with N keys uses no more than ⌊lg N⌋ + 1 compares for a search (successful or unsuccessful)." La prueba es una recurrencia simple: si $C(N)$ es el número de comparaciones necesarias, $C(N) \le C(\lfloor N/2 \rfloor) + 1$ — cada comparación reduce el problema a la mitad y suma un paso. Resolviendo esa recurrencia se llega directo a $\log_2 N$. *Fuente: [[Algorithms-4th-Edition-By-Robert Sedgewick and Kevin Wayne]], cap. 3.1 (Proposición B).*

Comparando el peor caso de ambas búsquedas a distintas escalas (verificado en este entorno):

| n | Lineal (peor caso) | Binaria (peor caso) |
|---:|---:|---:|
| 10 | 10 | 4 |
| 100 | 100 | 7 |
| 1.000 | 1.000 | 10 |
| 1.000.000 | 1.000.000 | 20 |
| 1.000.000.000 | 1.000.000.000 | 30 |

**Mirá la última fila.** Para encontrar algo entre **mil millones** de elementos, la búsqueda lineal necesita hasta mil millones de comparaciones, y la binaria necesita **30**. Treinta comparaciones. Es la razón por la que **los sistemas que buscan mucho mantienen índices ordenados** — un índice en una base de datos, en el fondo, existe para convertir búsquedas lineales en logarítmicas. Una cifra similar aparece en la bibliografía para estructuras más avanzadas (árboles balanceados): *"a tree that contains 1 billion keys is between 19 and 30 [...] we can guarantee to perform arbitrary search and insertion operations among 1 billion keys"* — el mismo orden de magnitud que la búsqueda binaria sobre un array. *Fuente: [[Algorithms-4th-Edition-By-Robert Sedgewick and Kevin Wayne]], cap. 3.3.*

> [!note] Recursión: la misma idea, escrita distinto
> La búsqueda binaria también se escribe recursivamente (caso base: rango vacío → no está, o coincidencia exacta → encontrado; si no, se llama de nuevo sobre la mitad que corresponda). Sedgewick incluye ambas versiones como ejemplo canónico de cuándo conviene usar recursión: la profundidad de la recursión es apenas $\log_2 n$ — para mil millones de elementos, **30 niveles**, muy lejos del límite de Python. Compará con Fibonacci recursivo sin memoizar, que se pasaba de rosca con n = 1.000 (ver [[recursion y memoizacion]]): **la recursión no es cara por ser recursión, es cara cuando el árbol de llamadas se ramifica** — acá no se ramifica, solo se achica.

### 1.3 La pregunta importante: ¿conviene ordenar primero?

Si la búsqueda binaria es tan superior, ¿por qué no ordenar siempre? Porque **ordenar cuesta**: ordenar es O(n log n) — bastante más caro que una sola búsqueda lineal, que es O(n).

| Escenario | Estrategia conveniente | Costo |
|---|---|---|
| Buscar **una vez** en datos desordenados | Búsqueda lineal | O(n) |
| Buscar **muchas veces** en los mismos datos | Ordenar una vez y usar binaria | O(n log n) + k·O(log n) |
| Los datos **ya vienen ordenados** | Binaria, siempre | O(log n) |
| Los datos **cambian todo el tiempo** | Lineal, o una estructura especializada | — |

**La regla:** ordenar es una inversión. Se amortiza si vas a buscar muchas veces — el mismo argumento contable de archivar comprobantes antes de que te los empiecen a pedir, no después.

Con 200.000 elementos desordenados (verificado en este entorno, contando operaciones según el modelo de costos de la clase: lineal = `n` por búsqueda, ordenar = `n·log₂n`, binaria = `log₂n` por búsqueda):

| Búsquedas (k) | Solo lineal | Ordenar + binaria | Conviene |
|---:|---:|---:|---|
| 1 | 200.000 | 3.521.946 | lineal |
| 10 | 2.000.000 | 3.522.104 | lineal |
| **18** | 3.600.000 | 3.522.245 | **ordenar** |
| 20 | 4.000.000 | 3.522.280 | ordenar |
| 100 | 20.000.000 | 3.523.689 | ordenar |
| 1.000 | 200.000.000 | 3.539.538 | ordenar |

Con 200.000 elementos, **a partir de la búsqueda número 18 ya conviene ordenar primero** — y de ahí en adelante la ventaja se agranda sin parar, porque el costo de ordenar (una sola vez) queda fijo mientras el costo de seguir buscando linealmente crece sin techo. Este mismo razonamiento —¿cuántas veces voy a consultar esto?— es el que decide si conviene crear un índice en una base de datos, o si conviene precalcular y guardar un reporte en vez de recalcularlo cada vez que alguien lo pide.

---

## 2. Ordenamiento: poner una lista en orden

### El problema

**Dada una lista, reorganizar sus elementos de menor a mayor** (o según el criterio que se elija). Ordenar habilita la búsqueda binaria de arriba, permite encontrar medianas y percentiles, agrupar valores iguales, detectar duplicados y calcular rankings — es de las operaciones más estudiadas de toda la computación.

Se ven los **tres algoritmos elementales** de la actividad. Los tres son **O(n²)** — ninguno es bueno para datos grandes — pero cada uno enseña algo distinto, y en la Sección 3 se comparan contra el ordenamiento real de Python, que sí es rápido. La operación básica de los tres es el **intercambio** ya visto en la [[01 - Introduccion a la programacion|clase 1]]: `lista[i], lista[j] = lista[j], lista[i]`.

### 2.1 Ordenamiento burbuja (*bubble sort*)

**Idea:** recorrer la lista comparando elementos adyacentes y, si están en el orden incorrecto, intercambiarlos. Repetir hasta que no haga falta ningún intercambio más. El nombre viene de que, en cada pasada, el elemento más grande "sube" hasta el final — como una burbuja.

```python
def burbuja(lista):
    """Ordena una copia de la lista con el método de la burbuja."""
    a = lista.copy()          # no modificamos la original
    n = len(a)

    for i in range(n):
        for j in range(n - 1 - i):        # el final ya está ordenado: no lo tocamos
            if a[j] > a[j + 1]:
                a[j], a[j + 1] = a[j + 1], a[j]
    return a
```

Con `datos = [64, 34, 25, 12, 22, 11, 90]`, pasada por pasada (verificado en este entorno):

| Pasada | Resultado parcial | Intercambios |
|---|---|---:|
| 1 | `[34, 25, 12, 22, 11, 64, 90]` | 5 |
| 2 | `[25, 12, 22, 11, 34, 64, 90]` | 4 |
| 3 | `[12, 22, 11, 25, 34, 64, 90]` | 3 |
| 4 | `[12, 11, 22, 25, 34, 64, 90]` | 1 |
| 5 | `[11, 12, 22, 25, 34, 64, 90]` | 1 |
| 6 | `[11, 12, 22, 25, 34, 64, 90]` | 0 → ya está ordenada |

Fijate el patrón: **después de la pasada `i`, los últimos `i` elementos ya están en su lugar definitivo** — por eso el bucle interno usa `range(n - 1 - i)`, para no revisar de nuevo lo que ya se sabe ordenado. A esta propiedad que se mantiene cierta pasada tras pasada se la llama el **invariante** del algoritmo, y es lo que garantiza matemáticamente que funcione.

> [!definition] Ordenamiento burbuja
> "Bubblesort uses the fairly obvious fact that, if an array is not sorted, it must contain two adjacent elements that are out of order. The algorithm repeatedly passes through the array, swapping items that are out of order, until it can't find any more swaps [...] The fact that item [...] seems to slowly bubble up to its correct position gives the bubblesort algorithm its name." *Fuente: [[Essential Algorithms A Practical Approach to Computer Algorithms]], cap. 6.*

**Análisis:** peor caso (lista al revés) y caso promedio, ambos con las dos vueltas completas: `n(n-1)/2` comparaciones → **O(n²)**. El mejor caso (lista ya ordenada) también es O(n²) en esta versión, porque igual da todas las vueltas — pero eso se puede arreglar:

```python
def burbuja_optimizada(lista):
    """Burbuja con detección temprana: corta si una pasada no hace intercambios."""
    a = lista.copy()
    n = len(a)
    for i in range(n):
        hubo_intercambio = False
        for j in range(n - 1 - i):
            if a[j] > a[j + 1]:
                a[j], a[j + 1] = a[j + 1], a[j]
                hubo_intercambio = True
        if not hubo_intercambio:
            break              # ya está ordenada
    return a
```

Ordenando una lista de 3.000 elementos que **ya estaba ordenada** (medido en este entorno): la burbuja simple tardó 80,3 ms; la optimizada, 0,06 ms — **una mejora de unas 1.250 veces**. Con esa única línea de más, el mejor caso pasó de O(n²) a O(n). El peor caso sigue siendo O(n²), pero en datos parcialmente ordenados —muy comunes en la práctica— la diferencia es enorme.

> [!warning] Bubble sort tiene mala fama, y no todos los libros coinciden en por qué
> Vale la pena marcar algo que aparece al comparar la bibliografía: **Sedgewick & Wayne no mencionan la burbuja ni una sola vez** en las más de 64.000 líneas de su libro — de los tres ordenamientos elementales de esta clase, solo desarrollan selección e inserción, y consideran que la burbuja no merece espacio ni para descartarla explícitamente. *Essential Algorithms*, en cambio, sí la desarrolla en profundidad y hasta la **defiende**: "bubblesort is fairly slow but may provide acceptable performance for small lists [...] It is also sometimes faster than more complicated algorithms for very small lists (five or so items)" — y describe optimizaciones adicionales (alternar la dirección de las pasadas, evitar escrituras redundantes) con datos concretos: sobre 10.000 elementos, 2,50 segundos sin mejoras contra 0,69 segundos con mejoras. *Fuente: [[Essential Algorithms A Practical Approach to Computer Algorithms]], cap. 6.* No es que un libro tenga razón y el otro no — es un buen recordatorio de que hasta la bibliografía técnica tiene preferencias pedagógicas, y de que "alternar la dirección de las pasadas" es, ni más ni menos, la idea detrás del **cocktail sort** de la actividad de esta clase.

**Lección general:** el análisis de peor caso es importante, pero no es toda la historia. Conocer la distribución real de los propios datos permite optimizaciones que el peor caso, por definición, no puede anticipar.

### 2.2 Ordenamiento por selección (*selection sort*)

**Idea:** buscar el mínimo de toda la lista y ponerlo primero. Después buscar el mínimo de lo que queda y ponerlo segundo. Y así, sucesivamente — como armar un mazo ordenado de menor a mayor sacando siempre la carta más chica que queda en la mano.

```python
def seleccion(lista):
    """Ordena buscando en cada paso el mínimo del resto."""
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

Sobre los mismos datos, paso por paso (verificado en este entorno): en el paso 1 encuentra el mínimo (11) y lo manda a la posición 0; en el paso 2, el mínimo del resto (12) a la posición 1; y así hasta ordenar todo en 6 pasos.

> [!definition] Ordenamiento por selección
> "The basic idea is to search the input list for the largest item it contains and then add it to the end of a growing sorted list. Alternatively, the algorithm can find the smallest item and move it to the beginning of the growing list." *Fuente: [[Essential Algorithms A Practical Approach to Computer Algorithms]], cap. 6.*

**Análisis:** siempre hace `n(n-1)/2` comparaciones, **sin importar cómo vengan los datos** — peor caso, caso promedio y mejor caso son los tres O(n²). No se puede optimizar como la burbuja.

> [!important] Dos propiedades "firma" del selection sort
> "Running time is insensitive to input [...] Data movement is minimal": tarda exactamente lo mismo con una lista ya ordenada, una con todas las claves iguales o una al azar — a diferencia de inserción, cuyo tiempo sí depende del orden de entrada. Y hace como máximo `n − 1` **intercambios** en total, muchos menos que la burbuja. Si mover un elemento fuera muy caro —por ejemplo, si cada elemento fuera un registro contable enorme en vez de un número— la selección resultaría preferible por esa sola razón. *Fuente: [[Algorithms-4th-Edition-By-Robert Sedgewick and Kevin Wayne]], cap. 2.1 (Proposición A).*

> [!tip] Dos algoritmos con la misma complejidad pueden tener perfiles muy distintos
> Big O captura **el crecimiento**, no todos los detalles del costo. Burbuja y selección son ambos O(n²), pero uno hace muchos intercambios y el otro casi ninguno — una diferencia real que la notación Big O, a propósito, no distingue.

### 2.3 Ordenamiento por inserción (*insertion sort*)

**Idea:** como ordenar cartas en la mano. Se toma una carta nueva y se la inserta en el lugar que le corresponde entre las que ya están ordenadas.

```python
def insercion(lista):
    """Ordena insertando cada elemento en su lugar dentro de la parte ya ordenada."""
    a = lista.copy()

    for i in range(1, len(a)):
        actual = a[i]
        j = i - 1
        # correr hacia la derecha todo lo que sea mayor que "actual"
        while j >= 0 and a[j] > actual:
            a[j + 1] = a[j]
            j -= 1
        a[j + 1] = actual      # acá va
    return a
```

> [!definition] Ordenamiento por inserción
> "The basic idea is to take an item from the input list and insert it into the proper position in the sorted output list (which initially starts empty)." *Fuente: [[Essential Algorithms A Practical Approach to Computer Algorithms]], cap. 6.*

**Análisis:** peor caso (lista al revés) — cada elemento tiene que correrse hasta el principio → **O(n²)**; caso promedio → **O(n²)**; mejor caso (ya ordenada) — el `while` nunca entra → **O(n)**.

> [!important] Por qué es "el mejor de los tres" en la práctica
> Insertion sort es sensible al orden de entrada de una forma que se puede medir con precisión: la cantidad de intercambios que hace es exactamente igual a la cantidad de **inversiones** de la lista (pares de elementos que están fuera de orden entre sí), y el número de comparaciones está entre esa misma cantidad y esa cantidad más `n − 1`. Una lista **parcialmente ordenada** —cada elemento no muy lejos de su posición final, algo extremadamente común con datos reales (un archivo que se actualiza todos los días, una tabla que ya viene casi ordenada de otra fuente)— tiene pocas inversiones, así que insertion sort la ordena casi al costo de recorrerla una sola vez, en vez de compararla contra todo el resto. *Fuente: [[Algorithms-4th-Edition-By-Robert Sedgewick and Kevin Wayne]], cap. 2.1 (Proposición C).*

Guardá ese dato — es exactamente el motivo por el que insertion sort aparece **dentro** del algoritmo que usa Python de verdad. Se ve en la sección siguiente.

Verificación final: los tres algoritmos (más `sorted()` de Python) dan siempre el mismo resultado sobre una lista de 50 números al azar (verificado en este entorno: coinciden los cuatro).

---

## 3. Comparación empírica y el ordenamiento real de Python

### 3.1 Midiendo los tres algoritmos

La teoría dice que los tres son O(n²), con distinto comportamiento en el mejor caso. Se mide sobre tres tipos de entrada distintos, con `n = 2.000` (medido en este entorno, tiempo mediano de 3 repeticiones):

| Algoritmo | Aleatoria | Ya ordenada | Orden invertido |
|---|---:|---:|---:|
| Burbuja | 65,9 ms | 35,5 ms | 76,2 ms |
| Burbuja optimizada | 67,5 ms | **0,04 ms** | 78,9 ms |
| Selección | 31,5 ms | 29,2 ms | 32,0 ms |
| Inserción | 35,4 ms | **0,09 ms** | 67,1 ms |
| `sorted()` de Python | **0,08 ms** | **0,01 ms** | **0,01 ms** |

**Cuatro hallazgos, leyendo esa tabla con cuidado:**

1. **La burbuja optimizada y la inserción son casi instantáneas con datos ya ordenados** — su mejor caso es O(n) y se nota a simple vista: milésimas de milisegundo contra decenas de milisegundos.
2. **La selección tarda prácticamente lo mismo en los tres casos.** No le importa cómo vengan los datos — siempre hace la misma cantidad de comparaciones, tal como predice su análisis de peor/mejor caso idénticos.
3. **La burbuja simple mejora un poco con datos ordenados, pero no de forma dramática** — hace **todas** las comparaciones igual, solo se ahorra los intercambios. Sigue siendo O(n²). La diferencia real está en la versión optimizada, que sí **corta** de verdad.
4. **`sorted()` de Python es cientos de veces más rápido que todos**, en los tres casos.

### 3.2 ¿Por qué `sorted()` es tan rápido?

Python usa **Timsort**, un algoritmo diseñado por Tim Peters en 2002 específicamente para CPython. Hoy también lo usan Java, Android, Swift y V8 (el motor de JavaScript de Chrome).

Es un algoritmo **híbrido** que combina dos ideas ya vistas en esta clase:
- **Mergesort**, que garantiza O(n log n) siempre, sin importar cómo vengan los datos.
- **Ordenamiento por inserción**, que —como se vio arriba— es muy rápido en tramos chicos y en datos casi ordenados.

Su truco es que **detecta tramos ya ordenados** en los datos reales (los llama *runs*) y los aprovecha en vez de rehacer el trabajo desde cero. Por eso, con datos parcialmente ordenados —lo habitual en el mundo real: registros con fecha, datos que ya vienen de una fuente indexada, planillas que se actualizan agregando filas al final— es muchísimo más rápido que su peor caso teórico.

> [!warning] Una fuente de la bibliografía tiene un dato desactualizado sobre esto
> Vale la pena señalarlo porque es justo el tipo de cosa que conviene poder detectar leyendo bibliografía técnica: *Data Structures and Algorithms with Python* afirma que "the built-in sort [de Python], which is quicksort implemented in C, runs the fastest" — pero **esto es incorrecto**: CPython usa Timsort desde la versión 2.3 (2003), no quicksort. Es un dato viejo o mal verificado en ese libro puntual, no una verdad alternativa — con `sorted()`/`.sort()` de Python, el algoritmo real es Timsort. *Fuente del error señalado: [[Data Structures and Algorithms with Python]], cap. 9.*

| | Mejor | Promedio | Peor | ¿Estable? |
|---|---|---|---|---|
| Burbuja | O(n)* | O(n²) | O(n²) | Sí |
| Selección | O(n²) | O(n²) | O(n²) | No |
| Inserción | O(n) | O(n²) | O(n²) | Sí |
| **Timsort (Python)** | **O(n)** | **O(n log n)** | **O(n log n)** | **Sí** |

\* solo la versión optimizada. Qué significa "estable" se desarrolla en [[estabilidad de un ordenamiento]] — importa, y mucho, en la Sección 4.

> [!tip] Por qué Timsort no es casualidad
> No es que "los buenos ordenamientos resulten ser O(n log n)" por buena suerte del diseño: se puede demostrar matemáticamente que **ningún** algoritmo que ordene comparando elementos de a pares puede hacerlo, en el peor caso, con menos de aproximadamente `n log n` comparaciones — ya desarrollado con la demostración completa en [[notación Big O y familias de complejidad]]. Timsort, mergesort y quicksort no son "buenos", son **óptimos** dentro de lo matemáticamente posible.

### 3.3 La ventaja se agranda con el volumen

Comparando inserción contra `sorted()` a medida que crece `n` (medido en este entorno):

| n | Inserción (ms) | `sorted()` (ms) | Razón |
|---:|---:|---:|---:|
| 500 | 2,21 | 0,014 | 160× |
| 1.000 | 8,60 | 0,038 | 225× |
| 2.000 | 34,93 | 0,086 | 405× |
| 4.000 | 157,60 | 0,202 | 780× |

Al duplicar `n`, el tiempo de inserción se **cuadruplica** — la firma de O(n²) ya vista en la clase pasada (ver el "doubling ratio" de [[notación Big O y familias de complejidad]]). El de `sorted()` apenas se duplica: es O(n log n). Por eso la última columna no para de crecer: **la ventaja de Timsort no es constante, se agranda con el volumen de datos.**

![[Ordenamientos vs sorted - tiempo de ejecucion.png]]

En el panel de escala lineal (izquierda), las tres curvas cuadráticas se doblan hacia arriba y `sorted()` queda pegado al eje, casi indistinguible de cero. El panel logarítmico (derecha) permite ver los cuatro a la vez: las tres curvas O(n²) quedan casi paralelas entre sí —misma complejidad, distintas constantes— y `sorted()` corre muy por debajo, con una pendiente claramente menor.

> [!important] Conclusión práctica
> En un trabajo real, usá siempre `sorted()` o `.sort()`. Implementar un ordenamiento a mano tiene sentido para **aprender** cómo funciona por dentro, o en el caso puntual de necesitar un criterio muy específico que la biblioteca no cubra. Pero ahora sabés **por qué** conviene, y podés reconocer cuándo un código propio esconde un O(n²) que podría evitarse.

---

## 4. Ordenar datos reales

Hasta acá se ordenaron números sueltos. En la práctica se ordenan **registros** —filas de una planilla, en el fondo— por alguno de sus campos: la fecha de un comprobante, el monto de una factura, el nombre de un cliente. Python resuelve esto con el parámetro `key`.

### 4.1 El parámetro `key`

Se trabaja con el dataset real de **pingüinos** (Palmer Penguins, 342 registros con especie, isla, sexo y masa corporal — descargado y verificado en este entorno):

```python
por_masa = sorted(pinguinos, key=lambda p: p["masa_g"])
```

`lambda p: p["masa_g"]` es una **función anónima**: una función chiquita, escrita en el lugar, sin nombre propio — desarrollada en profundidad en [[funciones, parametros y alcance]]. Equivale a escribir `def obtener_masa(p): return p["masa_g"]` y pasar `key=obtener_masa`, pero sin el paso extra de ponerle nombre a algo que se usa una sola vez. `sorted()` llama a esa función una vez por cada elemento, y ordena según el valor que devuelve — no según el diccionario completo.

> [!tip] Otra forma de dar la misma clave: una función que ya existe
> No siempre hace falta un `lambda`. Si la clave de orden es directamente el resultado de una función ya definida (incluso una incorporada al lenguaje), se la puede pasar tal cual: `sorted(palabras, key=len)` ordena strings por longitud, usando la función `len` sin necesidad de envolverla en `lambda p: len(p)`. *Fuente: [[Python-for-Data-Analysis]], cap. 3.*

Con los pingüinos ordenados por masa (verificado en este entorno, 342 registros reales): los 5 más livianos son todos Adelie y Chinstrap entre 2.700 y 2.900 g; los 5 más pesados son todos Gentoo entre 5.950 y 6.300 g — la propia ordenación ya revela, sin ningún gráfico, que Gentoo es sistemáticamente la especie más pesada.

### 4.2 Orden descendente y top-k

```python
mas_pesados = sorted(pinguinos, key=lambda p: p["masa_g"], reverse=True)[:10]
```

`reverse=True` invierte el sentido del orden completo. Combinado con `[:10]` (slicing, ver [[indexado y slicing]]), da el top 10 — que, verificado sobre los datos reales, son 10 pingüinos Gentoo macho de la isla Biscoe, entre 5.800 y 6.300 g.

> [!info] A futuro: el top-k sin ordenar todo
> Para obtener el top 10 no hace falta ordenar los 342 registros completos — existe `heapq.nlargest(10, ...)` en la biblioteca estándar de Python, que es O(n log k) en vez de O(n log n). Con 342 elementos la diferencia es invisible; con 10 millones, no lo es. Es el mismo razonamiento de "cuánto se usa esto" que decidió, en la Sección 1.3, si convenía ordenar antes de buscar.

### 4.3 Ordenar por varias claves

Se pasa una **tupla** como clave: Python compara primero el primer elemento de la tupla, y solo si empatan pasa a comparar el segundo. Es, ni más ni menos, el "ordenar por columna A y, dentro de cada A, por columna B" de cualquier planilla de cálculo.

```python
# Primero por especie (alfabético), después por masa descendente dentro de cada especie
ordenado = sorted(pinguinos, key=lambda p: (p["especie"], -p["masa_g"]))
```

El truco de `-p["masa_g"]` invierte el orden solo de ese campo, aprovechando que invertir el signo de un número invierte su orden — funciona con números; para texto hace falta otro recurso (ver la nota de estabilidad, abajo).

### 4.4 Estabilidad: por qué se puede ordenar "en etapas"

```python
paso1 = sorted(pinguinos, key=lambda p: p["masa_g"], reverse=True)
paso2 = sorted(paso1, key=lambda p: p["especie"])
```

Ordenar primero por masa descendente y **después** por especie da exactamente el mismo resultado que ordenar de una sola vez con la tupla `(especie, -masa)` de arriba (verificado en este entorno: ambos resultados coinciden dato por dato). Eso **solo** funciona porque `sorted()` de Python es **estable** — un ordenamiento estable no reordena al azar los elementos que ya estaban empatados en el criterio anterior. El desarrollo completo de por qué esto importa está en [[estabilidad de un ordenamiento]].

### 4.5 Buscar en datos reales con búsqueda binaria

Cerrando el círculo con la Sección 1: una vez que los datos están ordenados, se puede buscar por valor con búsqueda binaria — la biblioteca estándar de Python ya la trae hecha, en el módulo `bisect`.

```python
import bisect

masas = sorted(p["masa_g"] for p in pinguinos)

def cuantos_pesan_menos_de(umbral):
    """Cantidad de pingüinos con masa menor al umbral. O(log n)."""
    return bisect.bisect_left(masas, umbral)
```

Sobre los 342 pingüinos reales (verificado en este entorno):

| Umbral | Pingüinos por debajo |
|---:|---:|
| 3.000 g | 9 (2,6 %) |
| 3.500 g | 71 (20,8 %) |
| 4.000 g | 165 (48,2 %) |
| 4.500 g | 224 (65,5 %) |
| 5.000 g | 275 (80,4 %) |
| 5.500 g | 309 (90,4 %) |

Ese cálculo es, en el fondo, un **percentil** — y se obtuvo en O(log n), no revisando los 342 registros uno por uno, porque los datos ya estaban ordenados. Es la misma inversión de la Sección 1.3: ordenar una vez para responder muchas preguntas rápido, en vez de recorrer todo cada vez que se pregunta algo.

---

## 5. Cierre

### Lo que vimos hoy

**Búsqueda**
- **Lineal**: O(n), no exige nada, funciona siempre.
- **Binaria**: O(log n), exige datos ordenados — encuentra un elemento entre mil millones en 30 comparaciones.
- **La inversión de ordenar**: con 200.000 elementos, a partir de ~18 búsquedas ya conviene ordenar primero. Es el razonamiento detrás de un índice de base de datos.

**Ordenamiento**
- **Burbuja**: intercambia adyacentes. O(n²), pero con detección temprana su mejor caso es O(n).
- **Selección**: busca el mínimo. O(n²) siempre, pero hace pocos intercambios.
- **Inserción**: como ordenar cartas. O(n²) en el peor caso, O(n) en el mejor — el más útil de los tres elementales en la práctica, gracias a las inversiones.
- **Timsort**: el de Python. Híbrido de mergesort e inserción, O(n log n) garantizado, detecta tramos ya ordenados. Cientos de veces más rápido que los elementales, y la ventaja crece con el volumen.

**En datos reales**
- `sorted(..., key=lambda p: p["campo"])`, orden descendente con `reverse=True`, top-k.
- Ordenar por varias claves con una tupla, y por qué la **estabilidad** permite hacerlo también en etapas separadas.
- `bisect` para búsqueda binaria de biblioteca estándar — percentiles en O(log n).

### Tres ideas para llevarse

1. **Ordenar es una inversión.** Cuesta O(n log n) una vez, y después cada búsqueda sale O(log n) en vez de O(n). Se amortiza si se consulta muchas veces — el mismo cálculo que decide si conviene indexar una tabla.
2. **Misma complejidad no significa mismo comportamiento.** Los tres ordenamientos elementales son O(n²) y se comportaron de forma muy distinta según cómo venían los datos — y hasta la propia bibliografía discrepa en si vale la pena enseñar la burbuja.
3. **Usá la biblioteca.** Estos algoritmos se implementaron para entenderlos, no para usarlos en un trabajo real. Pero ahora se puede reconocer un O(n²) escondido en código propio, que es lo que realmente importa.

---

## Conceptos para desarrollar en notas aparte
- [[búsqueda lineal y búsqueda binaria]]
- [[ordenamiento burbuja, selección e inserción]]
- [[estabilidad de un ordenamiento]]
- [[ordenar con key, lambda y criterios múltiples]]

Siete casos adicionales que aplican estos conceptos con datos verificados, tomados de la bibliografía de Algoritmos y Python: [[04.1 - Casos aplicados]].

## Preguntas de repaso
1. ¿Por qué la búsqueda lineal es O(n) mientras que la búsqueda binaria es O(log n), y qué condición tiene que cumplir la lista para poder usar la segunda?
2. Con 200.000 elementos, ordenar primero conviene recién a partir de unas 18 búsquedas. ¿Por qué el umbral es un número finito y no "siempre conviene ordenar" o "nunca conviene ordenar"? ¿Qué le pasaría a ese umbral si `n` fuera mucho más chico, digamos 200 elementos?
3. Burbuja, selección e inserción son los tres O(n²) en el peor caso. Elegí dos de los tres y explicá una diferencia concreta en su comportamiento que la notación Big O, por sí sola, no distingue.
4. ¿Por qué insertion sort es rápido en datos "casi ordenados" y selection sort no, a pesar de tener la misma complejidad de peor caso?
5. ¿Qué combina Timsort de mergesort y de insertion sort, y por qué esa combinación lo hace más rápido que cualquiera de los dos por separado en datos parcialmente ordenados?
6. Si `sorted()` no fuera estable, ¿qué dejaría de funcionar del truco de "ordenar primero por masa y después por especie" de la Sección 4.4?

## Preguntas que me quedaron
-
-

## Para la próxima clase
**Clase 5 — NumPy, Pandas y análisis exploratorio.** La última clase. Se ven las herramientas con las que realmente se trabaja: NumPy para cálculo vectorizado y Pandas para manipulación de datos tabulares, más visualización con Matplotlib y Seaborn. Vas a reencontrarte con todo lo de las cuatro clases anteriores: el `group by` escrito a mano en la clase 1 va a ser una línea, el ordenamiento de hoy va a ser `sort_values()`, y se va a medir por qué vectorizar es tan rápido. Además se presenta el trabajo final integrador.

## Actividad
Está en **`Actividad_Clase4.ipynb`** (Moodle): contar comparaciones de una búsqueda binaria instrumentada y encontrar la primera aparición de un valor repetido; calcular a partir de qué cantidad de búsquedas conviene ordenar; implementar el **cocktail sort** (la variante bidireccional de la burbuja que resuelve el problema de la "tortuga" — un elemento chico que tarda muchas pasadas en llegar a su lugar); comparar experimentalmente cuatro algoritmos con gráficos por tipo de entrada; y aplicar todo sobre el dataset de propinas (Tips) con `bisect` para calcular percentiles. Se entrega antes del viernes 28 de agosto.
