---
titulo: Estadística descriptiva vs. inferencial
materia: Estadística
tipo: concepto
tags:
  - estadistica
  - maestria
  - concepto
  - tema/introduccion
fecha: 2026-08-19
---

# Estadística descriptiva vs. inferencial

Todo lo visto hasta ahora en la materia —tablas de frecuencias, gráficos, medias, desvíos— tiene un límite claro: describe **los datos que efectivamente se tienen**. Ninguna de esas herramientas, por sí sola, dice nada sobre los datos que **no** se observaron. Esa es exactamente la frontera entre las dos grandes ramas de la estadística.

> [!definition] Análisis (o estadística) descriptivo
> "Consiste en la aplicación de herramientas (tablas, gráficos, indicadores) para resumir o presentar un conjunto de datos, sean estos de una muestra o de una población finita." *Fuente: [[Estadística para la resolución de problemas en Ingeniería]], cap. 1.*

> [!definition] Análisis (o estadística) inferencial
> "Consiste en la aplicación de herramientas (intervalos de confianza, pruebas de hipótesis) que permiten extender las conclusiones de una muestra hacia la población, con riesgos controlados. Estas herramientas se apoyan en la Teoría de la Probabilidad." *Fuente: [[Estadística para la resolución de problemas en Ingeniería]], cap. 1.*

## La regla que decide cuál hace falta

> [!important] ¿Población completa o muestra?
> Cuando los datos corresponden a la **totalidad** de una población finita, el análisis descriptivo permite obtener conclusiones **definitivas** — no hace falta nada más. Cuando los datos provienen de una **muestra**, las conclusiones del análisis descriptivo se consideran **preliminares**, y deben complementarse con herramientas inferenciales para poder generalizarlas a la población. *Fuente: [[Estadística para la resolución de problemas en Ingeniería]], cap. 1.*

Es la misma distinción que separa un [[parámetro vs estadístico|parámetro de un estadístico]]: sobre una población completa se calcula directamente el parámetro (no hay nada que estimar); sobre una muestra, solo se puede calcular un estadístico, que **estima** al parámetro con un margen de incertidumbre — margen que es precisamente lo que cuantifica la inferencia.

> [!example] Ya lo viste en la práctica
> [[02.1 - Casos aplicados]] tiene un ejemplo directo de esta distinción: en el Caso 4 (dos lotes completos de 300 planchas cada uno), la conclusión sobre qué proporción cumple la especificación **es** un hecho, no una estimación — se trabajó con la población completa, alcanzaba con lo descriptivo. En los Casos 2 y 3, en cambio, se trabajó con muestras (20 mediciones, 50 reclamos): cualquier conclusión sobre "todos los reclamos" o "el desempeño real de cada laboratorio" queda, estrictamente, pendiente de un paso inferencial que la materia todavía no desarrolló.

## Un vocabulario alternativo, con otro énfasis: EDA vs. inferencia

La bibliografía de ciencia de datos suele plantear una distinción emparentada, pero con otro foco:

> [!quote] Análisis exploratorio como reacción a la inferencia clásica
> "Exploratory data analysis, or EDA, is a comparatively new area of statistics. Classical statistics focused almost exclusively on inference, a sometimes complex set of procedures for drawing conclusions about large populations based on small samples." *Fuente: [[Practical Statistics for Data Scientists]] (Bruce & Bruce), cap. 1.*

No es exactamente el mismo par de términos —"EDA" no es idéntico a "descriptiva", y no siempre se contrasta con "inferencial" sino con el análisis confirmatorio (ver [[análisis exploratorio vs confirmatorio]])— pero la tensión de fondo es la misma: ¿el objetivo es resumir y entender lo que hay, o generalizar con garantías formales más allá de lo que hay?

## Tabla comparativa

| | Descriptiva | Inferencial |
|---|---|---|
| Objeto de estudio | Los datos disponibles (muestra o población) | La población, a partir de una muestra |
| Herramientas | Tablas, gráficos, medidas de resumen | Intervalos de confianza, pruebas de hipótesis |
| Base matemática | Aritmética / álgebra de resumen | Teoría de la probabilidad |
| ¿Cuantifica incertidumbre? | No | Sí — con [[error muestral y error no muestral|riesgos controlados]] |

> [!note] En código
> Todo lo que hoy tiene una nota propia en `Estadistica/conceptos/` —medidas de posición, dispersión, gráficos— es **descriptivo**. Cuando llegue la inferencia formal, sus herramientas viven en [[06 - Tests de hipotesis - una y dos muestras]] y [[08 - Metodos de remuestreo]] de SciPy.

## Relacionado
- [[el ciclo estadístico (PPDAC)]]
- [[parámetro vs estadístico]]
- [[análisis exploratorio vs confirmatorio]]
- [[población y muestra]]
- [[02.1 - Casos aplicados]]
- [[01 - Como dar sentido a los datos]]
