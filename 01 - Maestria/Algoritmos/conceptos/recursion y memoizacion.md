---
titulo: Recursión y memoización
materia: Algoritmos
tipo: concepto
tags:
  - algoritmos
  - maestria
  - concepto
  - python
  - tema/recursion
fecha: 2026-08-08
---

# Recursión y memoización

## El problema, sin código todavía

Imaginate una fila de personas, y querés saber en qué posición estás. Una forma es contarte a vos mismo. Otra, más rara, funciona así: le preguntás a la persona que tenés justo **adelante** "¿vos en qué posición estás?", y a lo que te responda le sumás 1.

El problema es que esa persona tampoco sabe su posición de memoria — así que le hace la misma pregunta a quien tiene adelante suyo. Y esa persona, a la siguiente. Así hasta llegar a la primera persona de la fila, que **sí** puede responder sin preguntarle a nadie: *"yo soy la posición 1"*.

Ahí la cadena empieza a volver: la persona 1 le contesta "1" a la persona 2. La persona 2 calcula 1+1=2 y se lo pasa a la persona 3. Y así, sumando 1 en cada paso, hasta que la respuesta te llega a vos.

**Eso es recursión.** Nadie resolvió el problema completo de una sola vez. Cada persona resolvió una versión *idéntica pero más chica* del mismo problema — preguntarle a la de adelante — confiando en que esa persona iba a hacer exactamente lo mismo.

> [!definition] Función recursiva
> Una función que **se llama a sí misma**, para resolver un problema reduciéndolo a una versión más chica del mismo problema — igual que cada persona de la fila resuelve "mi posición" preguntando la posición de quien tiene adelante.

## Las dos piezas obligatorias

Toda función recursiva necesita **dos** partes; si falta alguna, no funciona:

1. **Caso base**: la situación tan simple que se resuelve directo, sin llamarse de nuevo. Es lo que hace que la cadena termine. (*"Soy la primera persona de la fila: mi posición es 1."*)
2. **Caso recursivo**: reducir el problema a una versión más chica y llamarse a sí misma con esa versión, confiando en que esa llamada más chica va a devolver la respuesta correcta. (*"Mi posición = 1 + la posición de quien tengo adelante."*)

> [!tip] La "fe recursiva": no hace falta seguirle el rastro a toda la cadena
> Lo que más cuesta al principio es la tentación de imaginarse mentalmente *toda* la fila de personas preguntando, paso a paso, antes de animarse a escribir la función. No hace falta. Alcanza con confiar en que la llamada recursiva **ya resuelve correctamente** la versión más chica del problema — el mismo salto de fe que hace la persona 5 al preguntarle a la persona 4, sin necesitar saber cómo hizo la persona 4 para averiguar la suya. Esta idea tiene nombre en la bibliografía: el **"salto de fe"** (*leap of faith*) al escribir el caso recursivo. *Fuente: [[Data Structures and Algorithms with Python]], cap. 3.*

> [!tip] Una tercera regla, menos obvia: que los subproblemas no se solapen
> Además de tener caso base y acercarse a él, conviene que las llamadas recursivas resuelvan **subproblemas independientes**, sin recalcular el mismo trabajo dos veces. Esta regla no hace que una recursión "funcione" o no (Fibonacci funciona igual sin respetarla, más abajo), pero es la que separa una recursión **eficiente** de una que no lo es. *Fuente: [[Algorithms-4th-Edition-By-Robert Sedgewick and Kevin Wayne]], cap. 1.*

## Por qué no se rompe la cadena: cada llamada "espera" a la anterior

Cuando la persona 5 le pregunta a la persona 4, la persona 5 **no se va a ningún lado** — se queda parada, esperando la respuesta, con la cuenta "lo que me diga + 1" ya preparada para cuando llegue. Es exactamente como una **pila de bandejas en un comedor**: la última bandeja que se apiló es la primera que se saca. Cada persona de la fila funciona como una bandeja que se apila mientras la cadena "baja" preguntando, y recién se empieza a "sacar" (a responder) cuando se llega al fondo de la pila — el caso base.

Esto no es solo una metáfora para entender: en la computadora es **literal**.

## Ejemplo: factorial

$$n! = n \times (n-1)! \qquad \text{con} \qquad 0! = 1$$

```python
def factorial(n):
    if n <= 1:                    # CASO BASE
        return 1
    return n * factorial(n - 1)   # CASO RECURSIVO

print([factorial(i) for i in range(6)])   # [1, 1, 2, 6, 24, 120]
```

Trazando `factorial(4)` con la misma lógica de la fila de personas — **primero baja preguntando, después sube respondiendo**:

```
factorial(4)   "no sé, preguntale a factorial(3) y multiplico por 4"
  factorial(3)   "no sé, preguntale a factorial(2) y multiplico por 3"
    factorial(2)   "no sé, preguntale a factorial(1) y multiplico por 2"
      factorial(1)   "yo sé mi respuesta sin preguntar: 1"     <- CASO BASE, acá se da vuelta
    factorial(2) recibe 1, calcula 2*1 = 2
  factorial(3) recibe 2, calcula 3*2 = 6
factorial(4) recibe 6, calcula 4*6 = 24
```

Ningún nivel tuvo que entender el problema completo: `factorial(4)` solo resolvió una pregunta chiquita ("¿cuánto es 4 por lo que me diga `factorial(3)`?") y confió en la respuesta de abajo — la misma fe recursiva de la fila de personas.

### La pila de llamadas es, literalmente, una pila (Stack, LIFO)

Cada llamada activa queda reservada en una zona de memoria llamada **stack**, separada del **heap** (donde viven los objetos, listas, diccionarios). Cada llamada guarda ahí sus variables locales en un registro propio (un *activation record*, "registro de activación": una ficha con los datos de esa llamada puntual — sus parámetros, sus variables, en qué línea quedó esperando), y esos registros se apilan y desapilan en orden **LIFO** (*last-in, first-out*, "último en entrar, primero en salir": la última llamada en entrar es la primera en salir) — el mismo principio que define al **TAD** (Tipo Abstracto de Datos) *Stack* que se ve más adelante en la materia, y la misma imagen de la pila de bandejas de arriba. El stack suele ser bastante más chico que el heap; por eso una recursión muy profunda puede agotarlo y terminar en `RecursionError` aunque sobre memoria "en general" (en el heap). *Fuente: [[Algorithms-4th-Edition-By-Robert Sedgewick and Kevin Wayne]], cap. 1; [[Essential Algorithms A Practical Approach to Computer Algorithms]], cap. 9.*

Esto tiene un costo real: la memoria usada por la pila crece con la **profundidad** de la recursión.

> [!danger] Sin caso base, o si el caso recursivo no se acerca a él: `RecursionError`
> ```python
> def factorial_roto(n):
>     return n * factorial_roto(n - 1)   # nunca llega a un caso base
>
> factorial_roto(5)   # RecursionError: maximum recursion depth exceeded
> ```
> Python corta a las ~1000 llamadas para proteger la memoria; es el equivalente recursivo de un bucle `while` infinito — o, con la imagen de arriba, una fila **sin primera persona**: todos preguntando para atrás, eternamente, sin que nadie conteste nunca. Es la misma idea que dos espejos puestos uno frente al otro: el reflejo se repite para siempre porque no hay ningún punto donde "cortar". Antes de escribir una función recursiva, conviene verificar: *¿existe un caso base, y cada llamada me acerca a él?*
>
> Ojo con un descuido común: `if n <= 1: return 1` "arregla" silenciosamente el caso de un `n` negativo (nunca debería pedirse el factorial de `-5`), tratándolo igual que el caso base en vez de avisar del error. Es cómodo, pero esconde un uso incorrecto de la función en vez de reportarlo — vale la pena tenerlo presente como una decisión de diseño, no solo como un detalle técnico.

## No toda recursión es sobre números: recorrer secuencias

Factorial reduce un **número**; la recursión también sirve para reducir una **secuencia** (lista, string), un dato ya conocido de la clase 1. El mismo patrón caso base/caso recursivo aplica igual — y muestra que la idea de "un pedacito + el resto, que es el mismo problema más chico" no es exclusiva de los números:

```python
def invertir(lista):
    if lista == []:            # CASO BASE: la lista vacía se invierte a sí misma
        return []
    return invertir(lista[1:]) + lista[0:1]   # CASO RECURSIVO: invertir "el resto" y agregar el primero al final

print(invertir([1, 2, 3, 4]))   # [4, 3, 2, 1]
```

`invertir([1, 2, 3, 4])` se lee: *"invertir el resto de la lista, y poner el primer elemento al final"*. La misma función sirve, casi sin cambios, para invertir un string (`lista[1:]` y `lista[0:1]` funcionan igual sobre un `str`, porque comparten el protocolo de slicing de la clase 1). No es una coincidencia: cualquier estructura que se pueda "partir en primero + resto" es candidata natural a recorrerse recursivamente. *Fuente: [[Data Structures and Algorithms with Python]], cap. 3.*

> [!tip] Checklist para escribir cualquier función recursiva
> Cuatro preguntas que alcanzan siempre, combinando el criterio de Sedgewick y de *Data Structures and Algorithms with Python*:
> 1. ¿Cuál es el caso **tan simple** que se puede responder directo, sin llamar de nuevo a la función?
> 2. ¿Cómo se reduce el problema a una versión **más chica** del mismo problema?
> 3. ¿Esa versión más chica **se acerca** al caso base en cada llamada (nunca se aleja ni se queda igual)?
> 4. Al escribir la llamada recursiva, ¿se está **confiando** en que ya funciona para ese caso más chico (la fe recursiva de arriba), en vez de tratar de imaginarse toda la cadena de llamadas?
>
> Si las cuatro respuestas están claras, la función funciona — aunque al principio se sienta raro "confiar" en una función que todavía ni se terminó de escribir.

## Fibonacci y el costo oculto de la recursión

$$F(n) = F(n-1) + F(n-2) \qquad \text{con} \qquad F(0)=0,\ F(1)=1$$

```python
def fibonacci(n):
    if n <= 1:                              # DOS casos base: F(0)=0 y F(1)=1
        return n
    return fibonacci(n - 1) + fibonacci(n - 2)

print([fibonacci(i) for i in range(12)])
# [0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89]
```

La función se lee igual que la definición matemática — pero es **terriblemente ineficiente**, porque recalcula el mismo valor una y otra vez:

```
                    fib(5)
              /                \
          fib(4)               fib(3)
         /      \             /      \
     fib(3)    fib(2)     fib(2)    fib(1)
    /     \    /    \     /    \
 fib(2) fib(1) ...        ...
```

`fib(3)` se calcula 2 veces, `fib(2)` 3 veces, `fib(1)` 5 veces — y la redundancia empeora exponencialmente con `n`. Contando cuántas veces se invoca la función (un conteo exacto, no una medición de tiempo que dependa de la máquina):

| n | F(n) | Llamadas a fibonacci() |
|---:|---:|---:|
| 5 | 5 | 15 |
| 10 | 55 | 177 |
| 15 | 610 | 1.973 |
| 20 | 6.765 | 21.891 |
| 25 | 75.025 | 242.785 |
| 30 | 832.040 | 2.692.537 |

Para calcular `F(30)` —un número de apenas seis cifras— la función se invoca casi **2,7 millones de veces**, y cada vez que `n` sube en 1 la cantidad de llamadas se multiplica por aproximadamente 1,6 (la proporción áurea). Esto es complejidad **O(2ⁿ)**, de las peores posibles — la clase 3 le pone nombre y notación formal a esta idea (ver [[complejidad O(1) vs O(n)]]).

> [!important] La elegancia del código no dice nada sobre su eficiencia
> Tres líneas hermosas, casi 2,7 millones de llamadas repetidas para un solo valor mediano. La cosa empeora rápido: calcular `F(100)` sin memoizar necesitaría, según el mismo conteo, más de **1.146.295.688.027.634.168.201** llamadas — a 10 microsegundos por llamada, tardaría unos **363 millones de años**. Es la misma explosión combinatoria que la Torre de Hanoi con muchos discos ($T(n) = 2\,T(n-1) + 1 = 2^n - 1$ movimientos): dos problemas de dominios completamente distintos (números, discos) con la misma estructura recursiva de fondo, y el mismo costo exponencial. *Fuente: [[Data Structures and Algorithms with Python]], cap. 5; [[Essential Algorithms A Practical Approach to Computer Algorithms]], cap. 9.*

## La solución: memoización

Si el problema es recalcular lo mismo, la solución es **guardar los resultados ya calculados** la primera vez, en un diccionario, y reutilizarlos después:

```python
def fibonacci_memo(n, memoria=None):
    if memoria is None:
        memoria = {}
    if n in memoria:               # ¿ya lo calculamos antes?
        return memoria[n]
    if n <= 1:
        return n
    resultado = fibonacci_memo(n - 1, memoria) + fibonacci_memo(n - 2, memoria)
    memoria[n] = resultado          # lo guardamos para la próxima
    return resultado

print(fibonacci_memo(30))    # 832040 -> mismo resultado, una sola pasada por cada n
print(f"{fibonacci_memo(100):,}")   # 354.224.848.179.261.915.075
```

Con memoización, cada valor de `n` se calcula **una sola vez**: el costo pasa de O(2ⁿ) a O(n). Es lo que permite calcular `F(100)` o `F(300)` al instante, valores que la versión directa jamás alcanzaría en un tiempo razonable. Esta técnica —cachear resultados en una estructura de acceso O(1)— es la misma idea que hace rápido a un diccionario o un `set` (ver [[hashing y hashabilidad]]).

> [!tip] Una variante: el diccionario "afuera" en vez de como parámetro
> `fibonacci_memo` de arriba pasa el diccionario `memoria` como parámetro con valor por defecto — una forma explícita y autocontenida de memoizar. Una variante habitual es declarar el diccionario **una sola vez, fuera de la función** (en el módulo, o en una función envolvente), y que la función recursiva lo lea/escriba por alcance **enclosing** en vez de recibirlo como argumento — el mismo resultado, con menos parámetros pero un poco menos autocontenido. Ver [[funciones, parametros y alcance]] para la distinción de alcances. *Fuente: [[Data Structures and Algorithms with Python]], cap. 5.*

## ¿Recursión o bucle?

Casi todo lo recursivo se puede reescribir con un bucle, y suele ser más eficiente porque no consume pila:

```python
def fibonacci_bucle(n):
    a, b = 0, 1
    for _ in range(n):
        a, b = b, a + b     # intercambio múltiple, visto en la clase 1
    return a

print(fibonacci_bucle(30))   # 832040
```

Por qué el bucle suele ganar en velocidad, más allá de no consumir pila: cada llamada a función tiene un costo propio (armar el *activation record*, ver el callout de la pila de llamadas más arriba); revisar la condición de un `while` es más barato que hacer esa llamada. Convertir una recursión en bucle acumulando el resultado en una variable (como hace `fibonacci_bucle`) se conoce como **eliminar la recursión** — `fibonacci_bucle` no es solo "otra forma de escribirlo", es exactamente esa técnica aplicada al caso de Fibonacci. Es, además, la misma idea de fondo que la memoización: en vez de recordar resultados ya calculados con un diccionario, empezando por el problema grande y resolviendo hacia abajo a medida que hace falta (*top-down*, "de arriba hacia abajo"), se los calcula una única vez, en orden creciente, empezando por los casos más chicos y subiendo directamente con un bucle (*bottom-up*, "de abajo hacia arriba") — dos caminos distintos a la misma eliminación de trabajo repetido. *Fuente: [[Essential Algorithms A Practical Approach to Computer Algorithms]], cap. 9.*

> [!note] Entonces, ¿para qué sirve la recursión?
> Para problemas cuya **estructura** es recursiva. Un bucle recorre una secuencia lineal; la recursión recorre naturalmente estructuras que se ramifican. En la clase 3 (árboles y grafos) cada nodo tiene hijos que a su vez son árboles — ahí la versión recursiva es de tres líneas y la iterativa es un enredo. Esto importa directamente en minería de datos: **un árbol de decisión es un árbol**, y se construye y se recorre recursivamente.

## Puente con Tecnologías

La memoización es el mismo principio de fondo que hace útil el *caching* ("guardar en caché": conservar un resultado ya calculado a mano, en vez de rehacer el cálculo) en librerías de cómputo — por ejemplo, resultados intermedios que scikit-learn o statsmodels evitan recalcular. Y el diagnóstico "el código elegante no es necesariamente el eficiente" es la razón exacta por la que existe NumPy: comparar `fibonacci` (recursión directa) contra `fibonacci_memo` es, en miniatura, la misma comparación que un bucle en Python puro contra una operación vectorizada — ver [[complejidad O(1) vs O(n)]].

## Relacionado
- [[02 - Programacion imperativa]]
- [[funciones, parametros y alcance]]
- [[complejidad O(1) vs O(n)]]
- [[hashing y hashabilidad]]
