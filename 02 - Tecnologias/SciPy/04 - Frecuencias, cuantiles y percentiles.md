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

largos_pico = [39.1, 39.5, 40.3, 36.7, 39.3, 38.9, 39.2]   # largo de pico (mm), 7 pingüinos

stats.scoreatpercentile(largos_pico, 75)   # 39.4 -> el valor que acumula el 75% (q3)
```

Hace lo mismo que `np.percentile(largos_pico, 75)` (ver [[medidas de posición]]): ambas devuelven un [[medidas de posición|percentil]]. La diferencia práctica es de dónde viven — este vive junto al resto de las herramientas de `scipy.stats`.

## La pregunta inversa: `percentileofscore`

```python
stats.percentileofscore(largos_pico, 39.5)   # 71.4 -> 39.5 mm deja atrás al 71.4% de los demás pingüinos
```

Mientras que un percentil responde *"¿qué valor acumula el 75 % de los datos?"*, `percentileofscore` responde la pregunta al revés: *"este valor puntual, ¿qué proporción de los datos deja por debajo?"* — es la $F(x^{*})$ de la notación de la [[02 - El estudio de la variabilidad|clase de Estadística]], evaluada en un punto concreto en vez de despejada.

## Frecuencias acumuladas

```python
resultado = stats.cumfreq(largos_pico, numbins=5)
resultado.cumcount        # array([1., 3., 4., 6., 7.]) -> frecuencia absoluta acumulada, bin a bin
```

`cumcount` es exactamente la columna $F_i$ de una [[distribución de frecuencias]] agrupada en intervalos: en el primer bin (los valores más chicos) ya cayó 1 pingüino, en el segundo hay 3 acumulados, y así hasta llegar a los 7 totales. Es lo mismo que arma "a mano" la tabla de frecuencias de la clase, pero para datos agrupados en bins en vez de valores/categorías puntuales — la base numérica de la **ojiva**.

## Estadísticos por bin: `binned_statistic`

```python
# ¿cuál es la masa promedio de los pingüinos, agrupados por rango de largo de pico?
masas = [3750, 3800, 3250, 3450, 3650, 3625, 3475]

stats.binned_statistic(largos_pico, masas, statistic='mean', bins=3)
# BinnedStatisticResult(statistic=array([3625., 3450., 3625.]), ...)
```

Agrupa `largos_pico` en 3 intervalos (como un histograma) y calcula el promedio de `masas` **dentro de cada intervalo**, en vez de sobre el conjunto completo — responde "¿los pingüinos con pico más largo también pesan más, en promedio?" sin armar el agrupamiento a mano. Es una versión continua de [[estratificación|estratificar]] por rangos de una variable numérica.

## Relacionado
- [[01 - Introduccion a SciPy.stats]]
- [[medidas de posición]]
- [[distribución de frecuencias]]
- [[04 - Agregaciones y estadistica descriptiva]]
