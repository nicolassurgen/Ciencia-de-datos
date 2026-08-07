---
titulo: "SciPy.stats - Métodos de remuestreo"
materia: SciPy
tipo: apunte
tags:
  - scipy
  - tecnologias
  - python
  - tema/inferencia
fuente: "SciPy Reference Guide — scipy.stats (docs.scipy.org/doc/scipy/reference/stats.html)"
---

# Métodos de remuestreo

> [!info] Contenido a futuro
> Los intervalos de confianza formales todavía no se dieron en Estadística. Esta nota queda como referencia para cuando el curso llegue a inferencia.

## La idea: simular muestreo repetido a partir de una sola muestra

[[población y muestra|La nota de Estadística sobre población y muestra]] explica que un estudio por muestreo "requiere herramientas de inferencia [...] para generalizar a toda la población, con un margen de error". El **remuestreo** (*resampling*) es una familia de técnicas que estima ese margen de error **sin fórmulas matemáticas cerradas**: en vez de eso, simula computacionalmente qué pasaría si se repitiera el muestreo muchas veces, usando la única muestra que sí se tiene como si fuera la población.

## Bootstrap: remuestrear con reposición

```python
from scipy import stats
import numpy as np

muestra = [39.1, 39.5, 40.3, 36.7, 39.3, 38.9, 39.2]

resultado = stats.bootstrap((muestra,), np.mean, n_resamples=9999, confidence_level=0.95)
resultado.confidence_interval
# ConfidenceInterval(low=38.4, high=39.7)
# -> con 95% de confianza, la media poblacional está entre 38.4 y 39.7 mm
```

`bootstrap()` toma la muestra, saca miles de "remuestras" del mismo tamaño **con reposición** (el mismo dato puede salir elegido más de una vez), calcula el estadístico de interés (acá la media) en cada una, y con esa distribución de estadísticos simulados arma un intervalo de confianza. Es una forma directa de responder "¿qué tan preciso es mi estadístico?" sin necesitar los supuestos de un test paramétrico clásico.

## Test de permutación: ¿la diferencia entre grupos es real?

```python
maquina_1 = [39.1, 39.5, 40.3, 36.7, 39.3]
maquina_2 = [41.2, 40.8, 42.1, 39.9, 40.5]

def diferencia_de_medias(x, y):
    return np.mean(x) - np.mean(y)

resultado = stats.permutation_test((maquina_1, maquina_2), diferencia_de_medias)
resultado.pvalue   # 0.016 -> una diferencia así de grande aparece solo 1.6% de las veces por puro azar
```

Mezcla aleatoriamente las etiquetas de grupo miles de veces (bajo el supuesto de que "no hay diferencia real") y ve qué tan seguido una diferencia así de grande aparece por puro azar. Es una alternativa a `ttest_ind` (ver [[06 - Tests de hipotesis - una y dos muestras]]) que no asume que los datos sean normales.

## Test de Monte Carlo

```python
resultado = stats.monte_carlo_test(muestra, rvs=stats.norm(loc=0, scale=1).rvs, statistic=np.mean)
```

Simula datos desde una distribución teórica hipotética (en vez de remuestrear los datos observados) para ver si el estadístico observado es compatible con esa distribución.

## Relacionado
- [[01 - Introduccion a SciPy.stats]]
- [[población y muestra]]
- [[parámetro vs estadístico]]
- [[06 - Tests de hipotesis - una y dos muestras]]
