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

Algunos problemas se definen de forma natural en términos de una versión más chica de sí mismos: el factorial de `n` se define usando el factorial de `n-1`; recorrer un árbol significa recorrer los subárboles de cada uno de sus hijos, que a su vez son árboles. Un `for`/`while` recorre secuencias lineales; para un problema que se ramifica o se reduce a sí mismo, forzarlo a un bucle suele terminar en código más enredado que el problema original. La recursión ofrece una forma de expresarlo directamente.

> [!definition] Función recursiva
> Una función que **se llama a sí misma**. Es la forma natural de resolver problemas que se definen en términos de sí mismos: si sé resolver el problema para un caso más chico, puedo resolver el grande.

Toda función recursiva necesita **dos** partes; si falta alguna, no funciona:

1. **Caso base**: la situación tan simple que se resuelve directo, sin llamarse de nuevo. Es lo que hace que la cadena termine.
2. **Caso recursivo**: reducir el problema a una versión más chica y llamarse a sí misma con esa versión.

> [!tip] Una tercera regla, menos obvia: que los subproblemas no se solapen
> Además de tener caso base y acercarse a él, conviene que las llamadas recursivas resuelvan **subproblemas independientes**, sin recalcular el mismo trabajo dos veces. Esta regla no hace que una recursión "funcione" o no (Fibonacci funciona igual sin respetarla), pero es la que separa una recursión **eficiente** de una que no lo es — es exactamente lo que falla en el Fibonacci ingenuo de más abajo, y lo que la memoización viene a corregir. *Fuente: [[Algorithms-4th-Edition-By-Robert Sedgewick and Kevin Wayne]], cap. 1.*

## Ejemplo: factorial

$$n! = n \times (n-1)! \qquad \text{con} \qquad 0! = 1$$

```python
def factorial(n):
    if n <= 1:                    # CASO BASE
        return 1
    return n * factorial(n - 1)   # CASO RECURSIVO

print([factorial(i) for i in range(6)])   # [1, 1, 2, 6, 24, 120]
```

### Cómo se ejecuta realmente: la pila de llamadas

`factorial(4)` no se resuelve de una vez: se abre una cadena de llamadas que **baja** hasta el caso base y después **vuelve** multiplicando. Cada llamada queda "esperando" en memoria (en la **pila de llamadas**, *call stack*) a que la de adentro termine:

```
factorial(4)
  -> 4 * factorial(3)
       -> 3 * factorial(2)
            -> 2 * factorial(1)
                 -> 1              <- caso base, empieza la vuelta
            -> 2 * 1 = 2
       -> 3 * 2 = 6
  -> 4 * 6 = 24
```

Esto tiene un costo real: la memoria usada por la pila crece con la **profundidad** de la recursión.

> [!tip] La pila de llamadas es, literalmente, una pila (Stack, LIFO)
> No es una metáfora: el intérprete reserva cada llamada activa en una zona de memoria llamada **stack**, separada del **heap** (donde viven los objetos, listas, diccionarios). Cada llamada guarda ahí sus variables locales en un registro propio (un *activation record*), y esos registros se apilan y desapilan en orden **LIFO** (*last-in, first-out*: la última llamada en entrar es la primera en salir) — el mismo principio que define al TAD *Stack* que se ve más adelante en la materia. El stack suele ser bastante más chico que el heap; por eso una recursión muy profunda puede agotarlo y terminar en `RecursionError` aunque sobre memoria "en general" (en el heap). *Fuente: [[Algorithms-4th-Edition-By-Robert Sedgewick and Kevin Wayne]], cap. 1; [[Essential Algorithms A Practical Approach to Computer Algorithms]], cap. 9.*

> [!danger] Sin caso base, o si el caso recursivo no se acerca a él: `RecursionError`
> ```python
> def factorial_roto(n):
>     return n * factorial_roto(n - 1)   # nunca llega a un caso base
>
> factorial_roto(5)   # RecursionError: maximum recursion depth exceeded
> ```
> Python corta a las ~1000 llamadas para proteger la memoria; es el equivalente recursivo de un bucle `while` infinito. Antes de escribir una función recursiva, conviene verificar: *¿existe un caso base, y cada llamada me acerca a él?*
>
> Ojo con un descuido común: `if n <= 1: return 1` "arregla" silenciosamente el caso de un `n` negativo (nunca debería pedirse el factorial de `-5`), tratándolo igual que el caso base en vez de avisar del error. Es cómodo, pero esconde un uso incorrecto de la función en vez de reportarlo — vale la pena tenerlo presente como una decisión de diseño, no solo como un detalle técnico.

## No toda recursión es sobre números: recorrer secuencias

Factorial reduce un **número**; la recursión también sirve para reducir una **secuencia** (lista, string), un dato ya conocido de la clase 1. El mismo patrón caso base/caso recursivo aplica igual:

```python
def invertir(lista):
    if lista == []:            # CASO BASE: la lista vacía se invierte a sí misma
        return []
    return invertir(lista[1:]) + lista[0:1]   # CASO RECURSIVO: invertir "el resto" y agregar el primero al final

print(invertir([1, 2, 3, 4]))   # [4, 3, 2, 1]
```

La misma función sirve, casi sin cambios, para invertir un string (`lista[1:]` y `lista[0:1]` funcionan igual sobre un `str`, porque comparten el protocolo de slicing de la clase 1). No es una coincidencia: cualquier estructura que se pueda "partir en primero + resto" es candidata natural a recorrerse recursivamente. *Fuente: [[Data Structures and Algorithms with Python]], cap. 3.*

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

Por qué el bucle suele ganar en velocidad, más allá de no consumir pila: cada llamada a función tiene un costo propio (armar el *activation record*, ver el callout de la pila de llamadas más arriba); revisar la condición de un `while` es más barato que hacer esa llamada. Convertir una recursión en bucle acumulando el resultado en una variable (como hace `fibonacci_bucle`) se conoce como **eliminar la recursión** — `fibonacci_bucle` no es solo "otra forma de escribirlo", es exactamente esa técnica aplicada al caso de Fibonacci. Es, además, la misma idea de fondo que la memoización: en vez de recordar resultados ya calculados con un diccionario (*top-down*), se los calcula una única vez, en orden creciente, directamente con un bucle (*bottom-up*) — dos caminos distintos a la misma eliminación de trabajo repetido. *Fuente: [[Essential Algorithms A Practical Approach to Computer Algorithms]], cap. 9.*

> [!note] Entonces, ¿para qué sirve la recursión?
> Para problemas cuya **estructura** es recursiva. Un bucle recorre una secuencia lineal; la recursión recorre naturalmente estructuras que se ramifican. En la clase 3 (árboles y grafos) cada nodo tiene hijos que a su vez son árboles — ahí la versión recursiva es de tres líneas y la iterativa es un enredo. Esto importa directamente en minería de datos: **un árbol de decisión es un árbol**, y se construye y se recorre recursivamente.

## Puente con Tecnologías

La memoización es el mismo principio de fondo que hace útiles al *caching* en librerías de cómputo (por ejemplo, resultados intermedios que scikit-learn o statsmodels evitan recalcular). Y el diagnóstico "el código elegante no es necesariamente el eficiente" es la razón exacta por la que existe NumPy: comparar `fibonacci` (recursión directa) contra `fibonacci_memo` es, en miniatura, la misma comparación que un bucle en Python puro contra una operación vectorizada — ver [[complejidad O(1) vs O(n)]].

## Relacionado
- [[02 - Programacion imperativa]]
- [[funciones, parametros y alcance]]
- [[complejidad O(1) vs O(n)]]
- [[hashing y hashabilidad]]
