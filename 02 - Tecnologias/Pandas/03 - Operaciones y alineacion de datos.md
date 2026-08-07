---
titulo: Pandas - Operaciones y alineación de datos
materia: Pandas
tipo: apunte
tags:
  - pandas
  - tecnologias
  - python
  - tema/operaciones
fuente: "pandas — Essential basic functionality, arithmetic/data alignment (pandas.pydata.org/docs/user_guide/basics.html); Python Data Science Handbook (Jake VanderPlas) — Parte III"
---

# Operaciones y alineación de datos

## Las ufuncs de NumPy funcionan igual en Pandas

Todo lo que ya sabés de [[03 - Ufuncs y operaciones vectorizadas]] se traslada directo:

```python
poblacion / 1_000_000    # población en millones, vectorizado
# California    39.538223
# Texas         29.145505
# Florida       21.538187
# dtype: float64
```

## La diferencia clave: alineación automática por índice

Acá Pandas hace algo que NumPy no hace: cuando operás entre dos `Series` (o dos `DataFrame`), **alinea automáticamente por el índice**, no por posición.

```python
a = pd.Series({'California': 423967, 'Texas': 695662})
b = pd.Series({'California': 39538223, 'Texas': 29145505, 'Florida': 21538187})

a + b
# California    3.995790e+07
# Florida                NaN   <- 'Florida' no está en `a`
# Texas         2.984117e+07
```

> [!important] Alineación, no concatenación por posición
> Pandas junta los datos por **etiqueta de índice**, sin importar el orden en que aparecen ni si un índice le falta a alguna de las dos Series. Donde una etiqueta no existe en ambos lados, el resultado es `NaN` (ver [[04 - Datos faltantes]]) — Pandas prefiere avisarte con un faltante antes que adivinar mal o descartar datos en silencio.
>
> Esto es exactamente lo que necesitás cuando cruzás dos fuentes de datos que no están perfectamente sincronizadas (un CSV de censo y otro de superficie, por ejemplo) — no hace falta ordenar ni emparejar nada a mano.

## Completar los huecos que deja la alineación

Si preferís un valor por defecto en vez de `NaN` cuando falta una etiqueta de un lado:

```python
a.add(b, fill_value=0)
# California    3.995790e+07
# Florida       2.153819e+07   <- ahora usa el valor de b (21538187) en vez de NaN
# Texas         2.984117e+07
```

Cada operador tiene su versión "método" equivalente, que acepta `fill_value`: `+` → `.add()`, `-` → `.sub()`, `*` → `.mul()`, `/` → `.div()`.

## Operaciones entre DataFrame y Series: broadcasting por fila

```python
df = pd.DataFrame([[6, 9, 2, 6], [7, 4, 3, 7], [7, 2, 5, 4]], columns=list('ABCD'))

df - df.iloc[0]     # resta la PRIMERA FILA a cada fila del DataFrame
#    A  B  C  D
# 0  0  0  0  0
# 1  1 -5  1  1
# 2  1 -7  3 -2
```

Es el mismo [[05 - Broadcasting|broadcasting]] de NumPy: por defecto, la operación se alinea **por columna** y se repite fila por fila. Si necesitás que sea **por fila** en cambio, hay que ser explícito con `axis`:

```python
df.subtract(df['A'], axis=0)    # resta la columna 'A' a cada columna, fila por fila
#    A  B   C  D
# 0  0  3  -4  0
# 1  0 -3  -4  0
# 2  0 -5  -2 -3
```

Mismo parámetro `axis` que ya conocés de [[04 - Agregaciones y estadistica descriptiva]] en NumPy: `axis=0` señala la dirección de las filas.

## Relacionado
- [[03 - Ufuncs y operaciones vectorizadas]]
- [[05 - Broadcasting]]
- [[04 - Datos faltantes]]
- [[02 - Indexado y seleccion (loc, iloc)]]
