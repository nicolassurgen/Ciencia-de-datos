---
titulo: Funciones, parámetros y alcance
materia: Algoritmos
tipo: concepto
tags:
  - algoritmos
  - maestria
  - concepto
  - python
  - tema/funciones
fecha: 2026-08-08
---

# Funciones, parámetros y alcance

La lógica de "convertir texto a número, o `None` si el campo está vacío" aparece varias veces al preparar un dataset: una vez por cada columna numérica. Escribirla suelta cada vez tiene un costo silencioso: si mañana cambia el criterio de conversión, hay que corregirla en todos los lugares donde se copió, y es fácil olvidarse de uno. Una función resuelve ese problema dándole nombre al procedimiento.

> [!definition] Función
> Procedimiento empaquetado bajo un nombre, para invocarlo cuantas veces haga falta. Tres beneficios: **no repetir código** (se escribe una vez, se usa muchas), **un solo lugar para corregir** un error, y **legibilidad** (`limpiar_masa(x)` dice qué hace; cinco líneas sueltas, no).

## Definir e invocar

```python
def a_numero(texto):
    """Convierte texto a float. Devuelve None si el campo está vacío."""
    if texto == "":
        return None
    return float(texto)

print(a_numero("39.1"))   # 39.1
print(a_numero(""))       # None
```

| Parte | En el ejemplo | Qué es |
|---|---|---|
| `def` | `def` | Palabra clave: "acá empieza una función" |
| Nombre | `a_numero` | Cómo se invoca. Conviene que sea un **verbo** |
| Parámetros | `(texto)` | Los datos de entrada |
| `:` y sangría | | Delimitan el cuerpo, igual que en `if`/`for` |
| *Docstring* | `"""Convierte..."""` | Documenta qué hace. Opcional pero muy recomendable |
| `return` | `return None` | Qué devuelve. **Termina la función inmediatamente** |

## `return` vs. `print`: el punto que más confunde

**`return` corta la ejecución**: nada de lo que esté después de un `return` ya ejecutado corre. **Una función sin `return` devuelve `None`** — si una función imprime pero no retorna, no se puede usar su resultado.

```python
def sumar_mal(a, b):
    print(a + b)        # imprime, pero NO devuelve

def sumar_bien(a, b):
    return a + b        # devuelve el valor

x = sumar_mal(2, 3)     # imprime: 5
print(x)                 # None  <- x quedó vacío
y = sumar_bien(2, 3)
print(y, y * 10)         # 5 50  <- se puede seguir operando
```

> [!important] Regla práctica
> `print` es para **mostrarle** algo a una persona. `return` es para **entregarle** un valor al programa. Casi siempre se quiere `return`.

## Parámetros, valores por defecto y argumentos por nombre

```python
def describir(especie, masa, unidad="g"):
    """unidad tiene un valor POR DEFECTO: si no se pasa, vale 'g'."""
    return f"{especie}: {masa} {unidad}"

print(describir("Adelie", 3750))                  # Adelie: 3750 g   (usa el default)
print(describir("Gentoo", 5.1, "kg"))              # Gentoo: 5.1 kg   (lo sobreescribe)
print(describir(masa=4500, especie="Chinstrap"))   # Chinstrap: 4500 g (por nombre, cualquier orden)
```

Pasar argumentos **por nombre** aclara el código cuando hay varios parámetros:

```python
entrenar(datos, 0.8, True, 42)                              # ¿qué es cada cosa?
entrenar(datos, proporcion=0.8, mezclar=True, semilla=42)   # se entiende solo
```

Los parámetros con valor por defecto van **siempre después** de los que no lo tienen.

## Devolver varios valores

```python
def resumir(valores):
    """Devuelve (mínimo, máximo, promedio) de una lista de números."""
    return min(valores), max(valores), sum(valores) / len(valores)

minimo, maximo, promedio = resumir([3750.0, 4200.0, 3300.0])
print(f"{minimo:.1f} {maximo:.1f} {promedio:.1f}")   # 3300.0 4200.0 3750.0
```

La función devuelve una **tupla**, que se reparte con el mismo desempaquetado visto en la clase 1 con listas y diccionarios.

> [!tip] Alternativa: devolver un diccionario
> Cuando son muchos los valores a devolver, una tupla obliga a recordar el **orden** exacto en el que se desempaquetan. Devolver un diccionario evita ese problema, a costa de un poco más de código al construirlo:
> ```python
> def resumir_dict(valores):
>     return {"minimo": min(valores), "maximo": max(valores), "promedio": sum(valores)/len(valores)}
>
> r = resumir_dict([3750.0, 4200.0, 3300.0])
> print(r["promedio"])   # 3750.0  <- se accede por nombre, no por posición
> ```
> *Fuente: [[Python-for-Data-Analysis]], cap. 3.*

## Alcance (*scope*): local vs. global

- Las variables creadas **dentro** de una función son **locales**: nacen al invocarla y mueren al terminar. Afuera no existen.
- Las creadas **fuera** son **globales**: la función puede **leerlas**, pero no modificarlas directamente.

> [!note] El nombre completo: alcance LEGB
> Python busca un nombre en cuatro niveles, en este orden: **L**ocal (dentro de la función actual) → **E**nclosing (si la función está anidada dentro de otra, el alcance de la función que la contiene) → **G**lobal (el módulo) → **B**uilt-in (funciones y nombres propios de Python, como `print` o `len`). Local y Global son los dos niveles que usan las funciones de esta nota; Enclosing aparece cuando una función se define dentro de otra (una función auxiliar interna, por ejemplo); Built-in es la razón por la que conviene evitar nombrar una variable propia `list` o `int` — taparía el nombre incorporado de Python en ese alcance. *Fuente: [[Data Structures and Algorithms with Python]], cap. 3.*

```python
def calcular():
    resultado_local = 42
    return resultado_local

print(calcular())        # 42
print(resultado_local)   # NameError: name 'resultado_local' is not defined
```

> [!important] Esto es una ventaja, no una limitación
> Que las variables locales mueran al terminar la función significa que la función es una caja razonablemente cerrada: se puede entender mirando solo su código, sin miedo a que le esté pisando variables al resto del programa.

```python
UMBRAL = 4000     # variable global

def es_grande(masa):
    return masa > UMBRAL     # la función PUEDE LEER la global

print(es_grande(4500))   # True
```

```python
contador = 0

def incrementar_mal():
    contador = contador + 1     # intenta modificar la global: falla
    return contador

incrementar_mal()   # UnboundLocalError: cannot access local variable 'contador'...
```

Al **asignarle** un valor dentro de la función, Python considera a `contador` **local** en todo el cuerpo de la función — y entonces intenta leerla antes de que exista. Se puede forzar con `global contador`:

```python
contador = 0

def incrementar_forzado():
    global contador          # avisa: "contador de acá es la global, no una local nueva"
    contador = contador + 1
```

pero casi nunca conviene — incluso la bibliografía lo desaconseja explícitamente: *"generalmente se desalienta el uso de `global`... puede ser señal de que hace falta una estructura distinta"*. Las funciones que modifican estado global son difíciles de seguir y de testear. La forma correcta es pasar el valor y devolverlo: *Fuente: [[Python-for-Data-Analysis]], cap. 3.*

```python
def incrementar_bien(valor):
    return valor + 1

contador = 0
contador = incrementar_bien(contador)
contador = incrementar_bien(contador)
print(contador)   # 2
```

## Las funciones son objetos como cualquier otro

En Python una función se puede guardar en una variable, meter en una lista, y pasar como argumento de otra función — igual que un número o un string:

```python
def sin_espacios(s):
    return s.strip()

def mayusculas(s):
    return s.upper()

operaciones = [sin_espacios, mayusculas]   # una lista de funciones, sin llamarlas (sin paréntesis)

texto = "  hola  "
for operacion in operaciones:
    texto = operacion(texto)
print(texto)   # HOLA
```

Esto abre la puerta a **funciones anónimas** (`lambda`) para casos de una sola línea, donde definir la función con `def` y ponerle nombre sería excesivo — típicamente como argumento de otra función:

```python
palabras = ["banana", "kiwi", "frutilla"]
palabras.sort(key=lambda p: len(p))   # ordenar por longitud, sin escribir una función aparte
print(palabras)   # ['kiwi', 'banana', 'frutilla']
```

`lambda p: len(p)` es equivalente a `def f(p): return len(p)`, pero sin nombre y en una sola expresión — no admite `if`/`for` completos ni varias líneas, solo una expresión que se evalúa y se devuelve. *Fuente: [[Python-for-Data-Analysis]], cap. 3.*

## Puente con Estadística

`resumen_por(registros, clave_grupo, clave_valor)` — una función que agrupa y agrega, escrita a mano con diccionarios y el patrón acumulador de [[bucles for, while y el patron acumulador]] — es exactamente lo que hace un `group by`: la misma pregunta ("¿cómo varía esta medida entre grupos?") que estructura buena parte de [[02 - El estudio de la variabilidad]]. En Pandas, la misma idea es `df.groupby(...)` (ver [[06 - Agregacion y groupby]]); acá se ve qué hace por dentro.

## Relacionado
- [[02 - Programacion imperativa]]
- [[bucles for, while y el patron acumulador]]
- [[recursion y memoizacion]]
- [[06 - Agregacion y groupby]]
