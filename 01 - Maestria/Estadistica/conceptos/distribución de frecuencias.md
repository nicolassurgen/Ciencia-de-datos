---
titulo: Distribución de frecuencias
materia: Estadística
tipo: concepto
tags:
  - estadistica
  - maestria
  - concepto
  - tema/variabilidad
fecha: 2026-08-03
---

# Distribución de frecuencias

> [!definition] Distribución de frecuencias
> La forma más básica de representar la **variabilidad** de una variable: una tabla que indica, para cada valor o categoría, **cuántas veces aparece** en el conjunto de datos.

## Tipos de frecuencia

| Frecuencia | Símbolo | Qué mide |
|---|---|---|
| **Absoluta** | $f_i$ | Cantidad de casos en la categoría/valor $i$ |
| **Relativa** | $h_i = f_i / n$ | Proporción del total (útil para comparar entre conjuntos de distinto tamaño) |
| **Absoluta acumulada** | $F_i$ | Casos hasta $i$ (solo tiene sentido si la variable está ordenada) |
| **Relativa acumulada** | $H_i$ | Proporción acumulada hasta $i$ |

> [!warning] Las acumuladas necesitan orden
> Solo se pueden acumular frecuencias si la variable tiene un **orden natural** (ordinal, discreta o continua). Para una variable **nominal** no tiene sentido "acumular": no hay un antes y un después entre las categorías.

## Según el tipo de variable

- **Cualitativa** → tabla de $f_i$/$h_i$ por categoría. Gráficos: torta, barras, [[diagrama de Pareto]].
- **Cuantitativa discreta** → tabla por valor entero, con acumuladas. Gráficos: diagrama de bastones, función de distribución empírica.
- **Cuantitativa continua** → los valores casi no se repiten, por lo que se agrupan en **intervalos de clase** (p. ej. `(89, 92]`, abierto a la izquierda y cerrado a la derecha, para que cada dato caiga en un único intervalo). Gráficos: [[histograma]], polígono de frecuencias, ojiva, [[diagrama de tallo y hoja]].

## Cuándo NO usarla

Si los datos tienen una **dimensión temporal** y el proceso no es estable, aplastar el tiempo en una distribución de frecuencias borra la información más relevante. En ese caso corresponde una [[series de tiempo|serie de tiempo]] en su lugar.

> [!note] En código
> `df['columna'].value_counts()` en Pandas da la tabla de frecuencias absolutas de una variable cualitativa en una línea (`normalize=True` para relativas). Para graficarla: `sns.histplot()` (cuantitativas, ver [[05 - Distribuciones (histplot, kdeplot, ecdfplot)]]) o `sns.countplot()` (cualitativas, ver [[06 - Variables categoricas (boxplot, violinplot, barplot)]]) en Seaborn. Para las acumuladas por intervalo, `scipy.stats.cumfreq()` arma directo la columna $F_i$ agrupada en bins (ver [[04 - Frecuencias, cuantiles y percentiles]]).

## Relacionado
- [[02 - El estudio de la variabilidad]]
- [[histograma]] · [[diagrama de tallo y hoja]]
- [[diagrama de Pareto]]
- [[series de tiempo]]
- [[05 - Distribuciones (histplot, kdeplot, ecdfplot)]]
- [[04 - Frecuencias, cuantiles y percentiles]]
