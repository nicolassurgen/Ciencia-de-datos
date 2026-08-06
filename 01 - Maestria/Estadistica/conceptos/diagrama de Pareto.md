---
titulo: Diagrama de Pareto
materia: Estadística
tipo: concepto
tags:
  - estadistica
  - maestria
  - concepto
  - tema/variabilidad
fecha: 2026-08-03
---

# Diagrama de Pareto

> [!definition] Diagrama de Pareto
> Gráfico para una variable **cualitativa** (categórica) que combina **barras ordenadas de mayor a menor** frecuencia con una **curva de frecuencia acumulada** superpuesta. Ver [[distribución de frecuencias]] para la tabla de frecuencias que lo sustenta.

## La regla 80/20

> [!example] Ejemplo — quejas de una ferretería
> Con 350 quejas registradas y motivos ordenados por frecuencia, **Factura + Envases + Dimensiones** ya explican cerca del 70 % de las quejas. El Pareto permite identificar los **"pocos vitales"**: las pocas categorías que concentran la mayor parte del problema, donde conviene concentrar los esfuerzos de mejora.

La idea detrás (popularizada por Joseph Juran a partir del principio de Pareto) es que en muchos fenómenos, una minoría de las categorías explica la mayoría del efecto total — de ahí el nombre informal "regla 80/20".

## Construcción

1. Ordenar las categorías de **mayor a menor** frecuencia (a diferencia de un gráfico de barras común, donde el orden puede ser arbitrario o alfabético).
2. Dibujar las barras de frecuencia (absoluta o relativa).
3. Superponer una curva con la **frecuencia relativa acumulada** ($H_i$), leída en un eje secundario que va de 0 % a 100 %.

## Por qué el orden importa

El ordenamiento decreciente es lo que hace visible **dónde está el "codo"**: el punto a partir del cual agregar más categorías aporta poco a la frecuencia acumulada. Es una herramienta clásica de la gestión de la calidad para priorizar sobre qué actuar primero.

> [!note] En código
> La curva acumulada que se superpone a las barras es la misma idea que `scipy.stats.cumfreq()` (ver [[04 - Frecuencias, cuantiles y percentiles]]), aplicada acá a categorías ya ordenadas en vez de a intervalos numéricos.

## Relacionado
- [[02 - El estudio de la variabilidad]]
- [[distribución de frecuencias]]
- [[diagrama de Ishikawa]]
- [[04 - Frecuencias, cuantiles y percentiles]]
