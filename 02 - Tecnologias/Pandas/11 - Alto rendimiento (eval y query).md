---
titulo: "Pandas - Alto rendimiento (eval y query)"
materia: Pandas
tipo: apunte
tags:
  - pandas
  - tecnologias
  - python
  - tema/performance
fuente: "pandas — Enhancing performance, eval()/query() (pandas.pydata.org/docs/user_guide/enhancingperf.html); Python Data Science Handbook (Jake VanderPlas) — Parte III"
---

# Alto rendimiento: `eval` y `query`

## El problema que resuelven

Una operación compuesta como `df1 + df2 + df3 + df4` no se calcula de una sola vez: Pandas arma **arrays temporarios intermedios** en cada paso (`df1 + df2`, después `+ df3`, después `+ df4`), y eso cuesta memoria y tiempo extra en DataFrames grandes. `eval()` y `query()` evitan esos intermedios calculando la expresión completa de una — usan por debajo la librería `NumExpr`.

```python
pd.eval('df1 + df2 + df3 + df4')   # mismo resultado que df1 + df2 + df3 + df4, sin los intermedios
```

## `df.eval()`: expresiones usando nombres de columna

`DataFrame.eval()` deja escribir una expresión tratando **cada columna como si fuera una variable**, sin repetir `df["..."]` en cada término:

```python
df = pd.DataFrame({'A': [1, 2, 3], 'B': [4, 5, 6], 'C': [7, 8, 9]})

df.eval('(A + B) / (C - 1)')   # en vez de: (df['A'] + df['B']) / (df['C'] - 1)
# 0    0.833333
# 1    1.000000
# 2    1.125000
# dtype: float64
```

**También sirve para crear o modificar una columna**, con `inplace=True`:

```python
df.eval('D = (A + B) / C', inplace=True)   # crea la columna D
df
#    A  B  C         D
# 0  1  4  7  0.714286
# 1  2  5  8  0.875000
# 2  3  6  9  1.000000
```

**Variables locales de Python** (no columnas) se marcan con `@`:

```python
promedio_c = df['C'].mean()   # 8.0
df.eval('A + @promedio_c')
# 0     9.0
# 1    10.0
# 2    11.0
# dtype: float64
```

## `df.query()`: la versión legible del filtrado booleano

Filtrar con máscaras booleanas (ver [[06 - Comparaciones, mascaras y filtrado booleano]] de NumPy) funciona, pero se vuelve difícil de leer con varias condiciones:

```python
df[(df.A < 3) & (df.B < 5)]        # funciona, pero hay que repetir "df." en cada condición
#    A  B  C         D
# 0  1  4  7  0.714286

df.query('A < 3 and B < 5')         # mismo resultado, más legible
#    A  B  C         D
# 0  1  4  7  0.714286

df.query('A < @promedio_c')         # también acepta @variables -> las 3 filas, porque A siempre es < 8.0
```

> [!tip] `query()` es al filtrado lo que `eval()` es al cálculo
> Mismo mecanismo (expresiones como texto, evaluadas con NumExpr), aplicado a dos tareas distintas: `eval()` calcula, `query()` filtra filas.

## Cuándo realmente conviene usarlos

> [!warning] No son automáticamente más rápidos
> Con DataFrames chicos, el método tradicional (`df['A'] + df['B']`) suele ser **igual de rápido o más rápido** que `eval`/`query` — armar la expresión como string también tiene su costo. La ganancia real aparece con DataFrames **grandes**, donde evitar los arrays intermedios ahorra memoria de forma notoria (y a veces, de paso, tiempo). El beneficio principal es la **memoria ahorrada** y una sintaxis más clara, no una promesa general de velocidad.

## Relacionado
- [[01 - Introduccion a Series y DataFrame]]
- [[06 - Comparaciones, mascaras y filtrado booleano]]
- [[03 - Operaciones y alineacion de datos]]
