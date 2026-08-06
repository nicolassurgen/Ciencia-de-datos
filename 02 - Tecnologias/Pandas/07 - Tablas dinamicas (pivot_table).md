---
titulo: "Pandas - Tablas dinámicas (pivot_table)"
materia: Pandas
tipo: apunte
tags:
  - pandas
  - tecnologias
  - python
  - tema/agregacion
fuente: "Python Data Science Handbook (Jake VanderPlas) — Parte III"
---

# Tablas dinámicas (pivot_table)

Si ya entendiste [[06 - Agregacion y groupby|groupby]], una tabla dinámica es un caso particular: **agrupar por dos variables a la vez** y mostrar el resultado como una grilla — filas para una variable, columnas para la otra. Es el mismo concepto que una tabla dinámica de Excel/Google Sheets.

## De groupby a pivot_table

Agrupar por dos claves con `groupby` es posible, pero el resultado queda "apilado":

```python
titanic.groupby(['sexo', 'clase'])['sobrevivio'].mean()
# sexo    clase
# mujer   1        0.97
#         2        0.92
#         3        0.50
# hombre  1        0.37
#         2        0.16
#         3        0.14
```

`pivot_table` hace exactamente ese cálculo, pero **reacomoda el resultado en una grilla** mucho más legible:

```python
titanic.pivot_table('sobrevivio', index='sexo', columns='clase')
# clase      1      2      3
# sexo
# mujer   0.97   0.92   0.50
# hombre  0.37   0.16   0.14
```

> [!important] Los 4 parámetros que definen una tabla dinámica
> ```python
> df.pivot_table(values, index, columns, aggfunc='mean')
> ```
> - **`values`** → qué columna resumir (por defecto, la media).
> - **`index`** → qué variable va en las **filas**.
> - **`columns`** → qué variable va en las **columnas**.
> - **`aggfunc`** → cómo resumir (`'mean'`, `'sum'`, `'count'`, o una lista de varias).

## Con más de una función de agregación

```python
titanic.pivot_table('sobrevivio', index='sexo', columns='clase', aggfunc=['mean', 'count'])
```

Te da, en la misma tabla, la tasa de supervivencia **y** la cantidad de pasajeros en cada combinación de sexo/clase — útil para no sacar conclusiones de un grupo con muy pocos casos.

## Agrupar una variable continua: `pd.cut`

Para usar como `index`/`columns` una variable numérica continua (edad, en vez de una categoría), primero hay que discretizarla en intervalos — el mismo concepto que los **intervalos de clase** de [[distribución de frecuencias]] en Estadística:

```python
edades = pd.cut(titanic['edad'], [0, 18, 40, 80])
titanic.pivot_table('sobrevivio', index=['sexo', edades], columns='clase')
```

## Totales de fila y columna: `margins=True`

```python
titanic.pivot_table('sobrevivio', index='sexo', columns='clase', margins=True)
```

Agrega una fila y una columna `'All'` con el promedio general — muy útil para tener el punto de referencia global al lado de cada grupo.

## Relacionado
- [[06 - Agregacion y groupby]]
- [[distribución de frecuencias]]
- [[01 - Introduccion a Series y DataFrame]]
