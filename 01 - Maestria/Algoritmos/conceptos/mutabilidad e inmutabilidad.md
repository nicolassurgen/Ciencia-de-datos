---
titulo: Mutabilidad e inmutabilidad
materia: Algoritmos
tipo: concepto
tags:
  - algoritmos
  - maestria
  - concepto
  - python
  - tema/introduccion
fecha: 2026-08-03
---

# Mutabilidad e inmutabilidad

> [!definition] Mutable
> Un objeto es **mutable** si su contenido puede **cambiar después de creado**, sin crear un objeto nuevo. Ejemplo: las **listas** (`[ ]`) y los **diccionarios** (`{k: v}`).

> [!definition] Inmutable
> Un objeto es **inmutable** si, una vez creado, su contenido **no puede modificarse**. Cualquier "cambio" en realidad crea un objeto nuevo. Ejemplo: las **tuplas** (`( )`), los `str`, los `int`, los `float`.

## Mutable: listas

```python
m = [39.1, 39.5, 40.3]
m[0] = 38.0          # se puede reasignar una posición
m.append(36.7)       # se puede agregar
```

## Inmutable: tuplas

```python
coordenada = (-34.6, -58.4)
coordenada[0] = 0.0   # TypeError: no admite asignación
```

## ¿Para qué querríamos algo que no se puede cambiar?

1. **Seguridad** — si un dato no debe cambiar (una coordenada, una fecha de nacimiento), la inmutabilidad lo garantiza.
2. **Velocidad** — los objetos inmutables son más livianos y rápidos de manejar.
3. **Uso como clave de diccionario** — solo los objetos **hasheables** (inmutables) pueden ser clave de un `dict` o elemento de un `set`. Ver [[hashing y hashabilidad]].

> [!tip] Regla práctica
> Colección de *varias cosas del mismo tipo que van a cambiar* → **lista**. *Un registro con campos fijos* → **tupla**.

> [!note] Dos tipos de métodos: accessor y mutator
> Vocabulario útil para nombrar la diferencia: un método **accessor** *lee* el objeto sin cambiarlo (`str.upper()`, que devuelve un string nuevo); un método **mutator** *cambia* el objeto en el lugar (`list.append()`, `list.sort()`, que no devuelven nada útil — devuelven `None` — porque su trabajo es mutar, no producir un valor nuevo). Distinguir cuál es cuál evita un error común: escribir `m = m.append(x)` esperando el resultado, cuando `append` ya modificó `m` y devolvió `None`. *Fuente: [[Data Structures and Algorithms with Python]], cap. 1.*

## La trampa de la copia compartida

Asignar una lista (mutable) a otra variable **no crea una copia**: ambas apuntan al **mismo objeto** en memoria.

```python
a = [1, 2, 3]
b = a          # NO es una copia: a y b son el mismo objeto
b.append(4)
print(a)       # [1, 2, 3, 4]  <- ¡a también cambió!
```

La forma correcta de copiar: `b = a.copy()` (o `list(a)`, o `a[:]`). Esta trampa **no existe** con tipos inmutables: como no se pueden modificar "in place", no hay riesgo de que un cambio se propague a otra variable por accidente. Ver [[is vs == (identidad vs igualdad)]]: `a is b` sería `True` en el ejemplo de arriba, justamente porque comparten el mismo objeto.

> [!important] El mismo fenómeno tiene nombre: *aliasing*
> Que dos variables distintas refieran al **mismo objeto** en memoria se llama **aliasing** (`a` es un *alias* de `b`, o viceversa). No es un defecto de Python: es consecuencia directa de que una variable es una **referencia** a un objeto, no una casilla que "contiene" el valor — asignar (`b = a`) copia la referencia, no el objeto. El aliasing es, según la bibliografía, *"una fuente común de errores"* precisamente porque no siempre es obvio cuándo dos nombres apuntan al mismo lugar. *Fuente: [[Algorithms-4th-Edition-By-Robert Sedgewick and Kevin Wayne]], cap. 1.*

### La misma trampa, pasando un mutable a una función

El aliasing no aparece solo con `b = a`: pasar una lista o un diccionario como **argumento** de una función también comparte el objeto, no lo copia. Si la función lo muta adentro, el cambio se ve afuera:

```python
def agregar_elemento(lista, elemento):
    lista.append(elemento)   # muta el objeto recibido

datos = [1, 2, 3]
agregar_elemento(datos, 4)
print(datos)   # [1, 2, 3, 4]  <- cambió, aunque nunca se reasignó "datos" directamente
```

Esto **no** es lo mismo que el `UnboundLocalError` de reasignar una variable dentro de una función (ver [[funciones, parametros y alcance]]): ahí se intenta cambiar **a qué objeto apunta el nombre**, y falla; acá se cambia **el contenido del objeto al que ya apunta**, y funciona — porque es el mismo objeto que tiene la variable de afuera. La distinción entre "reasignar" y "mutar" es la que separa ambos comportamientos. *Fuente: [[Python-for-Data-Analysis]], cap. 3.*

### Copia superficial (shallow) vs. copia profunda (deep)

`a.copy()` resuelve la trampa de arriba **solo en el primer nivel**. Si la lista contiene a su vez objetos mutables (listas de listas, diccionarios anidados), la copia superficial (*shallow copy*) copia el contenedor externo, pero los objetos internos siguen siendo **compartidos**:

```python
import copy

original = [ [1, 2], [3, 4] ]
superficial = original.copy()      # copia "de un nivel"
superficial[0].append(99)
print(original)                    # [ [1, 2, 99], [3, 4] ]  <- ¡también cambió!

profunda = copy.deepcopy(original)  # copia recursiva, todos los niveles
profunda[0].append(100)
print(original)                    # [ [1, 2, 99], [3, 4] ]  <- esta vez no cambia
```

La lista de diccionarios que ya se usa para representar un dataset (ver [[lista de diccionarios y JSON]]) es exactamente esta situación: copiar la lista externa con `.copy()` **no** protege los diccionarios de cada registro de ser mutados por accidente — para eso hace falta `copy.deepcopy()`. *Fuente: [[Data Structures and Algorithms with Python]], cap. 4.*

## Puente con Tecnologías

Esta misma trampa reaparece en NumPy, pero al revés: un slice de un array (`x[:2]`) es una **vista**, no una copia — modificarla modifica el array original (ver [[02 - Indexado, slicing y forma de los arrays]]). Y la regla de "solo lo inmutable puede ser clave" es la razón por la que el `Index` de un DataFrame de Pandas es inmutable (ver [[01 - Introduccion a Series y DataFrame]]): permite que varias `Series` lo compartan sin riesgo de que una lo modifique por accidente.

## Relacionado
- [[01 - Introduccion a la programacion]]
- [[listas, tuplas, diccionarios y conjuntos]]
- [[is vs == (identidad vs igualdad)]]
- [[hashing y hashabilidad]]
- [[02 - Indexado, slicing y forma de los arrays]]
- [[01 - Introduccion a Series y DataFrame]]
