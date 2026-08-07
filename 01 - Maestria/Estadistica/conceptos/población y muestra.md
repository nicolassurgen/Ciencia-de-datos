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

> [!info] A futuro: cuantificar ese margen de error
> `scipy.stats.bootstrap()` (ver [[08 - Metodos de remuestreo]]) simula computacionalmente qué pasaría si se repitiera el muestreo muchas veces, usando la muestra que sí se tiene — la forma más directa de responder "¿con qué margen de error estima esto a la población?" sin fórmulas cerradas.

## Por qué definir bien la población

De la definición de la población depende la [[validez externa]] de las conclusiones: hasta qué grupo se tiene derecho a extender lo encontrado en la muestra. Una muestra puede ser perfectamente representativa de una población mal delimitada, y aun así llevar a conclusiones que no generalizan al grupo que realmente interesaba.

## Relacionado
- [[01 - Como dar sentido a los datos]]
- [[parámetro vs estadístico]]
- [[validez externa]] · [[sesgo de autoselección]]
- [[08 - Metodos de remuestreo]]
