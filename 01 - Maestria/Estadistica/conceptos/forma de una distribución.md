---
titulo: Forma de una distribución
materia: Estadística
tipo: concepto
tags:
  - estadistica
  - maestria
  - concepto
  - tema/variabilidad
fecha: 2026-08-19
---

# Forma de una distribución

Dos conjuntos de datos pueden tener exactamente la misma media y el mismo desvío estándar y, aun así, verse completamente distintos al graficarlos: uno con un solo pico bien centrado, el otro con dos grupos separados, o con una cola larga hacia un lado. Centro y dispersión no agotan la descripción de una [[distribución estadística|distribución]] — falta una tercera pregunta: **¿qué forma tiene?**

> [!definition] Forma de una distribución
> Describe el **patrón general** con el que se reparten los valores: cuántos picos tiene (modalidad), si es simétrica o está "estirada" hacia un lado (asimetría), y qué tan largas son sus colas. Es la tercera de las tres preguntas que describen una distribución completa, junto con [[medidas de posición|centro]] y [[medidas de dispersión|dispersión]].

## Modalidad: cuántos picos tiene

> [!quote] Unimodal, bimodal, multimodal
> "En un conjunto puede existir una única moda (distribución unimodal) o bien más de una (distribución bimodal si se presentan dos, o multimodal si son más de dos modas); también es posible que no exista ninguna si todos los valores de la variable se dan con frecuencias similares." *Fuente: [[Estadística para la resolución de problemas en Ingeniería]], cap. 2.*

> [!important] Un histograma bimodal es una pista, no un resultado final
> Cuando aparecen dos picos claramente separados, casi siempre es señal de que los datos mezclan **dos poblaciones distintas** (por ejemplo, la misma pieza fabricada en dos máquinas, o mediciones tomadas en dos turnos). La forma bimodal es la pista visual de que conviene [[estratificación|estratificar]] — separar el conjunto en subgrupos y analizar cada uno por separado — en vez de seguir describiendo el conjunto mezclado con un único centro y una única dispersión, que no representarían bien a ninguno de los dos subgrupos.

## Simetría y asimetría

> [!definition] Distribución simétrica
> "Una distribución es simétrica cuando valores (o intervalos de valores) de la variable equidistantes de la media presentan frecuencias similares a ambos lados de la misma [...] En las distribuciones perfectamente simétricas la media y la mediana coinciden y si además, la distribución es unimodal, la moda coincide con ellas." *Fuente: [[Estadística para la resolución de problemas en Ingeniería]], cap. 2.*

Cuando esa simetría se rompe, hay dos formas posibles:

> [!definition] Asimetría a la derecha (positiva)
> Las observaciones están más concentradas a la izquierda de la media y más dispersas a su derecha; la **cola derecha** es más larga. Como consecuencia, el promedio queda por encima de la mediana, que a su vez queda por encima de la moda. *Fuente: [[Estadística para la resolución de problemas en Ingeniería]], cap. 2.*

> [!definition] Asimetría a la izquierda (negativa)
> El patrón simétrico al anterior: la cola izquierda es más larga, y el promedio queda por debajo de la mediana y la moda. *Fuente: [[Estadística para la resolución de problemas en Ingeniería]], cap. 2.*

> [!tip] Se nombra por dónde está la cola, no por dónde está el pico
> Es el error más común al leer un histograma asimétrico: la forma se llama "asimétrica a la derecha" o "a la izquierda" según hacia dónde se estira la **cola** (los valores menos frecuentes y más extremos), no según dónde está la moda (el pico, que suele estar del lado opuesto a la cola).

Ejemplos reales de ambos patrones, con datos verificados y gráfico embebido, en [[histograma]].

## Colas: qué tan extremos pueden ser los valores raros

> [!quote] Tails
> "Sometimes, the distribution is highly skewed (asymmetric), such as with income data [...] Both symmetric and asymmetric distributions may have long tails. The tails of a distribution correspond to the extreme values (small and large)." *Fuente: [[Practical Statistics for Data Scientists]] (Bruce & Bruce), cap. 1.*

Una distribución puede ser simétrica y aun así tener **colas largas** (valores extremos poco frecuentes pero mucho más probables de lo que la intuición esperaría) — el ejemplo clásico son los retornos diarios de una acción, donde eventos de variación grande ocurren con más frecuencia de la que sugeriría una distribución "bien comportada". Simetría/asimetría y "cola larga" son dos ejes de la forma que no siempre van juntos: hay que evaluarlos por separado.

## De lo cualitativo a lo cuantitativo

Todo lo anterior es una lectura **visual y cualitativa** de la forma — útil, pero que no permite decir "esta distribución es más asimétrica que aquella" con un número. Ese paso siguiente, cuantificar la asimetría con una fórmula concreta y compararla entre conjuntos de datos, está desarrollado en [[coeficiente de asimetría (skewness)]].

> [!note] En código
> `sns.histplot(data=df, x="columna", kde=True)` (ver [[05 - Distribuciones (histplot, kdeplot, ecdfplot)]] de Seaborn) es la forma más rápida de ver la forma de una distribución de un vistazo. `scipy.stats.skew()` la cuantifica (ver [[coeficiente de asimetría (skewness)]] para sus matices de robustez).

## Relacionado
- [[distribución estadística]]
- [[histograma]]
- [[coeficiente de asimetría (skewness)]]
- [[estratificación]]
- [[medidas de posición]] · [[medidas de dispersión]]
- [[02 - El estudio de la variabilidad]]
