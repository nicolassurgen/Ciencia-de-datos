---
titulo: Histograma
materia: Estadística
tipo: concepto
tags:
  - estadistica
  - maestria
  - concepto
  - tema/variabilidad
fecha: 2026-08-03
---

# Histograma

> [!definition] Histograma
> Gráfico para una variable **cuantitativa continua** (o discreta con muchos valores) construido a partir de una [[distribución de frecuencias]] agrupada en **intervalos de clase**. Las barras van **pegadas** entre sí (sin espacio), porque los intervalos son contiguos, a diferencia de un gráfico de barras para variables cualitativas.

## Qué muestra

Es el gráfico de referencia para ver la **forma** de la distribución de una variable continua:

- **Simétrica / centrada** → los datos se reparten parejo a ambos lados del centro.
- **Asimétrica a la derecha** (sesgo positivo) → mayoría de valores bajos, cola larga hacia valores altos.
- **Asimétrica a la izquierda** (sesgo negativo) → mayoría de valores altos, cola larga hacia valores bajos.
- **Número de modas** (picos) → unimodal, bimodal, etc. Un histograma **bimodal** suele señalar que hay **dos grupos mezclados** (ver [[estratificación]]).

> [!tip] Cómo recordar el sentido de la asimetría
> Se nombra por **dónde está la cola**, no dónde está el pico. En estas distribuciones la media es "arrastrada" hacia la cola: asimétrica a la derecha → media > mediana; asimétrica a la izquierda → media < mediana.

## Gráficos emparentados

- **Polígono de frecuencias** → une los puntos medios de las cimas del histograma.
- **Ojiva** → polígono de frecuencias **acumuladas**; curva creciente de $H_i$, permite leer percentiles gráficamente.
- **[[diagrama de tallo y hoja]]** → como un histograma "acostado", pero sin perder los datos originales.

> [!note] En código
> `sns.histplot(data=df, x="columna")` en Seaborn (ver [[05 - Distribuciones (histplot, kdeplot, ecdfplot)]]) — con `kde=True` superpone además la versión suavizada (KDE). `ax.hist()` en Matplotlib es la versión de más bajo nivel (ver [[04 - Tipos de graficos basicos]]). Esa curva KDE es `scipy.stats.gaussian_kde()` por debajo — una versión del histograma que no depende de dónde se corten los intervalos (ver [[09 - Estimacion de densidad y ajuste de distribuciones]]).

## Relacionado
- [[02 - El estudio de la variabilidad]]
- [[distribución de frecuencias]]
- [[diagrama de tallo y hoja]] · [[boxplot]]
- [[estratificación]]
- [[05 - Distribuciones (histplot, kdeplot, ecdfplot)]]
- [[09 - Estimacion de densidad y ajuste de distribuciones]]
