---
titulo: "SciPy.stats - Transformaciones y detección de atípicos"
materia: SciPy
tipo: apunte
tags:
  - scipy
  - tecnologias
  - python
  - tema/estadistica-descriptiva
fuente: "SciPy Reference Guide — scipy.stats (docs.scipy.org/doc/scipy/reference/stats.html)"
---

# Transformaciones y detección de atípicos

## Estandarización: `zscore`

```python
from scipy import stats

stats.zscore(x)   # (x - media) / desvío estándar, elemento a elemento
```

El **z-score** mide a cuántos desvíos estándar está cada dato de la media. [[valores atípicos|La nota de Estadística sobre atípicos]] ya menciona esta idea como un criterio "no visto en la clase, pero de uso común" (alternativo al criterio del [[boxplot|1.5·RIQ]] visto en clase): un valor con $|z| > 3$ suele marcarse como sospechoso.

> [!warning] El z-score hereda el problema de la media
> El z-score se calcula con la media y el desvío estándar — ambas medidas **NO robustas** (ver [[robustez estadística]]). Si ya hay atípicos extremos, esas mismas medidas están infladas por ellos, lo que puede **esconder** atípicos menos extremos. Por eso el criterio del RIQ (basado en percentiles, robusto) suele preferirse cuando se sospecha de atípicos importantes.

## Sigma-clipping: recortar iterativamente

```python
resultado, low, high = stats.sigmaclip(x, low=3, high=3)
```

Recorta iterativamente los valores que quedan a más de `low`/`high` desvíos estándar de la media, **recalculando** la media y el desvío en cada pasada (a diferencia de un z-score de una sola pasada). Es una forma automática de aislar el "núcleo" de los datos, útil como paso de [[tratamiento primario|tratamiento primario]] antes de un análisis descriptivo.

## Transformaciones de potencia: Box-Cox y Yeo-Johnson

```python
datos_transformados, lambda_optimo = stats.boxcox(x)   # requiere x > 0
datos_transformados, lambda_optimo = stats.yeojohnson(x)  # admite negativos y ceros
```

Buscan la transformación de potencia que hace que los datos se parezcan más a una distribución normal — útil cuando un [[histograma]] muestra fuerte asimetría y varios métodos estadísticos (a futuro: regresión, ver [[02 - Regresion lineal (OLS y WLS)]] de statsmodels) asumen datos aproximadamente normales.

## Relacionado
- [[01 - Introduccion a SciPy.stats]]
- [[valores atípicos]]
- [[robustez estadística]]
- [[tratamiento primario]]
