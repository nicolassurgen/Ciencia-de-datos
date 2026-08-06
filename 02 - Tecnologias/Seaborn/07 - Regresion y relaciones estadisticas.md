---
titulo: Seaborn - Regresión y relaciones estadísticas
materia: Seaborn
tipo: apunte
tags:
  - seaborn
  - tecnologias
  - python
  - tema/regresion
fuente: "seaborn.pydata.org (documentación oficial)"
---

# Regresión y relaciones estadísticas

Esta es la primera nota de la guía donde el gráfico no solo **describe** los datos — también **ajusta un modelo** sobre ellos. Es un paso conceptual más allá de todo lo anterior.

> [!important] La pregunta estadística detrás de este gráfico
> "¿Existe una relación lineal entre estas dos variables, y qué tan fuerte/segura es?" — no solo mirar la nube de puntos ([[04 - Relaciones entre variables (scatterplot, lineplot)|scatterplot]]) sino **cuantificarla** con una línea y una banda de incertidumbre.

## `regplot()` y `lmplot()`: scatter + modelo lineal

```python
sns.lmplot(data=tips, x="total_bill", y="tip")
```

Ambas funciones dibujan un scatterplot de `x` e `y`, ajustan el modelo $y = \beta_0 + \beta_1 x$ y grafican la recta resultante junto con una **banda de confianza del 95 %**. `regplot` es de ejes; `lmplot` es de figura (ver [[02 - Funciones de figura vs funciones de ejes]]) — y solo `lmplot` acepta `hue`/`col`/`row`, porque por dentro usa un `FacetGrid` (ver [[08 - Grids y comparaciones multiples]]).

> [!warning] La regla más importante de este gráfico
> Que Seaborn te dibuje una línea prolija **no significa que el modelo lineal sea apropiado**. Antes de confiar en la recta, mirá si la nube de puntos realmente parece lineal — y recordá [[variable de confusión|el mismo cuidado]] que ya viste en Estadística: una relación entre dos variables puede deberse a una tercera que no estás mirando. Correlación no es causalidad, ni siquiera cuando viene con una banda de confianza prolija.

## Variantes del modelo

```python
sns.lmplot(data=anscombe.query("dataset == 'II'"), x="x", y="y", order=2)         # polinomial
sns.lmplot(data=anscombe.query("dataset == 'III'"), x="x", y="y", robust=True)    # robusto a atípicos
sns.lmplot(data=tips, x="total_bill", y="big_tip", logistic=True, y_jitter=.03)    # logística (Y binaria)
sns.lmplot(data=tips, x="total_bill", y="tip", lowess=True)                        # suavizado, sin banda de IC
```

| Parámetro | Para qué sirve |
|---|---|
| `order=2` | Ajusta un polinomio en vez de una recta, si la relación es curva |
| `robust=True` | Reduce el peso de los [[valores atípicos|atípicos]] al ajustar — la versión "regresión" de usar la [[robustez estadística|mediana en vez de la media]] |
| `logistic=True` | Para Y binaria (0/1) — estima probabilidades, no valores continuos |
| `lowess=True` | Suavizado no paramétrico, sin asumir una forma funcional fija (no calcula banda de confianza) |
| `ci=None` | Desactiva la banda de confianza — más rápido, útil con `logistic`/`robust` sobre datasets grandes |

## Datos discretos en X: `x_jitter` y `x_estimator`

```python
sns.lmplot(data=tips, x="size", y="tip", x_jitter=.05)                 # separa visualmente los puntos superpuestos
sns.lmplot(data=tips, x="size", y="tip", x_estimator=np.mean)           # un punto + IC por cada valor de size
```

Cuando `x` es una variable discreta (ver [[variables]] de Estadística — "cuento → discreta"), los puntos se apilan en columnas exactas y es difícil ver la densidad. `x_jitter` agrega ruido visual; `x_estimator` colapsa cada valor de X a su media con intervalo de confianza, algo parecido a un [[06 - Variables categoricas (boxplot, violinplot, barplot)|pointplot]] pero sobre una variable numérica.

## `residplot()`: chequear si el modelo lineal tenía sentido

```python
sns.residplot(data=tips, x="total_bill", y="tip")
```

Grafica los **residuos** (lo que el modelo no explica) contra X. Si el modelo lineal es apropiado, los residuos deberían verse como una nube sin patrón, centrada en cero. Si aparece una curva o un embudo (la dispersión crece con X), es una señal de que el modelo lineal simple no alcanza — el mismo tipo de diagnóstico que un análisis de [[grados de libertad|regresión]] formal haría con estadísticos de bondad de ajuste.

## Relacionado
- [[04 - Relaciones entre variables (scatterplot, lineplot)]]
- [[variable de confusión]]
- [[robustez estadística]]
- [[valores atípicos]]
- [[03 - Optimizacion]]
