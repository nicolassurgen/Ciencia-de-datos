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
| Mediana, promedio truncado (parcial), RIQ, MAD | Media, rango, varianza / desvío estándar |

Las medidas robustas suelen basarse en **percentiles** (mediana, cuartiles, RIQ) en lugar de en **sumas y promedios de todos los valores** (media, varianza), que dan igual peso a cada observación, incluidas las extremas. La [[medidas de dispersión|desviación absoluta mediana (MAD)]] es, de todas, la más resistente a atípicos: tolera hasta la mitad de los datos siendo extremos sin distorsionarse.

## Por qué importa elegir bien

Si los datos tienen [[valores atípicos]] o vienen de una distribución asimétrica, resumir solo con media y desvío puede dar una imagen engañosa del "valor típico" y de la dispersión real. El [[boxplot]] es, en ese sentido, un resumen construido enteramente sobre medidas robustas.

> [!note] En código
> El ejemplo de arriba usa `numpy` y [[03 - Estadistica descriptiva|`scipy.stats.trim_mean`]] — ver [[03 - Ufuncs y operaciones vectorizadas]] y [[04 - Agregaciones y estadistica descriptiva]] de NumPy para el resto de las agregaciones vectorizadas.

## Relacionado
- [[02 - El estudio de la variabilidad]]
- [[valores atípicos]]
- [[medidas de posición]]
- [[tratamiento primario]]
- [[04 - Agregaciones y estadistica descriptiva]]
- [[03 - Estadistica descriptiva]]
