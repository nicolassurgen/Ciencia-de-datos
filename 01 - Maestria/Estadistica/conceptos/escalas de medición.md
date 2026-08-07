---
titulo: Escalas de medición
materia: Estadística
tipo: concepto
tags:
  - estadistica
  - maestria
  - concepto
  - tema/introduccion
fecha: 2026-08-03
---

# Escalas de medición

Cuatro escalas, en orden creciente de "qué operaciones permiten". Cada escala **acumula** las capacidades de la anterior: razón permite todo lo que permite intervalo, más los cocientes.

| Escala | ¿Distingue? | ¿Ordena? | ¿Diferencias? | ¿Cocientes? | Cero absoluto | Asociada a | Ejemplo |
|---|:---:|:---:|:---:|:---:|:---:|---|---|
| **Nominal** | ✅ | ❌ | ❌ | ❌ | — | Cualitativas | Material de la vivienda; motivo de consulta |
| **Ordinal** | ✅ | ✅ | ❌ | ❌ | — | Cuali/cuanti* | Nivel de estudios; nivel de contaminación (bajo/medio/alto) |
| **Intervalo** | ✅ | ✅ | ✅ | ❌ | No | Cuantitativas | Temperatura en °C |
| **Razón** | ✅ | ✅ | ✅ | ✅ | **Sí** | Cuantitativas | Nivel de colesterol; peso; ingreso |

\* Las ordinales son un caso frontera: se tratan como cualitativas si tienen pocos niveles, o como cuantitativas si tienen muchos.

## Detalle de cada escala

- **Nominal** — solo permite *distinguir* una unidad de otra. No hay orden entre categorías.
- **Ordinal** — distingue **y ordena**, pero las distancias entre categorías no son necesariamente comparables.
- **Intervalo** — distingue, ordena y permite **restar** (diferencias), pero **no cocientes**, porque el **0 no es absoluto**. 20 °C es 10 grados más que 10 °C, pero no es "el doble" de calor.
- **Razón** — permite todo, **incluidos los cocientes**, porque el **0 es absoluto**. 220 mg/l de colesterol es 20 mg/l más *y* un 10 % más que 200 mg/l; esa afirmación solo es válida en escala de razón.

> [!tip] Para el análisis, ¿qué distinción importa más?
> Entre **intervalo y razón**, para el análisis de datos **no suele importar** la diferencia. Lo que **sí importa siempre** es distinguir si la variable cuantitativa es **discreta o continua**.

## Qué medida de resumen permite cada escala

- **Nominal** → solo **moda**.
- **Ordinal** → moda y **mediana / percentiles**.
- **Intervalo / Razón** → todas: media, mediana, moda, promedio truncado, percentiles.

Ver el detalle en [[medidas de posición]].

> [!note] En código
> Pandas tiene un `dtype` dedicado para esto: `pd.Categorical(x, categories=[...], ordered=True)` distingue nominal de ordinal explícitamente (con `ordered=True`, respeta el orden al graficar y comparar). Ver [[01 - Introduccion a Series y DataFrame]].

> [!info] A futuro: la escala también decide qué test de asociación usar
> Igual que decide qué medida de resumen corresponde (arriba), la escala de medición decide qué test de correlación es válido entre dos variables: `pearsonr` para razón/intervalo, `spearmanr` para ordinal, `chi2_contingency` para nominal. Ver [[07 - Correlacion y tests de asociacion]] de SciPy.

## Relacionado
- [[01 - Como dar sentido a los datos]]
- [[medidas de posición]]
- [[parámetro vs estadístico]]
- [[01 - Introduccion a Series y DataFrame]]
- [[07 - Correlacion y tests de asociacion]]
- [[09 - Colorbars y mapas de color]]
