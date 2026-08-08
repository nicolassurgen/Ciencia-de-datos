---
titulo: Población y muestra
materia: Estadística
tipo: concepto
tags:
  - estadistica
  - maestria
  - concepto
  - tema/introduccion
fecha: 2026-08-03
---

# Población y muestra

> [!definition] Población
> Conjunto de **todos** los elementos (unidades elementales) bajo estudio. Puede ser **finita o infinita**. Debe estar **perfectamente delimitada en tiempo y espacio**, usando **criterios de inclusión/exclusión**. Su tamaño se denota $N$.

> [!definition] Muestra
> Un **subconjunto** de la población, seleccionado para estudiarla sin observar todas sus unidades. Su tamaño se denota $n$.

> [!definition] Unidad elemental
> Cada uno de los elementos que componen la población; la "unidad de análisis" sobre la que se miden las variables.

## Censo vs. muestreo

- **Estudio poblacional (censo)** → se observan **todas** las unidades de la población. Las conclusiones son **definitivas** para esa población: no hace falta inferencia.
- **Estudio por muestreo** → se observa solo una parte. Requiere **herramientas de inferencia** (intervalos de confianza, pruebas de hipótesis) para generalizar a toda la población, con un **margen de error** y **riesgos controlados**.

> [!tip] ¿Por qué muestrear en vez de censar?
> Un censo suele ser más costoso, más lento o directamente inviable (por ejemplo, si medir implica destruir el producto). El muestreo cambia certeza total por costo/tiempo, a condición de definir bien el **tipo** y el **tamaño** de la muestra.
>
> Hay además una razón práctica más allá del costo: revisar manualmente la **calidad** de los datos (outliers, faltantes, errores de carga — ver [[tratamiento primario]]) es viable sobre una muestra de miles de registros, pero prohibitivo sobre millones. Trabajar con una muestra manejable no es solo "más barato": también permite controlar mejor lo que se está midiendo.
>
> Esto no es absoluto: hay problemas donde el muestreo **no ayuda** y de verdad hace falta todo el volumen de datos disponible (el ejemplo típico son sistemas con eventos muy raros o relaciones muy dispersas entre variables, donde reducir el volumen puede hacer directamente invisible el fenómeno que se busca). La decisión de muestrear o no depende del problema, no es una regla universal. *Fuente: [[Practical Statistics for Data Scientists]] (Bruce & Bruce), cap. 2.*

> [!example] Muestreo deliberadamente no proporcional (oversampling)
> No toda muestra aleatoria reparte los estratos en la misma proporción que la población. La Encuesta Nacional de Crecimiento Familiar de EE.UU. (NSFG), por ejemplo, **sobremuestreó deliberadamente** a hispanos, afroamericanos y adolescentes: los incluyó en una proporción mayor a su peso real en la población, para poder sacar conclusiones confiables también sobre esos subgrupos específicos (que en una muestra puramente proporcional habrían quedado con muy pocos casos). El costo de esa decisión: generalizar directamente de esta muestra a "la población general" requiere corregir esa sobrerrepresentación (ponderar de vuelta), no promediar los datos tal cual vinieron. Es un ejemplo concreto de por qué "aleatorio" no es sinónimo de "proporcional a la población". *Fuente: [[Think Stats – Exploratory Data Analysis in Python]], cap. 1.*

> [!info] A futuro: cuantificar ese margen de error
> `scipy.stats.bootstrap()` (ver [[08 - Metodos de remuestreo]]) simula computacionalmente qué pasaría si se repitiera el muestreo muchas veces, usando la muestra que sí se tiene — la forma más directa de responder "¿con qué margen de error estima esto a la población?" sin fórmulas cerradas.
>
> En ese contexto de inferencia, conviene distinguir dos fuentes de error que hoy se tratan juntas de forma informal: el **sesgo de muestreo** (la muestra en sí no representa bien a la población, por cómo se seleccionó) y el **error de medición** (cada dato individual está mal registrado, aunque la muestra esté bien elegida). Son problemas distintos con soluciones distintas — el primero se ataca con mejor diseño muestral, el segundo con mejor [[tratamiento primario]] — pero la materia todavía no los separó formalmente.

## Por qué definir bien la población

De la definición de la población depende la [[validez externa]] de las conclusiones: hasta qué grupo se tiene derecho a extender lo encontrado en la muestra. Una muestra puede ser perfectamente representativa de una población mal delimitada, y aun así llevar a conclusiones que no generalizan al grupo que realmente interesaba.

## Relacionado
- [[01 - Como dar sentido a los datos]]
- [[parámetro vs estadístico]]
- [[validez externa]] · [[sesgo de autoselección]]
- [[08 - Metodos de remuestreo]]
