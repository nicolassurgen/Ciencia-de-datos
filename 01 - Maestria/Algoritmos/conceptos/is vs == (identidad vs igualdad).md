---
titulo: "is vs == (identidad vs igualdad)"
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

# is vs == (identidad vs igualdad)

> [!definition] `==` — igualdad
> Pregunta si dos valores **son iguales** (mismo contenido), aunque sean objetos distintos en memoria.

> [!definition] `is` — identidad
> Pregunta si dos nombres apuntan **al mismo objeto** en memoria (mismo `id()`), no solo a valores iguales.

## Por qué `None` se compara con `is`

```python
sexo = None
print(sexo is None)    # True  -> forma recomendada
print(sexo == None)    # funciona, pero NO es lo recomendado
```

`None` es **único**: existe una sola vez en todo el programa, así que preguntar por identidad (`is None`) es más directo y es la convención de la comunidad Python (`PEP 8`).

## Donde la diferencia se vuelve visible: la copia compartida de listas

```python
a = [1, 2, 3]
b = a          # b NO es una copia: apunta al mismo objeto que a
b.append(4)
print(a)       # [1, 2, 3, 4]  <- a también cambió
print(a is b)  # True  -> son el mismo objeto
print(a == b)  # True  -> además tienen el mismo contenido
```

Si en cambio se copia con `b = a.copy()`, `a == b` sigue siendo `True` (mismo contenido) pero `a is b` pasa a ser `False` (son objetos distintos). El fenómeno de que dos nombres compartan el mismo objeto (como `a` y `b` antes de copiar) tiene nombre propio: **aliasing** — ver [[mutabilidad e inmutabilidad]] para el detalle completo de por qué esto importa con listas.

## Regla práctica

- Usá `==` para comparar **valores** (lo habitual: `edad == 30`, `nombre == "Ana"`).
- Usá `is` solo para comparar **identidad**, principalmente con `None`, `True` y `False`.

## Puente con Tecnologías

Con arrays de NumPy, `==` se vuelve **todavía más distinto** de lo que parece acá: `array1 == array2` no da un solo `True`/`False`, da un **array booleano** elemento por elemento (ver [[06 - Comparaciones, mascaras y filtrado booleano]]). Por eso `if array:` tira un error de "*truth value ambiguous*" — Python no sabe si evaluar la identidad, la igualdad completa, o cuál de los elementos del array.

## Relacionado
- [[01 - Introduccion a la programacion]]
- [[mutabilidad e inmutabilidad]]
- [[datos faltantes y None]]
- [[06 - Comparaciones, mascaras y filtrado booleano]]
