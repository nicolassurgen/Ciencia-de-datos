---
titulo: "Seaborn - Forma de los datos: long-form vs wide-form"
materia: Seaborn
tipo: apunte
tags:
  - seaborn
  - tecnologias
  - python
  - tema/introduccion
fuente: "seaborn.pydata.org (documentación oficial)"
---

# Forma de los datos: long-form vs wide-form

Antes de graficar nada, Seaborn espera que tu `DataFrame` tenga una forma particular. Entender esto de entrada te ahorra la mayoría de los `ValueError` confusos del principio.

## La forma que Seaborn quiere: *long-form* (datos "prolijos"/*tidy*)

> [!important] La regla de oro
> **Cada columna es una variable. Cada fila es una observación.** Es exactamente la [[01 - Como dar sentido a los datos|matriz de datos]] que ya viste en Estadística: individuos en las filas, variables en las columnas.

```python
tips.head()
#    total_bill   tip     sex  smoker  day    time  size
# 0       16.99  1.01  Female      No  Sun  Dinner     2
# 1       10.34  1.66    Male      No  Sun  Dinner     3
```

Cada fila es una observación (una mesa), cada columna una variable (`total_bill`, `tip`, `sex`...). Con los datos así, graficar es simplemente **nombrar** las columnas que querés:

```python
sns.relplot(data=tips, x="total_bill", y="tip", hue="smoker")
```

## La forma opuesta: *wide-form*

En una tabla *wide*, las variables no están nombradas en columnas — están **repartidas entre filas y columnas**. Ejemplo clásico: una tabla de pasajeros por mes y año, donde cada año es una columna:

```python
flights_wide
# month     1950  1951  1952  ...
# January    112   115   145  ...
# February   118   126   150  ...
```

Acá "año" no es una variable con nombre — es una dimensión de la tabla. Seaborn **puede** graficar esto, pero con mapeos fijos y mucho menos control:

```python
sns.relplot(data=flights_wide.transpose(), kind="line")   # funciona, pero es rígido
```

## Por qué Seaborn insiste en long-form

> [!definition] Por qué importa
> La propia documentación lo resume así: *"cuando sea posible, tratá de representar tus datos con una estructura long-form al emprender un análisis serio"*. Con datos long-form:
> - Podés **reasignar** qué variable va a `x`, `y`, `hue`, `col`, etc. con solo cambiar un nombre de columna — no hace falta reorganizar la tabla.
> - Un mismo formato sirve para 2 variables o para 20 — el wide-form se vuelve inmanejable apenas hay más de dos o tres.
> - Es **predecible**: siempre sabés qué gráfico vas a obtener a partir de qué mapeo. Con wide-form, distintas funciones de Seaborn interpretan la tabla de forma distinta según su estructura.

## De wide a long: `pd.melt()`

Cuando tu fuente de datos original viene en formato wide (muy común en Excel/CSV exportados de sistemas administrativos), la [[04 - Datos faltantes|herramienta de Pandas]] para convertirla es `melt()`:

```python
flights_long = flights_wide.melt(var_name="year", value_name="passengers", ignore_index=False)
```

`melt()` hace exactamente lo contrario de un `pivot_table()` ([[07 - Tablas dinamicas (pivot_table)|ya visto en Pandas]]): en vez de expandir una columna en varias, **apila** varias columnas en una sola, con otra columna nueva que registra de cuál venía cada valor.

> [!tip] Diagnóstico rápido
> Si para graficar algo en Seaborn te encontrás escribiendo `.T` (transponer), `.reset_index()` sin necesidad clara, o pasando arrays sueltos en vez de `data=df, x="...", y="..."` — es una señal de que tus datos están en wide-form y conviene pasarlos por `melt()` primero.

## Relacionado
- [[01 - Como dar sentido a los datos]]
- [[01 - Introduccion a Series y DataFrame]]
- [[07 - Tablas dinamicas (pivot_table)]]
- [[01 - Introduccion y primer grafico]]
