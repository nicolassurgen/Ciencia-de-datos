---
titulo: Seaborn - Grids y comparaciones múltiples
materia: Seaborn
tipo: apunte
tags:
  - seaborn
  - tecnologias
  - python
  - tema/grids
fuente: "seaborn.pydata.org (documentación oficial)"
---

# Grids y comparaciones múltiples

Todo lo visto hasta acá comparaba variables **dentro** de un mismo gráfico (con `hue`, `size`, `style`). Esta nota es sobre repetir el **mismo** gráfico varias veces, para comparar entre subconjuntos o entre pares de variables de una sola vez.

## `FacetGrid`: la estratificación de Estadística, en forma de grilla

> [!important] Esto es literalmente [[estratificación|estratificar]], pero visual
> En Estadística viste que separar los datos por una variable (por máquina, por turno) puede revelar patrones que los datos "todos juntos" esconden. `FacetGrid` hace exactamente eso: un panel (subplot) por cada nivel de una variable categórica.

```python
g = sns.FacetGrid(tips, col="time")
g.map(sns.histplot, "tip")
```

`col=` reparte los paneles en columnas, `row=` en filas — combinando ambos obtenés una grilla de 2 variables categóricas a la vez, con una tercera opcional codificada en `hue=` dentro de cada panel.

En la práctica, **casi nunca armás un `FacetGrid` a mano**: las funciones de figura que ya conocés (`relplot`, `displot`, `catplot`) lo usan por dentro y exponen `col=`/`row=` directo:

```python
sns.relplot(data=tips, x="total_bill", y="tip", hue="smoker", col="time", row="sex")
```

Cuatro variables (`total_bill`, `tip`, `smoker`, `time`, `sex` — cinco, en realidad) en un solo gráfico, sin escribir ningún loop.

## `pairplot()` / `PairGrid`: todas las relaciones de a pares

```python
sns.pairplot(iris, hue="species")
```

Arma automáticamente una **matriz** de gráficos: cada variable numérica contra cada otra (scatterplots fuera de la diagonal) y la distribución de cada variable consigo misma (histogramas en la diagonal). Es la forma más rápida de hacer un primer barrido exploratorio de un dataset con varias variables cuantitativas — el punto de partida típico antes de decidir qué [[07 - Regresion y relaciones estadisticas|regresión]] tiene sentido investigar más a fondo.

```python
g = sns.PairGrid(iris, hue="species")
g.map_diag(sns.histplot)      # la diagonal: distribución de cada variable
g.map_offdiag(sns.scatterplot) # fuera de la diagonal: relación entre pares
```

`PairGrid` es la versión "de bajo nivel" de `pairplot` — usala cuando querés una función distinta en la diagonal que fuera de ella (por ejemplo, `kdeplot` en la diagonal y `scatterplot` afuera), algo que `pairplot(diag_kind=...)` no cubre.

## `heatmap()`: visualizar una matriz de correlación

Una aplicación muy común de `heatmap()` en análisis exploratorio: ver de un vistazo qué variables numéricas se mueven juntas.

```python
import numpy as np

corr = df.select_dtypes("number").corr()   # matriz de correlación, ver [[06 - Agregacion y groupby|Pandas]]
sns.heatmap(corr, annot=True, cmap="coolwarm", center=0)
```

> [!tip] Por qué `center=0` importa acá
> Una correlación va de $-1$ a $1$, con $0$ como punto neutro genuino (sin relación lineal). Usar una paleta **divergente** centrada en 0 (ver [[09 - Estilo, paletas de color y temas]]) es lo que hace que el heatmap se lea de un vistazo: los tonos cálidos y fríos separan visualmente correlación positiva de negativa, y el centro pálido resalta lo que **no** está relacionado.

`clustermap()` hace lo mismo que `heatmap`, pero además reordena filas y columnas agrupando las variables más parecidas entre sí — útil cuando la matriz es grande y el orden original de las columnas no ayuda a ver los bloques de relación.

## Relacionado
- [[estratificación]]
- [[06 - Variables categoricas (boxplot, violinplot, barplot)]]
- [[07 - Regresion y relaciones estadisticas]]
- [[09 - Estilo, paletas de color y temas]]
