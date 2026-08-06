---
titulo: Pandas - Operaciones y alineación de datos
materia: Pandas
tipo: apunte
tags:
  - pandas
  - tecnologias
  - python
  - tema/operaciones
fuente: "Python Data Science Handbook (Jake VanderPlas) — Parte III"
---

# Operaciones y alineación de datos

## Las ufuncs de NumPy funcionan igual en Pandas

Todo lo que ya sabés de [[03 - Ufuncs y operaciones vectorizadas]] se traslada directo:

```python
np.exp(poblacion)
np.sqrt(area)
poblacion / 1_000_000    # población en millones, vectorizado
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
```

Cada operador tiene su versión "método" equivalente, que acepta `fill_value`: `+` → `.add()`, `-` → `.sub()`, `*` → `.mul()`, `/` → `.div()`.

## Operaciones entre DataFrame y Series: broadcasting por fila

```python
df = pd.DataFrame(np.random.randint(10, size=(3, 4)), columns=list('ABCD'))

df - df.iloc[0]     # resta la PRIMERA FILA a cada fila del DataFrame
```

Es el mismo [[05 - Broadcasting|broadcasting]] de NumPy: por defecto, la operación se alinea **por columna** y se repite fila por fila. Si necesitás que sea **por fila** en cambio, hay que ser explícito con `axis`:

```python
df.subtract(df['A'], axis=0)    # resta la columna 'A' a cada columna, fila por fila
```

Mismo parámetro `axis` que ya conocés de [[04 - Agregaciones y estadistica descriptiva]] en NumPy: `axis=0` señala la dirección de las filas.

## Relacionado
- [[03 - Ufuncs y operaciones vectorizadas]]
- [[05 - Broadcasting]]
- [[04 - Datos faltantes]]
- [[02 - Indexado y seleccion (loc, iloc)]]
