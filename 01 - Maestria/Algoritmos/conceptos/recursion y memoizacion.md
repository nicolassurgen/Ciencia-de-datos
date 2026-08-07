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

> [!danger] Sin caso base, o si el caso recursivo no se acerca a él: `RecursionError`
> ```python
> def factorial_roto(n):
>     return n * factorial_roto(n - 1)   # nunca llega a un caso base
>
> factorial_roto(5)   # RecursionError: maximum recursion depth exceeded
> ```
> Python corta a las ~1000 llamadas para proteger la memoria; es el equivalente recursivo de un bucle `while` infinito. Antes de escribir una función recursiva, conviene verificar: *¿existe un caso base, y cada llamada me acerca a él?*

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
> Tres líneas hermosas, casi 2,7 millones de llamadas repetidas para un solo valor mediano.

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

> [!note] Entonces, ¿para qué sirve la recursión?
> Para problemas cuya **estructura** es recursiva. Un bucle recorre una secuencia lineal; la recursión recorre naturalmente estructuras que se ramifican. En la clase 3 (árboles y grafos) cada nodo tiene hijos que a su vez son árboles — ahí la versión recursiva es de tres líneas y la iterativa es un enredo. Esto importa directamente en minería de datos: **un árbol de decisión es un árbol**, y se construye y se recorre recursivamente.

## Puente con Tecnologías

La memoización es el mismo principio de fondo que hace útiles al *caching* en librerías de cómputo (por ejemplo, resultados intermedios que scikit-learn o statsmodels evitan recalcular). Y el diagnóstico "el código elegante no es necesariamente el eficiente" es la razón exacta por la que existe NumPy: comparar `fibonacci` (recursión directa) contra `fibonacci_memo` es, en miniatura, la misma comparación que un bucle en Python puro contra una operación vectorizada — ver [[complejidad O(1) vs O(n)]].

## Relacionado
- [[02 - Programacion imperativa]]
- [[funciones, parametros y alcance]]
- [[complejidad O(1) vs O(n)]]
- [[hashing y hashabilidad]]
