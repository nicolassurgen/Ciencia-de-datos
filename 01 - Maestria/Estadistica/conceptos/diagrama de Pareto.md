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

> [!important] "Más frecuente" no siempre es "más importante"
> El Pareto se construye por defecto ordenando por **frecuencia**, pero esa no es la única forma de medir "importancia" de una categoría: también se puede ordenar por **costo** o por **tiempo insumido**, y el resultado puede cambiar por completo. En una fábrica de turbinas, el defecto más *frecuente* era un problema de pintura (62 % de los casos) — pero el más *costoso* era un rodete defectuoso, presente en solo el 4 % de los casos y responsable, sin embargo, del 36 % del costo total de los defectos. Un Pareto armado solo por frecuencia habría llevado a priorizar mal: el problema "poco vital" en cantidad de casos era, en plata, el más vital de todos. Antes de construir el diagrama conviene preguntarse explícitamente **qué variable de importancia es la relevante para la decisión que se quiere tomar**. *Fuente: [[Estadística para la resolución de problemas en Ingeniería]], cap. 2.*

> [!note] En código
> La curva acumulada que se superpone a las barras es la misma idea que `scipy.stats.cumfreq()` (ver [[04 - Frecuencias, cuantiles y percentiles]]), aplicada acá a categorías ya ordenadas en vez de a intervalos numéricos.

## Relacionado
- [[02 - El estudio de la variabilidad]]
- [[distribución de frecuencias]]
- [[diagrama de Ishikawa]]
- [[04 - Frecuencias, cuantiles y percentiles]]
