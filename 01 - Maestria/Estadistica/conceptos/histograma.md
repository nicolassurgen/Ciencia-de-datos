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

> [!example] Formas de asimetría con datos reales
> - **Asimétrica a la derecha, clásica:** el **ingreso** de los hogares — la mayoría gana montos moderados, pero una cola de ingresos muy altos estira la distribución hacia la derecha. Los retornos diarios de una acción muestran el mismo patrón en una versión más extrema ("colas largas"): eventos de variación grande son más frecuentes de lo que la intuición sugiere.
> - **Asimétrica a la izquierda:** la duración del embarazo en semanas — la moda está en 39 semanas (a término), pero los partos prematuros extienden la cola hacia valores bajos, mientras que casi ningún embarazo pasa mucho de las 43 semanas (los médicos rara vez lo permiten). El peso al nacer tiene la misma forma, por una razón parecida.
> - **Casi simétrica:** la edad de la madre al dar a luz — moda alrededor de los 21 años, con una cola apenas más larga hacia edades mayores.
>
> *Fuentes: [[Practical Statistics for Data Scientists]] (Bruce & Bruce), cap. 1-2; [[Think Stats – Exploratory Data Analysis in Python]], cap. 2, datos de la encuesta NSFG.*

> [!example] Asimetría a la derecha con datos propios del curso
> El tiempo de resolución de 50 reclamos (Caso 3 de [[02.1 - Casos aplicados]]) es un ejemplo real y verificado de la misma forma que el ingreso de los hogares: la mayoría de los reclamos se resuelve rápido, pero una cola de casos demorados estira la distribución hacia la derecha, con la media (más alta) claramente por encima de la mediana.

![[Distribucion del tiempo de resolucion.png]]

> [!warning] No borres los bins vacíos
> Cuando un dato mucho más extremo que el resto obliga a usar intervalos de amplitud fija, pueden aparecer **bins sin ningún dato adentro** (huecos en el histograma) antes de llegar al valor extremo. Esos bins vacíos son información real — muestran que hay un salto grande entre el grueso de los datos y el valor atípico — y no deben eliminarse ni "acomodarse" para que el gráfico se vea más prolijo.

## Un chequeo rápido de simetría con los cuartiles

En una distribución razonablemente simétrica, la mediana queda **equidistante** de $q_1$ y $q_3$: $q_3 - \text{mediana} \approx \text{mediana} - q_1$. Cuando esa igualdad se rompe notoriamente para un lado, es una señal cuantitativa (no solo visual) de asimetría — el mismo chequeo aplica al leer un [[boxplot]], donde se traduce en una caja con la mediana descentrada hacia uno de los extremos.

## Gráficos emparentados

- **Polígono de frecuencias** → une los puntos medios de las cimas del histograma.
- **Ojiva** → polígono de frecuencias **acumuladas**; curva creciente de $H_i$, permite leer percentiles gráficamente. Desarrollada en detalle en [[función de distribución acumulada (CDF empírica)]].
- **[[diagrama de tallo y hoja]]** → como un histograma "acostado", pero sin perder los datos originales.
- **[[diagrama de puntos (dot plot)]]** → la versión sin agrupar en absoluto; conviene con pocos datos, donde agrupar en intervalos pierde demasiada información.

La asimetría descripta arriba de forma cualitativa se puede **cuantificar** con un número — ver [[coeficiente de asimetría (skewness)]].

> [!note] En código
> `sns.histplot(data=df, x="columna")` en Seaborn (ver [[05 - Distribuciones (histplot, kdeplot, ecdfplot)]]) — con `kde=True` superpone además la versión suavizada (KDE). `ax.hist()` en Matplotlib es la versión de más bajo nivel (ver [[04 - Tipos de graficos basicos]]). Esa curva KDE es `scipy.stats.gaussian_kde()` por debajo — una versión del histograma que no depende de dónde se corten los intervalos (ver [[09 - Estimacion de densidad y ajuste de distribuciones]]).

## Relacionado
- [[02 - El estudio de la variabilidad]]
- [[forma de una distribución]]
- [[distribución de frecuencias]]
- [[diagrama de tallo y hoja]] · [[boxplot]] · [[diagrama de puntos (dot plot)]]
- [[función de distribución acumulada (CDF empírica)]]
- [[coeficiente de asimetría (skewness)]]
- [[estratificación]]
- [[05 - Distribuciones (histplot, kdeplot, ecdfplot)]]
- [[09 - Estimacion de densidad y ajuste de distribuciones]]
