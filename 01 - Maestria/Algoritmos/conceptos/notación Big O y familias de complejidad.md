---
titulo: "Notación Big O y familias de complejidad"
materia: Algoritmos
tipo: concepto
tags:
  - algoritmos
  - maestria
  - concepto
  - python
  - tema/complejidad
fecha: 2026-08-15
---

# Notación Big O y familias de complejidad

## El problema, sin código todavía

"¿Cuánto tarda este programa?" es una pregunta con trampa. Depende de la computadora, de qué más esté corriendo en ese momento, y sobre todo, de **cuántos datos** le des. Un algoritmo que anda perfecto con cien registros puede volverse inusable con cien millones — y la única forma de saberlo de antemano, sin tener que esperar a que falle en producción, es dejar de preguntar "¿cuánto tarda hoy?" y empezar a preguntar **"¿cómo crece el tiempo a medida que crecen los datos?"**. Esa pregunta —de forma, no de segundos concretos— es lo que responde la notación Big O.

Esta nota generaliza [[complejidad O(1) vs O(n)]] (que quedó centrada en el contraste puntual lista-vs-conjunto de la clase 1) al marco completo: todas las familias, la regla exacta para calcularlas, y un método para verificarlas empíricamente con una fórmula, no solo "a ojo".

## Definición formal

Todo lo de esta sección es **ampliación matemática opcional**: sirve para leer bibliografía que la use, pero ninguna nota del resto del vault depende de entenderla. La idea completa ya quedó dicha en criollo más arriba ("cómo crece el tiempo cuando crecen los datos, ignorando constantes y entradas chicas") — lo que sigue es esa misma idea, pero escrita con el lenguaje que usan los libros de texto: en vez de decir "para $n$ chico esto puede fallar, pero de cierto punto en adelante siempre se cumple", la convención matemática es nombrar ese "cierto punto" con una letra ($n_0$) y decir formalmente "para todo $n$ mayor o igual a $n_0$".

> [!definition] O(g(n))
> Una función $f(n)$ es $O(g(n))$ si existen constantes $c > 0$ y $n_0 \ge 0$ (números reales positivos) tales que $f(n) \le c \cdot g(n)$ para todo $n \ge n_0$. En criollo: a partir de cierto tamaño de entrada ($n_0$ en adelante), el costo real ($f$) nunca supera a una versión escalada de $g$ — $g$ es una **cota superior** de cómo crece $f$, ignorando lo que pase con entradas chicas y ignorando constantes multiplicativas. *Fuente: [[Data Structures and Algorithms with Python]], sec. 2.4; [[Algorithms-4th-Edition-By-Robert Sedgewick and Kevin Wayne]], cap. 1.4.*

> [!example] Un ejemplo resuelto con números, no solo con letras
> ¿Es $f(n) = 3n + 5$ un $O(n)$? Hay que encontrar **algún** $c$ y **algún** $n_0$ que hagan cumplir $3n+5 \le c\cdot n$ para todo $n \ge n_0$ — no hace falta el mejor par posible, alcanza con que exista uno.
>
> Probando $c = 4$: la desigualdad $3n + 5 \le 4n$ es lo mismo que $5 \le n$. Así que con $n_0 = 5$ se cumple siempre: en $n=5$, $f(5)=20$ y $4\cdot 5=20$ (empatan, `≤` los deja pasar); en $n=6$, $f(6)=23 \le 24$; y sigue así para adelante. Para $n=4$ (menor a $n_0$) no se cumple ($f(4)=17$, mayor que $4\cdot 4=16$) — y no hace falta que se cumpla ahí, la definición solo exige la desigualdad **a partir de** $n_0$.
>
> Encontrado un par $(c, n_0) = (4, 5)$ que funciona, queda demostrado: $f(n) = 3n+5$ es $O(n)$.

> [!tip] Dos primas de O que vas a encontrar en la bibliografía

Las reglas prácticas que ya usa la clase (descartar constantes, quedarse con el término dominante, sumar bucles secuenciales, multiplicar bucles anidados, analizar el peor caso) son consecuencia directa de esta definición — no reglas separadas para memorizar, sino la forma de aplicarla sin tener que encontrar $c$ y $n_0$ a mano cada vez.

> [!tip] Dos primas de O que vas a encontrar en la bibliografía
> $\Omega(g(n))$ es la cota **inferior** (lo opuesto de O: el costo nunca es *menor* que $g$ escalada). $\Theta(g(n))$ exige las dos cosas a la vez —cota superior y cota inferior— y por eso es la más precisa: dice que el algoritmo crece **exactamente** al ritmo de $g$, ni más rápido ni más lento. En la práctica del día a día "O(n)" se usa como si fuera "$\Theta(n)$" (la forma exacta), y esa imprecisión casi nunca genera problemas — pero vale saber que existe la distinción.

## Las familias, completas

La tabla de la clase tiene una familia menos de las que suele listar la bibliografía: falta la **cúbica**, $O(n^3)$, típica de tres bucles anidados (comparar todas las triplas posibles de $n$ elementos, por ejemplo).

| Familia | Notación | Código típico | Ejemplo |
|---|---|---|---|
| Constante | $O(1)$ | `a = b + c` | Acceder a `lista[5]`, buscar en un `set` |
| Logarítmica | $O(\log n)$ | dividir a la mitad en cada paso | Búsqueda binaria |
| Lineal | $O(n)$ | un `for` | Recorrer una lista |
| Linealogarítmica | $O(n \log n)$ | divide y conquistarás | Los buenos algoritmos de ordenamiento |
| Cuadrática | $O(n^2)$ | dos `for` anidados | Comparar todos los pares |
| Cúbica | $O(n^3)$ | tres `for` anidados | Comparar todas las triplas |
| Exponencial | $O(2^n)$ | ramifica en 2 en cada paso | Fibonacci recursivo, fuerza bruta |

*Fuente: [[Algorithms-4th-Edition-By-Robert Sedgewick and Kevin Wayne]], cap. 1.4.* El propio Sedgewick aclara que esta lista **no es exhaustiva** — un algoritmo real puede tener un costo como $O(n^2 \log n)$ o $O(n^{3/2})$, formas intermedias que no encajan en ninguna fila prolija de la tabla; las seis-siete familias de arriba son simplemente las que más aparecen en la práctica.

> [!important] Por qué $O(n \log n)$ no es casualidad en los algoritmos de ordenamiento
> No es que "los buenos algoritmos de ordenamiento resulten ser $O(n \log n)$" por buena suerte de sus diseñadores: se puede demostrar matemáticamente que **ningún** algoritmo que ordene comparando elementos de a pares puede hacerlo, en el peor caso, con menos de aproximadamente $n \log n$ comparaciones. $O(n \log n)$ no es una meta razonable, es el **límite teórico** — por eso mergesort, quicksort y timsort (el que usa Python internamente en `sorted()`) se consideran óptimos, no simplemente "buenos". *Fuente: [[Essential Algorithms A Practical Approach to Computer Algorithms]], cap. 1.*

## Mejor caso, peor caso, caso promedio

La clase ya aclaró la convención ("se analiza el peor caso, salvo que se diga lo contrario"), pero vale ver un ejemplo donde los tres casos dan números **distintos y concretos**, no solo etiquetas. Insertion sort —un algoritmo de ordenamiento que inserta cada elemento nuevo en la posición que le corresponde entre los ya ordenados— sobre un array de $n$ elementos:

| Caso | Cuándo ocurre | Comparaciones |
|---|---|---|
| Mejor caso | El array ya está ordenado | $n - 1$ |
| Caso promedio | Orden aleatorio | $\sim n^2/4$ |
| Peor caso | El array está ordenado al revés | $\sim n^2/2$ |

*Fuente: [[Algorithms-4th-Edition-By-Robert Sedgewick and Kevin Wayne]], cap. 2.1 (Proposición B).* La intuición: cada elemento nuevo "retrocede" hasta encontrar su lugar entre los ya insertados. Si el array ya viene ordenado, retrocede cero pasos siempre ($n-1$ comparaciones en total). Si viene al revés, cada elemento nuevo tiene que retroceder hasta el principio ($1+2+\dots+n \approx n^2/2$). En promedio, cada elemento retrocede "la mitad del camino" — de ahí el $n^2/4$. Los tres casos son $O(n)$ o $O(n^2)$ según cómo vengan los datos: la misma línea de código, tres comportamientos.

> [!example] Peor caso vs. caso promedio, en una herramienta que ya usás
> `np.sort()` puede usar distintos algoritmos internamente, y sus garantías de peor caso no son todas iguales. ("Estable" quiere decir que, si dos elementos tienen el mismo valor, el ordenamiento respeta el orden en que aparecían originalmente entre ellos — no los mezcla al azar; importa, por ejemplo, si ya se ordenó una tabla por una columna y ahora se quiere ordenar por otra sin perder el primer orden.)
>
> | Algoritmo | Peor caso | Estable |
> |---|---|---|
> | `quicksort` (default) | $O(n^2)$ | No |
> | `mergesort` | $O(n \log n)$ | Sí |
> | `heapsort` | $O(n \log n)$ | No |
>
> NumPy usa quicksort por defecto —peor caso $O(n^2)$— **a pesar de** que mergesort garantiza $O(n \log n)$ siempre, porque en el caso promedio quicksort suele ser más rápido en la práctica. Es un recordatorio concreto de que "peor caso" y "lo que conviene usar" no siempre apuntan al mismo algoritmo. *Fuente: [[Python-for-Data-Analysis]], Apéndice A.*

## Verificación empírica: la fórmula detrás de la regla informal

La clase ya tiene una regla práctica para medir y adivinar la familia: "duplicá $n$ y mirá qué le pasa al tiempo — si no cambia es O(1), si se duplica es O(n), si se cuadruplica es O(n²)". Esa regla es un caso particular de un método formal, con una fórmula que da el exponente exacto en vez de tener que reconocerlo a ojo.

> [!definition] Doubling ratio (Sedgewick)
> Si $T(n) \sim a \cdot n^b$, entonces al duplicar $n$ la razón de tiempos converge a $2^b$:
> $$\frac{T(2n)}{T(n)} \to 2^b \qquad \Longrightarrow \qquad b = \log_2\left(\frac{T(2n)}{T(n)}\right)$$
> *Fuente: [[Algorithms-4th-Edition-By-Robert Sedgewick and Kevin Wayne]], cap. 1.4 (Proposición C).*

Esto es exactamente la regla de la clase, pero generalizada: la razón no solo dice "se duplicó" o "se cuadruplicó" — su logaritmo en base 2 **es** el exponente $b$, sirva 2, 3, 0,5 o cualquier otro número. Aplicado a la comparación `hay_duplicados_lento` (O(n²)) vs. `hay_duplicados_rapido` (O(n)) que ya mide la clase, con tiempos reales medidos en este mismo entorno:

| $n$ | $O(n^2)$ (ms) | razón vs. anterior | $b = \log_2(\text{razón})$ |
|---|---|---|---|
| 200 | 0,21 | — | — |
| 400 | 1,16 | 5,5× | 2,46 |
| 800 | 5,09 | 4,4× | 2,13 |
| 1.600 | 19,39 | 3,8× | 1,93 |
| 3.200 | 78,85 | 4,1× | 2,02 |

El exponente converge a **$b \approx 2$** — confirma empíricamente, con una fórmula y no solo "a ojo", que el algoritmo es $O(n^2)$. Con esa misma razón se puede además **predecir** tiempos sin medirlos: $T(n) = T(n_0) \cdot (n/n_0)^b$.

> [!warning] El método puede confundir O(n) con O(n log n)
> Para valores de $n$ moderados, la curva de $14n$ y la de $n \log n$ quedan visualmente casi pegadas — el factor logarítmico crece tan despacio que la razón de duplicación se acerca a 2 en ambos casos, y hace falta ir a $n$ bastante más grande (o medir con mucha más precisión) para distinguirlos con este método. Es una limitación real del enfoque empírico, no un error de aplicación. *Fuente: [[Algorithms-4th-Edition-By-Robert Sedgewick and Kevin Wayne]], cap. 1.4.*

> [!note] En código: `%timeit` automatiza lo que la clase hace a mano
> El patrón de la clase —repetir la medición varias veces y quedarse con la mediana, para no dejarse engañar por un pico aislado del sistema— es exactamente lo que hace automáticamente el comando mágico `%timeit` de IPython/Jupyter: ajusta solo la cantidad de repeticiones según la velocidad del código y devuelve media ± desvío estándar. Una salvedad real que documenta VanderPlas: si el código tiene **estado** que cambia entre repeticiones (por ejemplo, ordenar una lista que la primera repetición ya dejó ordenada), repetir sesga el resultado — para esos casos conviene medir una sola vez con `%time` en lugar de `%timeit`. *Fuente: [[Python data science handbook]], cap. 3, "Profiling and Timing Code".*

## Complejidad espacial y el intercambio memoria-tiempo

La memoización de [[recursion y memoizacion]] ya ilustra el *space-time tradeoff*: pagar memoria (el diccionario de resultados) para ahorrar tiempo (no recalcular). El tamaño real de ese ahorro es más extremo de lo que parece a simple vista:

> [!example] Fibonacci sin memoizar, en números concretos
> Calcular `fib(100)` sin memoizar requiere del orden de $10^{21}$ llamadas recursivas — a 10 microsegundos por llamada, unos **363 millones de años**. Memoizado, son 100 llamadas: **1 milisegundo**. Es la misma función, la misma respuesta matemática — la diferencia completa es haber guardado cada resultado una sola vez. *Fuente: [[Data Structures and Algorithms with Python]], sec. 5.8.*

El mismo intercambio aparece en cualquier tabla precalculada (un índice de base de datos, una caché de navegador, un dashboard que recalcula de noche en vez de en cada clic): se paga espacio de antemano para no volver a pagar tiempo cada vez que se pregunta lo mismo.

## Relacionado
- [[complejidad O(1) vs O(n)]]
- [[árboles]]
- [[grafos y recorridos (DFS, BFS)]]
- [[recursion y memoizacion]]
- [[hashing y hashabilidad]]
- [[02 - Programacion imperativa]]
