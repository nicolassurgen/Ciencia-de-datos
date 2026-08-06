---
titulo: "Pandas - Indexado y selección (loc, iloc)"
materia: Pandas
tipo: apunte
tags:
  - pandas
  - tecnologias
  - python
  - tema/indexado
fuente: "Python Data Science Handbook (Jake VanderPlas) — Parte III"
---

# Indexado y selección (loc, iloc)

Este es, probablemente, el tema de Pandas donde más tiempo se pierde al principio. La buena noticia: se resuelve casi del todo con dos palabras — `loc` e `iloc`.

## El problema que resuelven

```python
datos = pd.Series(['a', 'b', 'c'], index=[1, 3, 5])

datos[1]      # 'a'  -> ¿es la etiqueta 1, o la posición 1?
```

Con un índice de **enteros no consecutivos** como este, `datos[1]` es ambiguo a simple vista: Pandas lo resuelve usando la **etiqueta** (te da `'a'`, el elemento con índice `1`), pero `datos[1:3]` usa la **posición** (slicing por posición, como una lista). Esa inconsistencia es justo lo que `loc`/`iloc` vienen a eliminar.

> [!important] La regla que soluciona la ambigüedad para siempre
> - **`.loc[]`** → siempre por **etiqueta** (el valor del índice, tal cual aparece en `index`/`columns`).
> - **`.iloc[]`** → siempre por **posición** (un número entero, 0, 1, 2..., como en una lista o un array de NumPy — ver [[indexado y slicing]] de Algoritmos).
>
> Si tenés dudas sobre qué te va a devolver una selección, usá `loc`/`iloc` explícitamente. Nunca vas a estar en ambigüedad.

```python
datos.loc[1]      # 'a'   -> por etiqueta
datos.loc[1:3]    # incluye el 3 (a diferencia de slicing normal de Python!)

datos.iloc[1]     # 'b'   -> por posición (segundo elemento)
datos.iloc[1:3]   # NO incluye la posición 3 (slicing normal)
```

> [!warning] `.loc[a:b]` incluye el final; `.iloc[a:b]` no
> Es una inconsistencia real de Pandas, y vale la pena memorizarla así, tal cual: **`loc` es inclusivo en el límite superior, `iloc` no**. Es fácil de confundir porque en el resto de Python (listas, `range()`, `iloc`) el final siempre queda afuera.

## Seleccionar en un DataFrame

```python
estados.loc['California']              # la fila entera de California (por etiqueta)
estados.loc['California', 'area']      # celda puntual: fila, columna
estados.loc[:, 'area']                  # la columna 'area' completa
estados.loc[estados['population'] > 25_000_000]   # filtrar filas con una máscara booleana

estados.iloc[0]           # primera fila, por posición
estados.iloc[0, 1]        # fila 0, columna 1
estados.iloc[:3, :2]      # las primeras 3 filas, las primeras 2 columnas
```

El último ejemplo de `.loc` combina indexado con una [[06 - Comparaciones, mascaras y filtrado booleano|máscara booleana]] de NumPy — es exactamente el mismo mecanismo que `array[array > umbral]`, aplicado a un DataFrame entero.

## Acceder a una columna: el atajo

```python
estados['area']       # siempre funciona
estados.area           # atajo, funciona SI el nombre de columna es un identificador válido de Python
```

> [!tip] Preferí `estados['area']` sobre `estados.area`
> El atajo con punto es cómodo, pero falla silenciosamente en casos comunes: columnas con espacios (`'nivel educativo'`), que empiecen con número, o que coincidan con un método existente del DataFrame (`estados.count` te da el *método* `count`, no la columna "count"). `estados['area']` funciona siempre, sin sorpresas.

## Agregar o modificar una columna

```python
estados['densidad'] = estados['population'] / estados['area']
```

Operación vectorizada (ver [[03 - Ufuncs y operaciones vectorizadas]] de NumPy): se calcula fila por fila sin ningún loop explícito, y crea la columna si no existía o la reemplaza si ya existía.

## Relacionado
- [[01 - Introduccion a Series y DataFrame]]
- [[indexado y slicing]]
- [[06 - Comparaciones, mascaras y filtrado booleano]]
- [[03 - Operaciones y alineacion de datos]]
