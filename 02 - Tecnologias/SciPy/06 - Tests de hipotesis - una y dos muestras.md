---
titulo: "SciPy.stats - Tests de hipótesis (una y dos muestras)"
materia: SciPy
tipo: apunte
tags:
  - scipy
  - tecnologias
  - python
  - tema/inferencia
fuente: "SciPy Reference Guide — scipy.stats (docs.scipy.org/doc/scipy/reference/stats.html)"
---

# Tests de hipótesis: una y dos muestras

> [!info] Contenido a futuro
> La materia Estadística todavía no dio inferencia formal (intervalos de confianza, pruebas de hipótesis) — esta nota queda como referencia para cuando el curso llegue a ese tema. La [[diseño de experimentos|nota de diseño de experimentos]] ya lo anticipa: *"decidir si la diferencia observada entre tratamientos es real o puede deberse al azar [...] eso es exactamente lo que hacen las pruebas de hipótesis"*.

## La lógica común a todos los tests

Un test de hipótesis de `scipy.stats` siempre devuelve dos números: un **estadístico de prueba** (qué tan extremo es lo observado, en las unidades propias del test) y un **p-valor** (la probabilidad de ver un resultado así de extremo, o más, **si la hipótesis nula fuera cierta** — es decir, si en realidad no hubiera efecto).

> [!important] Nivel de significancia vs. p-valor: no son lo mismo
> El **nivel de significancia** ($\alpha$, típicamente 0.05) es un umbral que se fija **antes** de ver los datos, como criterio de decisión. El **p-valor** es una probabilidad que se **calcula a partir de los datos observados**, después del experimento. La regla es comparar uno contra otro: si `p < α`, se rechaza la hipótesis nula. Tratarlos como sinónimos —o decir "el p-valor es la probabilidad de que la hipótesis nula sea cierta"— es un error de interpretación frecuente; el p-valor no dice nada sobre la probabilidad de la hipótesis, sino sobre qué tan compatibles son los datos observados con ella.

## Comparar una muestra contra un valor de referencia

```python
from scipy import stats

muestra = [39.1, 39.5, 40.3, 36.7, 39.3, 38.9, 39.2, 37.8, 40.1, 38.5]
stats.ttest_1samp(muestra, popmean=39)
# TtestResult(statistic=-0.178, pvalue=0.863, df=9)
```

La media de la muestra es 38.94, muy cerca de 39. El estadístico ($t=-0.178$) es chico y el p-valor (0.863) es alto: con $\alpha=0.05$, no hay evidencia para rechazar que la media poblacional sea 39 — el resultado es perfectamente compatible con esa hipótesis. Esto **no prueba** que la media sea exactamente 39; solo dice que los datos no la contradicen.

## Comparar dos muestras independientes

```python
maquina_1 = [39.1, 39.5, 40.3, 36.7, 39.3]
maquina_2 = [41.2, 40.8, 42.1, 39.9, 40.5]

stats.ttest_ind(maquina_1, maquina_2)
# TtestResult(statistic=-2.711, pvalue=0.0266, df=8.0)
stats.mannwhitneyu(maquina_1, maquina_2)
# MannwhitneyuResult(statistic=1.0, pvalue=0.0159)
stats.levene(maquina_1, maquina_2)
# LeveneResult(statistic=0.170, pvalue=0.691)
```

Con $\alpha=0.05$, el p-valor de `ttest_ind` (0.0266) queda por debajo del umbral: hay evidencia de que las máquinas 1 y 2 tienen diámetros promedio distintos. `mannwhitneyu` (alternativa no paramétrica, sin asumir normalidad) coincide en la conclusión. `levene` da un p-valor alto (0.691): no hay evidencia de que las varianzas difieran, así que el supuesto de homocedasticidad del t-test estándar es razonable acá.

> [!important] El p-valor no dice si la diferencia importa en la práctica
> Un p-valor chico solo dice que la diferencia observada es difícil de explicar por azar — no dice si esa diferencia es **grande**. Para eso hace falta un **tamaño de efecto**, como la *d* de Cohen (la diferencia de medias, expresada en desvíos estándar):
> ```python
> import numpy as np
> def cohen_d(a, b):
>     a, b = np.array(a), np.array(b)
>     na, nb = len(a), len(b)
>     s_pooled = np.sqrt(((na-1)*np.var(a, ddof=1) + (nb-1)*np.var(b, ddof=1)) / (na+nb-2))
>     return (np.mean(a) - np.mean(b)) / s_pooled
>
> cohen_d(maquina_1, maquina_2)   # -1.71
> ```
> $|d| \approx 1.71$ es un efecto **grande** según las convenciones habituales (Cohen: ~0.2 chico, ~0.5 mediano, ~0.8 grande) — la diferencia no solo es estadísticamente significativa, también es sustancial en magnitud. Con una muestra mucho más grande, un efecto minúsculo (poco relevante en la práctica) también puede dar `p < 0.05`; el tamaño de efecto es lo que permite distinguir "significativo" de "importante".

Es el caso exacto de los *dotplots* de diámetro de las Máquinas 1 y 2 de la [[02 - El estudio de la variabilidad|clase 2]]: ahí se comparaban **visualmente** centro y dispersión; `ttest_ind` da una respuesta **numérica** a si esa diferencia visual es estadísticamente significativa, y el tamaño de efecto cuantifica qué tan grande es.

## Comparar tres o más grupos: ANOVA

```python
maquina_3 = [37.8, 38.2, 37.5, 38.9, 38.0]

stats.f_oneway(maquina_1, maquina_2, maquina_3)
# F_onewayResult(statistic=11.179, pvalue=0.00182)
stats.kruskal(maquina_1, maquina_2, maquina_3)
# KruskalResult(statistic=9.920, pvalue=0.00701)
```

Ambos p-valores están muy por debajo de 0.05: hay evidencia de que al menos una de las tres máquinas difiere de las demás en diámetro promedio. Ninguno de los dos tests dice **cuál** máquina es distinta — eso requiere un análisis posterior (comparaciones múltiples), fuera del alcance de esta nota.

Generaliza `ttest_ind` a más de dos grupos — la herramienta que la nota de [[diseño de experimentos]] menciona explícitamente para cuando hay 3 o más tratamientos.

## Verificar el supuesto de normalidad

```python
stats.shapiro(muestra)
# ShapiroResult(statistic=0.932, pvalue=0.465)
stats.normaltest(muestra)
# NormaltestResult(statistic=2.941, pvalue=0.230)
```

Ambos p-valores son altos (0.465 y 0.230): no hay evidencia contra la normalidad de `muestra`, así que usar un t-test sobre estos datos es razonable. Si alguno de estos tests diera un p-valor bajo, convendría preferir la alternativa no paramétrica (`mannwhitneyu`, `kruskal`) en vez del t-test o ANOVA.

Muchos tests (el t-test entre ellos) asumen que los datos siguen aproximadamente una [[02 - Distribuciones de probabilidad|distribución normal]]. Estos tests lo verifican formalmente, en vez de solo mirar la forma de un [[histograma]] a ojo.

> [!note] El parámetro `df` reaparece acá
> Los resultados de `ttest_1samp`/`ttest_ind` incluyen `df` (grados de libertad) en su salida detallada — el mismo concepto de [[grados de libertad]] visto en el cálculo de la varianza muestral, reutilizado acá para definir la forma exacta de la distribución t contra la que se compara el estadístico.

## Relacionado
- [[01 - Introduccion a SciPy.stats]]
- [[diseño de experimentos]]
- [[grados de libertad]]
- [[parámetro vs estadístico]]
