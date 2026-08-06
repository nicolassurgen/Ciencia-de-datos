---
titulo: "Pandas - Combinar datasets: concat, merge, join"
materia: Pandas
tipo: apunte
tags:
  - pandas
  - tecnologias
  - python
  - tema/combinar-datos
fuente: "Python Data Science Handbook (Jake VanderPlas) — Parte III"
---

# Combinar datasets: concat, merge, join

En la práctica los datos casi nunca vienen en una sola tabla — hay que juntar varias. Pandas separa esto en dos operaciones con lógicas distintas.

## `pd.concat`: apilar tablas

Para cuando las tablas tienen (más o menos) las **mismas columnas** y lo que querés es apilarlas una debajo de la otra (o una al lado de la otra):

```python
pd.concat([df1, df2])                 # apila filas (por defecto, axis=0)
pd.concat([df1, df2], axis=1)         # pega columnas, alineando por índice
```

Es la versión de Pandas de [[02 - Indexado, slicing y forma de los arrays|np.concatenate]] de NumPy, con la misma lógica de `axis`.

> [!warning] Índices duplicados
> `pd.concat` **no revisa** si los índices se repiten entre los DataFrames que estás uniendo — si `df1` y `df2` tienen ambos una fila con índice `0`, el resultado va a tener **dos filas** con índice `0`. Si eso no es lo que querés, usá `pd.concat([df1, df2], ignore_index=True)` para que reasigne un índice nuevo y consecutivo.

## `pd.merge`: combinar por una columna en común (como un JOIN de SQL)

Para cuando dos tablas describen **entidades relacionadas** a través de una columna clave (ej.: una tabla de empleados y otra de departamentos, unidas por `depto_id`):

```python
pd.merge(empleados, departamentos, on='depto_id')
```

Pandas detecta automáticamente qué filas corresponden entre sí según los valores de la columna en común — no hace falta que estén en el mismo orden ni tengan la misma cantidad de filas.

### Los 4 tipos de join

> [!important] `how=` decide qué hacer con las filas que no matchean
> | `how=` | Qué conserva |
> |---|---|
> | `'inner'` (default) | Solo las filas cuya clave está en **ambas** tablas |
> | `'outer'` | **Todas** las filas de ambas tablas; rellena con `NaN` donde falte (ver [[04 - Datos faltantes]]) |
> | `'left'` | Todas las filas de la tabla **izquierda**, aunque no tengan match en la derecha |
> | `'right'` | Todas las filas de la tabla **derecha** |

```python
pd.merge(empleados, departamentos, on='depto_id', how='left')
```

> [!tip] Cómo elegir `how`
> Preguntate: *"¿qué tabla es la que no quiero recortar?"* Si es la izquierda (por ejemplo, no querés perder ningún empleado aunque le falte el departamento), usá `'left'`. Si necesitás **todo**, sin perder nada de ninguna tabla, `'outer'`. `'inner'` (el default) es el más restrictivo: solo te quedás con lo que aparece en las dos.

### Cuando las columnas clave se llaman distinto

```python
pd.merge(izq, der, left_on='id_empleado', right_on='id')
```

## `.join()`: como `merge`, pero por índice

```python
df1.join(df2)
```

Atajo de `merge` para el caso específico de combinar **por el índice** en vez de por una columna — útil cuando ya tenés dos DataFrames con el mismo tipo de índice (por ejemplo, ambos indexados por fecha, ver [[08 - Series de tiempo]]).

## Relacionado
- [[01 - Introduccion a Series y DataFrame]]
- [[04 - Datos faltantes]]
- [[02 - Indexado, slicing y forma de los arrays]]
