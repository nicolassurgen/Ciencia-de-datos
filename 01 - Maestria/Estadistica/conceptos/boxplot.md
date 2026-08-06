---
titulo: Boxplot (diagrama de caja y bigotes)
materia: Estadística
tipo: concepto
tags:
  - estadistica
  - maestria
  - concepto
  - tema/variabilidad
fecha: 2026-08-03
---

# Boxplot (diagrama de caja y bigotes)

> [!definition] Boxplot
> Gráfico que resume una distribución con el ***five-number summary***: mínimo, primer cuartil ($q_1$), mediana, tercer cuartil ($q_3$) y máximo. Es la forma visual estándar de comparar **centro**, **dispersión** y presencia de **atípicos** entre distintos conjuntos de datos.

## Anatomía

![[Anatomia del boxplot.png]]

- La **caja** va de $q_1$ a $q_3$ → contiene el **50 % central** de los datos; su largo **es el [[medidas de dispersión|RIQ]]**.
- La **línea interna** de la caja es la **mediana**.
- Los **bigotes** se extienden hasta el dato más lejano que **no** sea considerado atípico.

## Detección de atípicos: criterio 1.5 · RIQ

> [!important] Vallas del boxplot
> Se considera **valor atípico** cualquier dato que caiga **fuera** de:
> $$[\,q_1 - 1{,}5 \cdot \text{RIQ}\ ,\ \ q_3 + 1{,}5 \cdot \text{RIQ}\,]$$
> Los bigotes llegan hasta el último dato **dentro** de esas vallas; los que quedan afuera se dibujan como **puntos individuales**. Ver [[valores atípicos]].

> [!example] Ejemplo — imperfecciones por pieza
> Con Q1 = 0, Q3 = 1, RIQ = 1: como $q_3 + 1{,}5\cdot\text{RIQ} = 2{,}5$, las piezas con **3 y 4** imperfecciones aparecen como **atípicos** (puntos por encima del bigote superior).

## Por qué es una herramienta robusta

El boxplot se construye enteramente a partir de **percentiles**, que son medidas [[robustez estadística|robustas]]: no se distorsiona por la presencia de atípicos, a diferencia de un resumen basado en la media y el desvío estándar.

> [!note] En código
> `sns.boxplot(data=df, x="grupo", y="valor")` en Seaborn (ver [[06 - Variables categoricas (boxplot, violinplot, barplot)]]) — el mismo criterio 1.5·RIQ de acá es el que usa para marcar los puntos como atípicos. `ax.boxplot()` en Matplotlib es la versión sin agrupar por categoría automáticamente. El RIQ que arma la caja se calcula directo con `scipy.stats.iqr(x)` (ver [[03 - Estadistica descriptiva]]).

## Relacionado
- [[02 - El estudio de la variabilidad]]
- [[medidas de dispersión]]
- [[valores atípicos]]
- [[robustez estadística]]
- [[06 - Variables categoricas (boxplot, violinplot, barplot)]]
- [[03 - Estadistica descriptiva]]
