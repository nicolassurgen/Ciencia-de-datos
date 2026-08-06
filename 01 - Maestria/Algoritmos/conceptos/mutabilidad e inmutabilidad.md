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

## La trampa de la copia compartida

Asignar una lista (mutable) a otra variable **no crea una copia**: ambas apuntan al **mismo objeto** en memoria.

```python
a = [1, 2, 3]
b = a          # NO es una copia: a y b son el mismo objeto
b.append(4)
print(a)       # [1, 2, 3, 4]  <- ¡a también cambió!
```

La forma correcta de copiar: `b = a.copy()` (o `list(a)`, o `a[:]`). Esta trampa **no existe** con tipos inmutables: como no se pueden modificar "in place", no hay riesgo de que un cambio se propague a otra variable por accidente. Ver [[is vs == (identidad vs igualdad)]]: `a is b` sería `True` en el ejemplo de arriba, justamente porque comparten el mismo objeto.

## Puente con Tecnologías

Esta misma trampa reaparece en NumPy, pero al revés: un slice de un array (`x[:2]`) es una **vista**, no una copia — modificarla modifica el array original (ver [[02 - Indexado, slicing y forma de los arrays]]). Y la regla de "solo lo inmutable puede ser clave" es la razón por la que el `Index` de un DataFrame de Pandas es inmutable (ver [[01 - Introduccion a Series y DataFrame]]): permite que varias `Series` lo compartan sin riesgo de que una lo modifique por accidente.

## Relacionado
- [[01 - Introduccion a la programacion]]
- [[listas, tuplas, diccionarios y conjuntos]]
- [[is vs == (identidad vs igualdad)]]
- [[hashing y hashabilidad]]
- [[02 - Indexado, slicing y forma de los arrays]]
- [[01 - Introduccion a Series y DataFrame]]
