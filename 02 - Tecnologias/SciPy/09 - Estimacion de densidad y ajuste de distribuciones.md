---
titulo: "SciPy.stats - Estimación de densidad y ajuste de distribuciones"
materia: SciPy
tipo: apunte
tags:
  - scipy
  - tecnologias
  - python
  - tema/distribuciones
fuente: "SciPy Reference Guide — scipy.stats (docs.scipy.org/doc/scipy/reference/stats.html)"
---

# Estimación de densidad y ajuste de distribuciones

## KDE: la versión suave de un histograma

```python
from scipy import stats

largos_pico = [39.1, 39.5, 40.3, 36.7, 39.3, 38.9, 39.2]

kde = stats.gaussian_kde(largos_pico)
kde.evaluate([39.0])   # array([0.435]) -> densidad estimada en largo_pico = 39.0 mm
```

Un [[histograma]] depende de dónde se ponen los cortes de los intervalos (dos histogramas con distinta cantidad de bins pueden verse bastante distintos para los mismos datos). El **KDE** (*kernel density estimation*) suaviza esa dependencia: en vez de contar cuántos datos caen en cada intervalo, pone una "curvita" (kernel) centrada en cada dato y las suma todas, dando una curva continua de densidad. Es exactamente la curva que `sns.histplot(kde=True)` superpone al histograma en Seaborn — ver [[05 - Distribuciones (histplot, kdeplot, ecdfplot)]].

## ECDF: la función de distribución empírica

```python
resultado = stats.ecdf(largos_pico)
resultado.cdf.probabilities
# array([0.143, 0.286, 0.429, 0.571, 0.714, 0.857, 1.   ])
# -> los H_i acumulados: el dato más chico (36.7) deja atrás al 14.3%, el más grande (40.3) al 100%
```

Es la versión **sin agrupar** de la $H_i$ (frecuencia relativa acumulada) que se calcula a mano en una [[distribución de frecuencias]]: en vez de una tabla con intervalos, da un escalón por cada dato observado. Es lo que dibuja `sns.ecdfplot()` de Seaborn.

## Ajustar una distribución teórica a datos reales

```python
media, desvio = stats.norm.fit(largos_pico)
# media=38.86, desvio=1.18 -> la normal N(38.86, 1.18) es la que mejor explica estos 7 datos
```

`fit()` encuentra los parámetros de una distribución teórica (ver [[02 - Distribuciones de probabilidad]]) que mejor explican los datos observados, por máxima verosimilitud. Es el paso que conecta "tengo un [[histograma]] con cierta forma" con "puedo modelar esto como una distribución normal/gamma/exponencial con estos parámetros exactos" — el punto de partida habitual antes de simular datos nuevos o calcular probabilidades fuera del rango observado.

## Relacionado
- [[01 - Introduccion a SciPy.stats]]
- [[02 - Distribuciones de probabilidad]]
- [[histograma]]
- [[distribución de frecuencias]]
