---
titulo: Robustez estadística
materia: Estadística
tipo: concepto
tags:
  - estadistica
  - maestria
  - concepto
  - tema/variabilidad
fecha: 2026-08-03
---

# Robustez estadística

> [!definition] Medida robusta
> Una medida de resumen es **robusta** cuando **no se distorsiona fuertemente** ante la presencia de [[valores atípicos]] o de asimetría en los datos. Una medida **no robusta**, en cambio, puede cambiar mucho por la influencia de solo una o pocas observaciones extremas.

## El ejemplo que lo muestra claramente

Partiendo de un vector "sano":

```python
import numpy as np
from scipy import stats

x = [2, 4, 3, 6, 3, 7, 5, 8, 7, 4]
np.mean(x)               # 4.9
stats.trim_mean(x, 0.1)  # 4.875
np.median(x)             # 4.5
```

Reemplazando el 8 por un valor cada vez más extremo:

| Dato extremo | Media | Media truncada (0.1) | Mediana |
|---|---:|---:|---:|
| … 8 … (original) | 4.9 | 4.875 | 4.5 |
| … **18** … | 5.9 | 4.875 | 4.5 |
| … **80** … | **12.1** | 4.875 | 4.5 |

> [!important] La lección
> Un **único** valor atípico dispara la **media** (de 4.9 a 12.1), mientras que la **mediana** y la **media truncada** ni se inmutan. Ante distribuciones **asimétricas o con atípicos**, la mediana suele describir mejor "el valor típico".

## Medidas robustas vs. no robustas

| Robustas | No robustas |
|---|---|
| Mediana, promedio truncado (parcial), RIQ, MAD, coeficiente de asimetría de Pearson | Media, rango, varianza / desvío estándar, tercer momento estandarizado (skewness "clásico") |

Las medidas robustas suelen basarse en **percentiles** (mediana, cuartiles, RIQ) en lugar de en **sumas y promedios de todos los valores** (media, varianza), que dan igual peso a cada observación, incluidas las extremas. La [[medidas de dispersión|desviación absoluta mediana (MAD)]] es, de todas, la más resistente a atípicos: tolera hasta la mitad de los datos siendo extremos sin distorsionarse. La misma lógica se aplica más allá de centro y dispersión: incluso para medir la **forma** de una distribución hay una versión robusta y una no robusta — ver [[coeficiente de asimetría (skewness)]].

## El porqué matemático: dos funciones de pérdida distintas

Media y mediana no son dos formas intercambiables de "medir el centro": cada una es la solución a un problema de minimización distinto, y esa diferencia explica formalmente por qué una es robusta y la otra no.

- La **media** es el valor $c$ que **minimiza la suma de errores al cuadrado**: $\bar y = \arg\min_c \sum_i (y_i - c)^2$ (la misma propiedad que fundamenta el $n-1$ en la varianza, ver [[grados de libertad]]).
- La **mediana** es el valor $c$ que **minimiza la suma de errores absolutos**: $\text{mediana} = \arg\min_c \sum_i |y_i - c|$.

Elevar al cuadrado penaliza fuertemente los errores grandes (el mismo argumento de la sección "Construyendo la varianza desde cero" en [[medidas de dispersión]]); el valor absoluto, en cambio, penaliza cada error en proporción directa a su tamaño, sin amplificar los extremos. Por eso la constante que minimiza el error cuadrático (la media) se deja arrastrar por un valor extremo mucho más que la que minimiza el error absoluto (la mediana): están resolviendo, literalmente, problemas distintos. *Fuente: [[The Elements of Statistical Learning]], cap. 2.*

## Por qué importa elegir bien

Si los datos tienen [[valores atípicos]] o vienen de una distribución asimétrica, resumir solo con media y desvío puede dar una imagen engañosa del "valor típico" y de la dispersión real. El [[boxplot]] es, en ese sentido, un resumen construido enteramente sobre medidas robustas.

> [!note] En código
> El ejemplo de arriba usa `numpy` y [[03 - Estadistica descriptiva|`scipy.stats.trim_mean`]] — ver [[03 - Ufuncs y operaciones vectorizadas]] y [[04 - Agregaciones y estadistica descriptiva]] de NumPy para el resto de las agregaciones vectorizadas.

## Relacionado
- [[02 - El estudio de la variabilidad]]
- [[valores atípicos]]
- [[medidas de posición]]
- [[medidas de dispersión]]
- [[grados de libertad]]
- [[coeficiente de asimetría (skewness)]]
- [[tratamiento primario]]
- [[04 - Agregaciones y estadistica descriptiva]]
- [[03 - Estadistica descriptiva]]
