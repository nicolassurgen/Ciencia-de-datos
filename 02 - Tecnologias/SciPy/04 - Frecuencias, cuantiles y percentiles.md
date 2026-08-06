---
titulo: "SciPy.stats - Frecuencias, cuantiles y percentiles"
materia: SciPy
tipo: apunte
tags:
  - scipy
  - tecnologias
  - python
  - tema/estadistica-descriptiva
fuente: "SciPy Reference Guide — scipy.stats (docs.scipy.org/doc/scipy/reference/stats.html)"
---

# Frecuencias, cuantiles y percentiles

## Percentiles: la otra forma de calcularlos

```python
from scipy import stats

stats.scoreatpercentile(x, 75)   # el valor que acumula el 75% -> q3
```

Hace lo mismo que `np.percentile(x, 75)` (ver [[medidas de posición]]): ambas devuelven un [[medidas de posición|percentil]]. La diferencia práctica es de dónde viven — este vive junto al resto de las herramientas de `scipy.stats`.

## La pregunta inversa: `percentileofscore`

```python
stats.percentileofscore(x, 39.5)   # ¿qué percentil ocupa el valor 39.5 dentro de x?
```

Mientras que un percentil responde *"¿qué valor acumula el 75 % de los datos?"*, `percentileofscore` responde la pregunta al revés: *"este valor puntual, ¿qué proporción de los datos deja por debajo?"* — es la $F(x^{*})$ de la notación de la [[02 - El estudio de la variabilidad|clase de Estadística]], evaluada en un punto concreto en vez de despejada.

## Frecuencias acumuladas

```python
resultado = stats.cumfreq(x, numbins=5)
resultado.cumcount        # array con las frecuencias absolutas acumuladas por bin
```

Construye exactamente la columna $F_i$ de una [[distribución de frecuencias]] agrupada en intervalos — lo mismo que arma "a mano" la tabla de frecuencias de la clase, pero para datos agrupados en bins en vez de valores/categorías puntuales. Es la base numérica de la **ojiva** (el polígono de frecuencias acumuladas).

## Estadísticos por bin: `binned_statistic`

```python
stats.binned_statistic(x, valores, statistic='mean', bins=5)
```

Agrupa `x` en intervalos (como un histograma) y calcula un estadístico (media, mediana, conteo, o una función propia) **por intervalo**, en vez de sobre el conjunto completo. Es útil cuando además de la frecuencia por intervalo interesa, por ejemplo, el promedio de otra variable dentro de cada uno — una versión continua de [[estratificación|estratificar]] por rangos de una variable numérica.

## Relacionado
- [[01 - Introduccion a SciPy.stats]]
- [[medidas de posición]]
- [[distribución de frecuencias]]
- [[04 - Agregaciones y estadistica descriptiva]]
