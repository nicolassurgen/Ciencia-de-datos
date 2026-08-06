---
titulo: "NumPy - Comparaciones, máscaras y filtrado booleano"
materia: NumPy
tipo: apunte
tags:
  - numpy
  - tecnologias
  - python
  - tema/filtrado
fuente: "Python Data Science Handbook (Jake VanderPlas) — Parte II"
---

# Comparaciones, máscaras y filtrado booleano

Esta es, en la práctica, la herramienta que más vas a usar para **responder preguntas sobre tus datos**: "¿cuántos valores superan tal umbral?", "dame solo las filas donde tal condición se cumple".

## Los operadores de comparación también son ufuncs

```python
x = np.array([1, 2, 3, 4, 5])

x < 3     # array([ True,  True, False, False, False])
x == 3    # array([False, False,  True, False, False])
x >= 3
```

Igual que `+` o `*` (ver [[03 - Ufuncs y operaciones vectorizadas]]), cada operador de comparación aplica **elemento a elemento** sobre todo el array y devuelve un array de `bool` del mismo tamaño.

## Contar y verificar

```python
np.count_nonzero(x < 3)   # 2  -> cuántos son True
np.sum(x < 3)              # 2  -> equivalente: True vale 1, False vale 0

np.any(x > 4)               # True  -> ¿hay AL MENOS uno que cumpla?
np.all(x > 0)               # True  -> ¿TODOS cumplen?
```

`np.sum()` sobre un array booleano es un patrón que vas a ver todo el tiempo: es la forma vectorizada de "contar cuántos cumplen la condición" — el equivalente de una frecuencia absoluta (ver [[distribución de frecuencias]] de Estadística).

## Máscaras booleanas: filtrar datos de verdad

Acá es donde se vuelve realmente útil: un array booleano se puede usar como **índice** para quedarte solo con los elementos que cumplen la condición.

```python
x[x < 3]     # array([1, 2])   -> solo los elementos que cumplen x < 3
```

```python
lluvia = np.array([0, 5, 12, 0, 0, 3, 20])   # mm de lluvia por día
lluvia[lluvia > 0]              # solo los días que llovió
lluvia[lluvia > 0].mean()       # promedio de lluvia, contando SOLO los días de lluvia
np.sum(lluvia == 0)             # cantidad de días secos
```

> [!important] Esto es exactamente lo que hacías "a mano" en Algoritmos
> Compará con el patrón de [[datos faltantes y None]]: `masas = [p["masa_g"] for p in pinguinos if p["masa_g"] is not None]`. La máscara booleana de NumPy es la versión vectorizada de ese mismo `if` dentro de una comprensión de lista — pero sin el loop explícito, y mucho más rápida sobre datos grandes.

## Combinar condiciones: `&`, `|`, `~` (no `and`, `or`, `not`)

```python
(lluvia > 0) & (lluvia < 10)    # Y lógico, elemento a elemento
(lluvia == 0) | (lluvia > 15)   # O lógico
~(lluvia > 0)                    # negación
```

> [!warning] `and`/`or`/`not` de Python NO funcionan elemento a elemento
> `and`, `or` y `not` de Python esperan **un solo valor de verdad**, no un array entero — y van a tirar un `ValueError` ("*the truth value of an array is ambiguous*") si los usás sobre un array con más de un elemento. Para arrays, siempre `&` (y), `|` (o), `~` (no) — los mismos operadores bit a bit que ya usás con conjuntos en Python (ver [[listas, tuplas, diccionarios y conjuntos]] de Algoritmos: `&` y `|` para intersección/unión de sets).
>
> Y ojo con la **precedencia**: `&` y `|` se evalúan antes que `<`/`>`/`==`, así que las condiciones individuales necesitan paréntesis: `(lluvia > 0) & (lluvia < 10)`, no `lluvia > 0 & lluvia < 10`.

## Relacionado
- [[03 - Ufuncs y operaciones vectorizadas]]
- [[07 - Indexado fancy y ordenamiento]]
- [[datos faltantes y None]]
- [[distribución de frecuencias]]
