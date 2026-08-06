---
titulo: "SciPy.stats - Introducción"
materia: SciPy
tipo: apunte
tags:
  - scipy
  - tecnologias
  - python
  - tema/introduccion
fuente: "SciPy Reference Guide — scipy.stats (docs.scipy.org/doc/scipy/reference/stats.html)"
---

# Introducción a SciPy.stats

> [!definition] SciPy
> Librería científica de Python construida **encima** de NumPy: donde NumPy da el `ndarray` y las operaciones básicas, SciPy agrega algoritmos numéricos de más alto nivel — optimización, álgebra lineal, señales, y el módulo que nos interesa acá: **`scipy.stats`**.

> [!definition] scipy.stats
> El submódulo de estadística de SciPy. Reúne en un solo lugar tres cosas que hasta ahora veníamos haciendo por separado: **distribuciones de probabilidad** (más de 100, continuas y discretas), **estadística descriptiva** (muchas de las medidas que ya calculás con NumPy, más otras que NumPy no tiene) y **estadística inferencial** (tests de hipótesis, correlación, remuestreo).

## Por qué existe si ya está NumPy

NumPy resuelve el **álgebra** de los datos: sumar, promediar, ordenar un array. `scipy.stats` resuelve la **estadística** propiamente dicha: no solo calcula un promedio, sino que sabe qué es una distribución normal, puede decirte la probabilidad de observar un valor tan extremo como el tuyo, o comparar dos grupos y decirte si la diferencia es significativa. Es, en cierto sentido, la traducción directa a código de la materia **Estadística** de la maestría.

> [!important] El hilo conductor de esta carpeta
> Cada nota de esta carpeta cita explícitamente **a qué nota de Estadística corresponde** lo que hace esa función. Donde la materia todavía no llegó a un tema (tests de hipótesis, correlación, remuestreo), la nota lo marca como **contenido a futuro**: la función existe y se explica igual, pero sin forzar una conexión que hoy no está.

## Importar

```python
from scipy import stats
```

Convención estándar: se importa el submódulo `stats`, no todo `scipy` (así como `import numpy as np`, ver [[01 - Introduccion y arrays]]).

## Recorrido de estas notas

1. **Introducción** *(esta nota)*
2. [[02 - Distribuciones de probabilidad]] — variables aleatorias, `pdf`/`cdf`/`ppf`/`rvs`.
3. [[03 - Estadistica descriptiva]] — `describe`, `variation`, `trim_mean`, `iqr`: el puente directo con las medidas de resumen de Estadística.
4. [[04 - Frecuencias, cuantiles y percentiles]] — percentiles, rangos, frecuencias acumuladas.
5. [[05 - Transformaciones y deteccion de atipicos]] — `zscore`, `sigmaclip`, estandarización.
6. [[06 - Tests de hipotesis - una y dos muestras]] — *(a futuro)* comparar grupos, normalidad.
7. [[07 - Correlacion y tests de asociacion]] — *(a futuro)* `pearsonr`, `spearmanr`, chi-cuadrado.
8. [[08 - Metodos de remuestreo]] — *(a futuro)* bootstrap, tests de permutación.
9. [[09 - Estimacion de densidad y ajuste de distribuciones]] — KDE, `fit`, ECDF.

## Relacionado
- [[01 - Introduccion y arrays]]
- [[01 - Como dar sentido a los datos]]
- [[02 - El estudio de la variabilidad]]
