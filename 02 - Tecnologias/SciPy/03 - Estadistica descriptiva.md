---
titulo: "SciPy.stats - Estadística descriptiva"
materia: SciPy
tipo: apunte
tags:
  - scipy
  - tecnologias
  - python
  - tema/estadistica-descriptiva
fuente: "SciPy Reference Guide — scipy.stats (docs.scipy.org/doc/scipy/reference/stats.html)"
---

# Estadística descriptiva

Esta nota es, junto con [[04 - Agregaciones y estadistica descriptiva]] de NumPy, la traducción directa a código de [[02 - El estudio de la variabilidad]] de Estadística. Casi todo lo que sigue tiene un nombre y una fórmula ya vistos en esa clase.

## `describe()` — el resumen de una sola vez

```python
from scipy import stats

x = [2, 4, 3, 6, 3, 7, 5, 8, 7, 4]
resultado = stats.describe(x)
# DescribeResult(nobs=10, minmax=(2, 8), mean=4.9, variance=3.8778, skewness=0.026, kurtosis=-1.06)
```

Devuelve de una sola vez casi todo lo que [[medidas de posición|medidas de posición]] y [[medidas de dispersión|medidas de dispersión]] calculan por separado: cantidad de observaciones, mínimo/máximo, media, varianza — y además **asimetría** (`skewness`) y **curtosis** (`kurtosis`), dos medidas de **forma** que no vimos como funciones aparte pero que cuantifican justamente lo que el [[histograma]] muestra a simple vista (cola hacia un lado, "picudez" de la distribución).

> [!warning] `variance` usa $n-1$ por defecto
> A diferencia de `np.var()` (que por defecto divide por $n$), `scipy.stats.describe()` usa `ddof=1` (divide por $n-1$) por defecto — la varianza **muestral**, no la poblacional. Ver [[grados de libertad]] para el porqué de esa diferencia.

## El coeficiente de variación, directo

```python
stats.variation(x)          # = desvío / media, SIN multiplicar por 100
```

Esto **es** el [[coeficiente de variación]] de Estadística, calculado en una sola función en vez de armarlo a mano (`np.std(x, ddof=1) / np.mean(x)`). Ojo: `scipy.stats.variation()` no multiplica por 100 — hay que hacerlo si se quiere el CV en porcentaje, como en la definición de la materia.

## Medidas robustas

```python
stats.trim_mean(x, proportiontocut=0.1)   # promedio truncado: descarta 10% de cada extremo
stats.iqr(x)                               # rango intercuartílico (RIQ)
stats.median_abs_deviation(x)              # MAD: el robusto más resistente de todos
stats.gmean(x)                             # media geométrica
```

Estas dos primeras funciones son las que ya aparecen usadas, sin desarrollar, en las notas de [[robustez estadística]] y en la [[02 - El estudio de la variabilidad|clase 2 de Estadística]] (el ejemplo del vector `[2, 4, 3, 6, 3, 7, 5, 8, 7, 4]` con la media, la mediana y la **media truncada**). `stats.iqr(x)` es la función exacta que la clase usa para calcular el RIQ de las imperfecciones por pieza y decidir los [[valores atípicos|atípicos]] del [[boxplot]].

> [!important] Por qué `trim_mean` e `iqr` viven en `scipy.stats` y no en NumPy
> NumPy cubre las agregaciones **básicas** (suma, media, desvío — ver [[04 - Agregaciones y estadistica descriptiva]]). Las medidas **robustas** (pensadas específicamente para no distorsionarse con atípicos, como la [[robustez estadística|clase ya vio]]) son estadística propiamente dicha, y por eso viven en `scipy.stats`.

## Todo junto, comparado con Estadística

| Estadística (clase) | `scipy.stats` | NumPy equivalente |
|---|---|---|
| Media | — | `np.mean(x)` |
| Mediana | — | `np.median(x)` |
| Promedio truncado | `stats.trim_mean(x, p)` | — (no existe en NumPy) |
| RIQ | `stats.iqr(x)` | `np.percentile(x,75) - np.percentile(x,25)` |
| Coeficiente de variación | `stats.variation(x)` | `np.std(x, ddof=1) / np.mean(x)` |
| Moda | `stats.mode(x)` | — (no existe en NumPy) |

## Relacionado
- [[01 - Introduccion a SciPy.stats]]
- [[04 - Agregaciones y estadistica descriptiva]]
- [[medidas de posición]]
- [[medidas de dispersión]]
- [[coeficiente de variación]]
- [[robustez estadística]]
- [[boxplot]]
