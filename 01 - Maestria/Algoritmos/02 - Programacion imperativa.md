---
titulo: "Clase 2 — Programación imperativa"
materia: Algoritmos
tipo: apunte
clase: 2
fecha: 2026-08-08
tags:
  - algoritmos
  - maestria
  - python
  - programacion-imperativa
  - tema/programacion-imperativa
---

# Algoritmos · Clase 2 — Programación imperativa

> [!abstract] Idea central de la clase
> La clase 1 enseñó a **guardar** datos (tipos, estructuras). Esta clase enseña a **hacer cosas con ellos**. Un programa que solo ejecuta instrucciones en línea recta alcanza para calcular, pero no para resolver problemas: hacen falta tres capacidades más — **decidir** (condicionales), **repetir** (bucles) y **abstraer** (funciones) — más una cuarta, más avanzada, que resuelve problemas que se definen en términos de sí mismos: la **recursión**.
>
> Dos ideas para llevarse:
> 1. **El código elegante no es necesariamente eficiente.** Fibonacci recursivo son tres líneas hermosas y casi 2,7 millones de llamadas para calcular un solo valor mediano.
> 2. **Toda repetición necesita una condición de salida.** Un `while` sin salida es un bucle infinito; una recursión sin caso base es un `RecursionError`. Es el mismo error, con dos caras distintas.

> [!note] Convención de esta nota
> Los callouts **"Puente con Estadística"** y **"Puente con Tecnologías"**, y cualquier tramo marcado explícitamente como **"ampliación"**, son agregados míos para conectar con el resto de la maestría — no los dio el profesor. El resto sigue de cerca la clase (notebooks `Clase2_Programacion_imperativa.ipynb` y el repaso de `Actividad_Clase2.ipynb`).

> [!info] Puente con Tecnologías
> Todo lo de hoy —recorrer con `for`, acumular en variables, filtrar con `if`— es exactamente lo que reemplazan las operaciones vectorizadas de NumPy y el `groupby` de Pandas. Escribirlo a mano una vez es lo que permite entender qué esconde `df.groupby("especie")["masa_g"].mean()`. Ver el bloque 7 de este apunte y [[bucles for, while y el patron acumulador]].

---

## 1. Condicionales: que el programa decida

Un **condicional** ejecuta un bloque de código **solo si** se cumple una condición — una expresión que da `True` o `False`, como las de la clase 1.

```python
masa = 3200
if masa > 4000:
    print("Esta línea está DENTRO del if")
print("Esta está AFUERA: se ejecuta siempre")
```

Dos cosas que Python exige: **los dos puntos `:`** al final de la línea del `if`, y la **sangría** (indentación, convención de 4 espacios) del bloque de adentro. En Python los bloques se marcan con sangría, no con llaves `{ }` — no es cosmética, es sintaxis.

`elif` (*else if*) encadena condiciones cuando hay más de dos casos. Se evalúan **en orden** y se ejecuta **solo la primera** que da verdadera:

```python
masa = 4500
if masa > 5000:
    categoria = "muy grande"
elif masa > 4000:
    categoria = "grande"
elif masa > 3500:
    categoria = "mediano"
else:
    categoria = "chico"
print(f"Masa {masa} g -> {categoria}")   # Masa 4500 g -> grande
```

Con `and`, `or`, `not` (y `in` como forma más legible de "es alguno de estos") se combinan condiciones, igual que en la clase 1.

El desarrollo completo de este bloque —incluido el error clásico de escribir las condiciones en el orden equivocado, y la trampa del truthy/falsy con datos faltantes (`if masa:` no es lo mismo que `if masa is None:`)— está en [[condicionales y evaluacion de verdad]].

---

## 2. Bucles: que el programa repita

Un **bucle** ejecuta un bloque de código varias veces — lo que permite aplicar el mismo tratamiento a los 344 pingüinos del dataset sin escribir 344 líneas.

`for` recorre una colección elemento por elemento:

```python
especies = ["Adelie", "Gentoo", "Chinstrap"]
for especie in especies:
    print(f"Procesando: {especie}")
```

`range()` genera una secuencia de enteros sin recorrer una colección existente; `enumerate()` entrega la posición junto con el elemento; `zip()` recorre varias colecciones en paralelo. El **patrón acumulador** —inicializar antes del bucle, actualizar adentro, usar después— es la estructura detrás de casi todo cálculo sobre datos:

```python
masas = [3750.0, 3800.0, 3250.0, 4500.0, 3700.0]
total, cantidad = 0, 0
for m in masas:
    total += m
    cantidad += 1
print(f"Promedio: {total / cantidad:,.1f} g")   # Promedio: 3,800.0 g
```

`break` corta el bucle por completo; `continue` saltea el resto de la vuelta actual. `while` repite mientras una condición sea verdadera — útil cuando no se sabe de antemano cuántas vueltas hacen falta, pero con el riesgo del **bucle infinito** si la condición nunca se vuelve falsa.

El desarrollo completo —`range()`/`enumerate()`/`zip()` con ejemplos, la trampa de `zip()` con listas de distinta longitud, `break`/`continue`, y el peligro concreto del `while` infinito— está en [[bucles for, while y el patron acumulador]].

### Comprensiones de listas

Python tiene una forma compacta de escribir "recorrer una lista y armar otra": la **comprensión de lista**.

```python
masas_validas = [p["masa_g"] for p in pinguinos if p["masa_g"] is not None]
```

Se lee de adentro hacia afuera: *"la masa, para cada pingüino, si no es None"*. Detalle completo, con la equivalencia exacta contra el `for` largo y el criterio de cuándo conviene usarla, en [[comprensiones de listas]].

---

## 3. Funciones: darle nombre a un procedimiento

Repetir la misma lógica de conversión varias veces (como pasó en el bloque 2, con "texto a número o `None`") es una señal de que hace falta una **función**: empaquetar un procedimiento bajo un nombre para invocarlo cuantas veces haga falta, corregirlo en un solo lugar, y hacer el código legible.

```python
def a_numero(texto):
    """Convierte texto a float. Devuelve None si el campo está vacío."""
    if texto == "":
        return None
    return float(texto)

print(a_numero("39.1"))   # 39.1
print(a_numero(""))       # None
```

Punto que más confunde a quien arranca: **`return` corta la ejecución** y **una función sin `return` devuelve `None`** — `print` es para mostrarle algo a una persona, `return` es para entregarle un valor al programa.

Los parámetros pueden tener **valores por defecto**, y los argumentos se pueden pasar **por nombre** (en cualquier orden, mucho más legibles cuando hay varios). Una función puede devolver **varios valores** a la vez, empaquetados en una tupla:

```python
def resumir(valores):
    """Devuelve (mínimo, máximo, promedio) de una lista de números."""
    return min(valores), max(valores), sum(valores) / len(valores)

minimo, maximo, promedio = resumir([3750.0, 4200.0, 3300.0])
```

### Alcance (*scope*)

Las variables creadas **dentro** de una función son **locales**: nacen al invocarla y mueren al terminar; afuera no existen. Las creadas **fuera** son **globales**: la función puede leerlas, pero no modificarlas directamente (intentarlo produce `UnboundLocalError`). La forma correcta de "modificar" un valor externo es pasarlo como parámetro y devolver el resultado.

Desarrollo completo —incluidos los dos errores típicos (`NameError` al usar una variable local afuera, `UnboundLocalError` al intentar modificar una global) y el pipeline de limpieza completo escrito con funciones (`limpiar_registro`, `esta_completo`, `promedio_por`)— en [[funciones, parametros y alcance]].

> [!info] Puente con Estadística
> `promedio_por(registros, clave_grupo, clave_valor)` —una función de dos líneas que agrupa y promedia sobre cualquier campo— responde exactamente el tipo de pregunta que estructura [[02 - El estudio de la variabilidad]]: cómo varía una medida entre grupos. Es el mismo `group by` que en Pandas es una línea (`df.groupby(...)`, ver [[06 - Agregacion y groupby]]), escrito acá a mano para ver qué hace por dentro.

---

## 4. Recursión

Una función **recursiva** se llama a sí misma. Sirve para problemas que se definen en términos de sí mismos: si sé resolver una versión más chica del problema, puedo resolver la grande. Necesita siempre dos partes: un **caso base** (la situación tan simple que se resuelve directo) y un **caso recursivo** (reducir el problema y llamarse de nuevo).

```python
def factorial(n):
    if n <= 1:                    # CASO BASE
        return 1
    return n * factorial(n - 1)   # CASO RECURSIVO

print([factorial(i) for i in range(6)])   # [1, 1, 2, 6, 24, 120]
```

Cada llamada queda "esperando" en la **pila de llamadas** hasta que la de adentro termine; sin caso base (o si el caso recursivo no se acerca a él), Python corta a las ~1000 llamadas con `RecursionError` — el equivalente recursivo de un `while` infinito.

**Fibonacci** ilustra el problema central de la recursión "ingenua": la versión directa recalcula el mismo valor una y otra vez, con un costo que crece **exponencialmente** (para `F(30)`, casi 2,7 millones de llamadas). La solución es la **memoización**: guardar cada resultado ya calculado en un diccionario, para no repetirlo.

Desarrollo completo —el diagrama de la pila de llamadas, la tabla exacta de cantidad de llamadas por `n`, el código de `fibonacci_memo`, y por qué casi todo lo recursivo también se puede escribir como bucle— en [[recursion y memoizacion]].

> [!tip] ¿Para qué sirve entonces la recursión, si un bucle suele ser más eficiente?
> Para problemas cuya **estructura** es recursiva: árboles y grafos, donde cada nodo tiene hijos que a su vez son árboles (clase 3). Esto importa directamente en minería de datos: **un árbol de decisión es un árbol**, y se construye y se recorre recursivamente.

---

## 5. Cierre

### Lo que vimos hoy

- **Condicionales**: `if`/`elif`/`else`, la sangría como sintaxis, el orden de las condiciones, `is None` para distinguir faltantes de ceros.
- **Bucles**: `for` sobre colecciones, `range()`, `enumerate()`, `zip()`, el patrón acumulador, `break`/`continue`, `while` y su riesgo de no terminar.
- **Comprensiones de listas**: transformar y filtrar en una línea.
- **Funciones**: `def`, parámetros, valores por defecto, `return`, docstrings, devolver tuplas, y el alcance local vs. global.
- **Recursión**: caso base y caso recursivo, la pila de llamadas, factorial y Fibonacci, el costo exponencial y la memoización.

### Tres ideas para llevarse

1. **El código elegante no es necesariamente eficiente.** Fibonacci recursivo son tres líneas hermosas y casi 2,7 millones de llamadas para un solo valor.
2. **Las funciones son la unidad de reutilización.** `promedio_por` respondió tres preguntas distintas sin cambiar una línea.
3. **Todo bucle y toda recursión necesita una condición de salida.** `while` sin salida es un bucle infinito; recursión sin caso base es un `RecursionError`.

---

## Conceptos para desarrollar en notas aparte
- [[condicionales y evaluacion de verdad]]
- [[bucles for, while y el patron acumulador]]
- [[comprensiones de listas]]
- [[funciones, parametros y alcance]]
- [[recursion y memoizacion]]

## Preguntas de repaso
1. ¿Por qué el siguiente código da un resultado incorrecto sin lanzar ningún error, y cómo se corrige?
   ```python
   masa = 5500
   if masa > 3500:
       categoria = "mediano"
   elif masa > 4000:
       categoria = "grande"
   elif masa > 5000:
       categoria = "muy grande"
   ```
2. ¿Por qué `if masa:` no es una forma segura de preguntar "¿falta el dato?", y qué hay que escribir en su lugar?
3. Si una función no tiene `return`, ¿qué devuelve al invocarla? ¿Qué diferencia práctica tiene eso frente a una función que sí tiene `return`?
4. ¿Por qué `contador = contador + 1` dentro de una función produce `UnboundLocalError` si `contador` fue definida afuera? ¿Cuál es la forma correcta de lograr el mismo efecto?
5. ¿Cuáles son las dos partes que toda función recursiva necesita, y qué pasa si falta alguna? ¿Por qué la versión recursiva directa de Fibonacci es tan lenta, y qué técnica lo soluciona?

## Preguntas que me quedaron
-
-

## Para la próxima clase
**Clase 3 — Estructuras no lineales y complejidad algorítmica.** Cierra las estructuras de datos con **árboles y grafos** (donde la recursión de hoy es indispensable) y le pone nombre formal a lo que se viene observando desde la clase 1: la **notación Big O**.

## Actividad
Consigna en **`Actividad_Clase2.ipynb`** (aula de Moodle): un pipeline de limpieza de datos escrito íntegramente con funciones propias (sin Pandas ni NumPy), más un ejercicio de recursión y su costo. Se entrega antes del viernes 14 de agosto.
