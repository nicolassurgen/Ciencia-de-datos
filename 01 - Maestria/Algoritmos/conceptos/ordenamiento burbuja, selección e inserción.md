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

### El "diálogo interno" del algoritmo, línea por línea

Hay **dos** bucles anidados, y conviene separar bien qué hace cada uno. El de afuera (`i`) cuenta **pasadas**: cuántas veces se recorre la lista de punta a punta. El de adentro (`j`) es el que hace el trabajo real en cada pasada: recorre posiciones adyacentes, y en cada una se pregunta *"¿el de acá (`a[j]`) es más grande que el de al lado (`a[j+1]`)? Si sí, los cambio de lugar."* — nada más complejo que eso, repetido una y otra vez.

Con `[64, 34, 25, 12, 22, 11, 90]`, así se ve la **primera pasada** (`i=0`) por dentro, vuelta por vuelta del `j`:

```
j=0: ¿a[0]=64 > a[1]=34? Sí.  Intercambio.  Lista: [34, 64, 25, 12, 22, 11, 90]
j=1: ¿a[1]=64 > a[2]=25? Sí.  Intercambio.  Lista: [34, 25, 64, 12, 22, 11, 90]
j=2: ¿a[2]=64 > a[3]=12? Sí.  Intercambio.  Lista: [34, 25, 12, 64, 22, 11, 90]
j=3: ¿a[3]=64 > a[4]=22? Sí.  Intercambio.  Lista: [34, 25, 12, 22, 64, 11, 90]
j=4: ¿a[4]=64 > a[5]=11? Sí.  Intercambio.  Lista: [34, 25, 12, 22, 11, 64, 90]
j=5: ¿a[5]=64 > a[6]=90? No. Sin cambios.   Lista: [34, 25, 12, 22, 11, 64, 90]
```

Mirá lo que pasó con el 64: entró a la pasada en la posición 0, y **cada vez que gana una comparación se muda un lugar a la derecha junto con el `j`** — no porque el algoritmo "decida" moverlo, sino porque es, literalmente, lo que hace `a[j], a[j+1] = a[j+1], a[j]` cuando `a[j]` es el más grande de los dos: el más grande siempre termina en la posición `j+1`, así que en la próxima vuelta (`j+1`) ese mismo valor vuelve a ser el candidato a comparar. Recién se "suelta" cuando se topa con algo todavía más grande que él (el 90) — ahí pierde la comparación y se queda quieto por el resto de la pasada. Ese desplazamiento progresivo, comparación tras comparación, es literalmente la "burbuja" que le da nombre al algoritmo.

Una vez que termina la pasada `i=0` (el `j` llegó al final), arranca la pasada `i=1` — otra vez `j` desde 0, pero ahora hasta `n-1-1` en vez de `n-1-0`, porque la posición 6 (donde quedó el 90) ya se sabe que está bien ubicada y no hace falta revisarla de nuevo. Así, pasada tras pasada, el rango que recorre `j` se va achicando por la derecha.

### Tabla resumen: cada comparación de la primera pasada

Ordenando `[64, 34, 25, 12, 22, 11, 90]`, mirando **cada comparación individual** de la primera pasada (verificado en este entorno):

| Comparación | Par comparado | ¿Fuera de orden? | Acción | Lista después de esta comparación |
|---:|---|:---:|---|---|
| 1 | (64, 34) | Sí | Intercambio | `[34, 64, 25, 12, 22, 11, 90]` |
| 2 | (64, 25) | Sí | Intercambio | `[34, 25, 64, 12, 22, 11, 90]` |
| 3 | (64, 12) | Sí | Intercambio | `[34, 25, 12, 64, 22, 11, 90]` |
| 4 | (64, 22) | Sí | Intercambio | `[34, 25, 12, 22, 64, 11, 90]` |
| 5 | (64, 11) | Sí | Intercambio | `[34, 25, 12, 22, 11, 64, 90]` |
| 6 | (64, 90) | No | Sin cambios | `[34, 25, 12, 22, 11, 64, 90]` |

El 64 (el valor con el que arrancó la pasada) fue "ganando" cada comparación contra su vecino de la derecha y **avanzando una posición cada vez**, hasta toparse con el 90 —más grande que él— y quedarse ahí. Es, literalmente, el fenómeno que le da nombre al algoritmo: en cada pasada, el elemento más grande "burbujea" hacia el final, una posición por comparación.

Repitiendo esto pasada tras pasada, hasta que una pasada completa no encuentre nada para intercambiar:

| Pasada | Resultado parcial | Intercambios en esta pasada |
|---:|---|---:|
| 1 | `[34, 25, 12, 22, 11, 64, 90]` | 5 |
| 2 | `[25, 12, 22, 11, 34, 64, 90]` | 4 |
| 3 | `[12, 22, 11, 25, 34, 64, 90]` | 3 |
| 4 | `[12, 11, 22, 25, 34, 64, 90]` | 1 |
| 5 | `[11, 12, 22, 25, 34, 64, 90]` | 1 |
| 6 | `[11, 12, 22, 25, 34, 64, 90]` | 0 → ya está ordenada, corta acá |

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

### El "diálogo interno" del algoritmo, línea por línea

También hay dos bucles anidados, pero cumplen un rol distinto al de la burbuja. El de afuera (`i`) recorre, una por una, **las posiciones que hay que llenar**: primero la 0, después la 1, y así. El de adentro (`j`) no compara vecinos — recorre **todo lo que falta** buscando el mínimo, guardando en `pos_min` la mejor posición vista hasta el momento, y solo al final (fuera del `for` de adentro) hace **un único intercambio** para poner ese mínimo en su lugar. Esa es la diferencia estructural con la burbuja: la burbuja intercambia **muchas veces** dentro del bucle de adentro; selección intercambia **una sola vez**, después de que el bucle de adentro ya terminó de decidir.

Con `[64, 34, 25, 12, 22, 11, 90]`, así se ve el `i=0` por dentro:

```
i=0: pos_min arranca en 0 (el candidato es a[0]=64, todavía no se comparó con nadie)
  j=1: ¿a[1]=34 < a[pos_min]=64? Sí. pos_min pasa a ser 1.
  j=2: ¿a[2]=25 < a[pos_min]=34? Sí. pos_min pasa a ser 2.
  j=3: ¿a[3]=12 < a[pos_min]=25? Sí. pos_min pasa a ser 3.
  j=4: ¿a[4]=22 < a[pos_min]=12? No. pos_min sigue siendo 3.
  j=5: ¿a[5]=11 < a[pos_min]=12? Sí. pos_min pasa a ser 5.
  j=6: ¿a[6]=90 < a[pos_min]=11? No. pos_min sigue siendo 5.
-- el for de adentro terminó: pos_min quedó en 5 (el valor 11) --
  intercambio único: a[0] y a[5] cambian de lugar
  Lista: [11, 34, 25, 12, 22, 64, 90]
```

Notá algo importante: durante **todo** el recorrido del `j`, la lista **no se tocó ni una vez** — `pos_min` es apenas un número que se va actualizando en la cabeza del algoritmo, ningún elemento cambia de lugar hasta el intercambio final. Es exactamente lo opuesto de la burbuja, que intercambia (potencialmente) en cada vuelta del `j`. Por eso selección hace, como mucho, un intercambio por pasada — `n-1` en total —, mientras que la burbuja puede hacer muchísimos más.

Sobre la misma lista, así se encuentra el mínimo en el **primer** paso — recorriendo todo, quedándose siempre con el candidato más chico visto hasta el momento (verificado en este entorno):

| Se compara contra | Valor | ¿Mejora al mínimo actual? | Mínimo actual tras esta comparación |
|---|---:|:---:|---:|
| (candidato inicial) | 64 | — | 64 |
| 34 | 34 | Sí | 34 |
| 25 | 25 | Sí | 25 |
| 12 | 12 | Sí | 12 |
| 22 | 22 | No (22 > 12) | 12 |
| 11 | 11 | Sí | 11 |
| 90 | 90 | No (90 > 11) | 11 |

El mínimo de toda la lista es **11**, y recién se lo confirma después de comparar contra **todos** los demás elementos — a diferencia de la burbuja, acá no hay forma de "cortar antes": hay que revisar el resto completo para estar seguro.

Tras ese intercambio, la lista queda `[11, 34, 25, 12, 22, 64, 90]` — el 11 ya en su lugar (posición 0), y el resto (posiciones 1 a 6) todavía sin tocar. El **paso 2** repite exactamente el mismo mecanismo, pero ahora buscando el mínimo solamente entre lo que queda:

| Se compara contra | Valor | ¿Mejora al mínimo actual? | Mínimo actual tras esta comparación |
|---|---:|:---:|---:|
| (candidato inicial, posición 1) | 34 | — | 34 |
| 25 | 25 | Sí | 25 |
| 12 | 12 | Sí | 12 |
| 22 | 22 | No (22 > 12) | 12 |
| 64 | 64 | No (64 > 12) | 12 |
| 90 | 90 | No (90 > 12) | 12 |

El mínimo de lo que quedaba es **12**, en la posición 3 — se lo intercambia con la posición 1 (la primera todavía sin resolver), y la lista pasa a `[11, 12, 25, 34, 22, 64, 90]`. Este mismo procedimiento —recorrer todo lo que falta, quedarse con el más chico, intercambiarlo al frente— se repite, cada vez sobre una porción más chica de la lista, hasta terminar. Los 6 pasos completos, con el resultado de cada uno:

| Paso | Mínimo encontrado | Posición original del mínimo | Lista después del intercambio |
|---:|---:|---:|---|
| 1 | 11 | 5 | `[11, 34, 25, 12, 22, 64, 90]` |
| 2 | 12 | 3 | `[11, 12, 25, 34, 22, 64, 90]` |
| 3 | 22 | 4 | `[11, 12, 22, 34, 25, 64, 90]` |
| 4 | 25 | 4 | `[11, 12, 22, 25, 34, 64, 90]` |
| 5 | 34 | 4 | `[11, 12, 22, 25, 34, 64, 90]` |
| 6 | 64 | 5 | `[11, 12, 22, 25, 34, 64, 90]` |

Fijate que los pasos 4 y 5 "intercambian" un elemento consigo mismo (ya estaba en su lugar) — el algoritmo no tiene forma de saberlo de antemano, así que igual busca el mínimo en todo el resto. Es la contracara exacta de la propiedad de "insensible al orden de entrada": no hay atajo posible, encuentre o no algo para mover.

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

### El "diálogo interno" del algoritmo, línea por línea

Acá el bucle de afuera (`i`) recorre los elementos **de izquierda a derecha**, uno por uno, y en cada vuelta guarda ese elemento en `actual` — es "la carta que se acaba de levantar del mazo". El bucle de adentro no es un `for` sino un `while`, y **mira hacia atrás**, no hacia adelante: empieza en `j = i - 1` (el vecino inmediato a la izquierda) y se pregunta, vuelta a vuelta, *"¿el de acá (`a[j]`) es más grande que `actual`? Si sí, no es su lugar — lo corro un lugar a la derecha y sigo mirando más atrás. Si no, ya encontré dónde va `actual`."*

Con `[64, 34, 25, 12, 22, 11, 90]`, así se ve `i=1` (la primera inserción, la más simple posible):

```
i=1: actual = a[1] = 34.  j arranca en i-1 = 0.
  j=0: ¿a[0]=64 > actual=34? Sí.  Corro el 64 a la posición 1.  j pasa a -1.
-- el while termina porque j=-1 (ya no hay más para comparar a la izquierda) --
  a[0] = actual (34)
  Lista: [34, 64, 25, 12, 22, 11, 90]
```

Y así se ve `i=4` (insertar el 22, un caso con más recorrido hacia atrás):

```
i=4: actual = a[4] = 22.  j arranca en i-1 = 3.  Lista antes: [12, 25, 34, 64, 22, 11, 90]
  j=3: ¿a[3]=64 > actual=22? Sí.  Corro el 64 a la posición 4.  j pasa a 2.
  j=2: ¿a[2]=34 > actual=22? Sí.  Corro el 34 a la posición 3.  j pasa a 1.
  j=1: ¿a[1]=25 > actual=22? Sí.  Corro el 25 a la posición 2.  j pasa a 0.
  j=0: ¿a[0]=12 > actual=22? No. El while para acá (j se queda en 0).
  a[1] = actual (22)   <- se inserta en j+1 = 1
  Lista: [12, 22, 25, 34, 64, 11, 90]
```

La diferencia con la burbuja y la selección salta a la vista: acá el bucle de adentro **no recorre toda la lista** ni compara contra un mínimo acumulado — recorre **solo hacia atrás, y solo hasta donde haga falta**, deteniéndose apenas encuentra un valor que ya es menor que `actual`. Por eso, cuando `actual` ya es más grande que todo lo que está a su izquierda (como el 90 al final), el `while` ni siquiera entra una vez: es el mecanismo exacto detrás de que inserción sea O(n) en el mejor caso.

Sobre la misma lista, insertando un elemento a la vez en la parte ya ordenada, el resultado de cada paso (verificado en este entorno):

| Elemento a insertar | Corrimientos necesarios | Posición final | Lista después de este paso |
|---:|---:|---:|---|
| 34 | 1 | 0 | `[34, 64, 25, 12, 22, 11, 90]` |
| 25 | 2 | 0 | `[25, 34, 64, 12, 22, 11, 90]` |
| 12 | 3 | 0 | `[12, 25, 34, 64, 22, 11, 90]` |
| 22 | 3 | 1 | `[12, 22, 25, 34, 64, 11, 90]` |
| 11 | 5 | 0 | `[11, 12, 22, 25, 34, 64, 90]` |
| 90 | 0 | 6 | `[11, 12, 22, 25, 34, 64, 90]` |

¿De dónde salen exactamente esos "3 corrimientos" al insertar el 22? Es la parte que la tabla resume en un número — acá está desarmada, comparación por comparación. Justo antes de este paso, la lista es `[12, 25, 34, 64, 22, 11, 90]` (ya se insertaron 34, 25 y 12; el 22 todavía está en su posición original, la 4):

| Comparación | ¿El vecino de la izquierda es mayor que 22? | Acción |
|---:|---|---|
| 1 | ¿64 > 22? Sí | Corro el 64 una posición a la derecha |
| 2 | ¿34 > 22? Sí | Corro el 34 una posición a la derecha |
| 3 | ¿25 > 22? Sí | Corro el 25 una posición a la derecha |
| 4 | ¿12 > 22? **No** | Paro acá: el 22 va justo después del 12 |

Tres corrimientos (64, 34 y 25 se movieron un lugar cada uno) y una cuarta comparación que no corrió nada, pero fue la que le indicó al algoritmo dónde parar. El resultado es `[12, 22, 25, 34, 64, 11, 90]` — exactamente la fila de la tabla de arriba. Es el mismo mecanismo del `while` del código: "mientras el vecino de la izquierda sea mayor, corrélo y seguí mirando más a la izquierda".

La parte ya ordenada (a la izquierda) crece de a uno en cada paso. En el último renglón, al llegar el 90, no hace falta correr **nada** — ya es más grande que todo lo que está a su izquierda. En el anteúltimo, el 11 tiene que correrse **5 posiciones** hasta el principio, porque es más chico que todos los que ya estaban ordenados. Esa diferencia enorme entre "0 corrimientos" y "5 corrimientos" según el valor es, exactamente, lo que hace que insertion sort sea rápido en datos casi ordenados y lento en datos al revés.

**Análisis:** peor caso (al revés) → **O(n²)**; caso promedio → **O(n²)**; mejor caso (ya ordenada, el `while` nunca entra) → **O(n)**. La cifra exacta ya está desarrollada en [[notación Big O y familias de complejidad]]: mejor caso $n-1$ comparaciones, promedio $\sim n^2/4$, peor caso $\sim n^2/2$.

> [!important] Por qué inserción es "el mejor de los tres" en la práctica: las inversiones
> La cantidad de intercambios que hace insertion sort es exactamente igual a la cantidad de **inversiones** de la lista de entrada — pares de elementos que están fuera de orden entre sí (por ejemplo, en `[3, 1, 2]`, el par `(3,1)` y el par `(3,2)` son inversiones, dos en total). Una lista con pocas inversiones se llama **parcialmente ordenada**, y son extremadamente comunes con datos reales: una tabla que ya viene casi ordenada de otra fuente, un archivo al que solo se le agregaron unas pocas filas nuevas al final. Sobre ese tipo de datos, insertion sort la ordena casi al costo de recorrerla una vez, muy lejos de su peor caso teórico. *Fuente: [[Algorithms-4th-Edition-By-Robert Sedgewick and Kevin Wayne]], cap. 2.1 (Proposición C).*

## Por qué se diferencian entre sí: la misma lista, la misma "primera pasada", tres lógicas distintas

Ya se vio el diálogo interno de cada uno por separado — acá están los tres, uno al lado del otro, actuando sobre la **misma** lista `[64, 34, 25, 12, 22, 11, 90]`, para que la diferencia de fondo quede a la vista de un vistazo:

| | Qué mira en cada vuelta del bucle de adentro | Cuándo intercambia/mueve | Qué queda resuelto al final de la primera pasada |
|---|---|---|---|
| **Burbuja** | Un par de **vecinos** (`a[j]` y `a[j+1]`) | En **cada** vuelta que estén al revés — potencialmente muchas veces por pasada | El elemento más grande de toda la lista (el que más veces "gana" comparaciones seguidas) queda al final |
| **Selección** | El candidato actual contra el **mejor mínimo visto hasta ahora** (`a[pos_min]`) | **Una sola vez**, recién cuando termina de recorrer todo lo que falta | El elemento más chico (11) queda al principio |
| **Inserción** | El elemento nuevo (`actual`) contra lo que ya está **ordenado a su izquierda** | Tantas veces como haga falta correr, pero solo **mirando hacia atrás** desde donde entró | El elemento en la posición `i` queda bien ubicado **respecto de todo lo que ya se procesó**, no de toda la lista |

Tres preguntas para fijar la diferencia:

> [!important] ¿En qué dirección "crece" lo que ya está resuelto?
> Burbuja y selección construyen la parte ordenada **de atrás para adelante** (burbuja fija el final, selección fija el principio) mirando **toda la lista completa** en cada pasada. Inserción construye la parte ordenada **de adelante para atrás**, pero solo necesita mirar la porción **ya procesada** — nunca los elementos que todavía no llegó a tocar. Esa es la razón estructural por la que inserción puede ser rápida en datos parcialmente ordenados y las otras dos, no: inserción literalmente ignora la mitad de la lista que sabe que todavía no importa.

> [!important] ¿Cuántos intercambios hace por cada elemento que "encuentra su lugar"?
> Burbuja puede necesitar **muchos** intercambios chiquitos (un vecino a la vez) para mover un valor lejos de donde está. Selección hace **un único** intercambio, sin importar qué tan lejos tenga que viajar el mínimo. Inserción hace **tantos corrimientos como haga falta**, pero cada uno mueve un solo elemento un solo lugar — parecido a la burbuja en el costo por movimiento, pero mirando en la dirección opuesta (hacia atrás, no hacia adelante) y solo dentro de la porción ya ordenada.

> [!important] ¿El algoritmo "sabe" cuándo puede dejar de trabajar?
> Selección **nunca** lo sabe de antemano: siempre recorre todo lo que falta, encuentre rápido el mínimo o no. Burbuja **sí** puede saberlo, con la bandera de la versión optimizada (si una pasada no intercambió nada, ya está). Inserción lo sabe **en cada elemento individual**: en cuanto el `while` encuentra un valor menor, para ahí mismo, sin necesidad de terminar de revisar toda la parte ordenada. Es la razón por la que, de los tres, inserción es el único que reacciona bien tanto a "la lista entera ya está ordenada" como a "una porción chica de la lista no lo está".

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
