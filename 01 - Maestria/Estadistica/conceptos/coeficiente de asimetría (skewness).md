---
titulo: Coeficiente de asimetría (skewness)
materia: Estadística
tipo: concepto
tags:
  - estadistica
  - maestria
  - concepto
  - tema/variabilidad
fecha: 2026-08-08
---

# Coeficiente de asimetría (skewness)

Decir que un [[histograma]] es "asimétrico a la derecha" es una lectura **cualitativa**: describe la forma, pero no dice **cuánto** de asimétrica es una distribución, ni permite comparar objetivamente la asimetría de dos conjuntos de datos distintos. Hace falta un número que cuantifique esa idea — el mismo paso que ya se dio para el centro (media) y la dispersión (desvío estándar).

> [!definition] Coeficiente de asimetría de Pearson
> $$g_p = \frac{3(\bar y - \text{mediana})}{s}$$
> Cuantifica la asimetría aprovechando una idea ya conocida: en una distribución **asimétrica a la derecha**, la media queda por encima de la mediana (la cola de valores altos "arrastra" la media); en una **asimétrica a la izquierda**, ocurre lo opuesto. El coeficiente normaliza esa diferencia por el desvío estándar $s$ para que el resultado no dependa de la escala de la variable.
> - $g_p > 0$ → asimetría a la **derecha** (cola hacia valores altos).
> - $g_p < 0$ → asimetría a la **izquierda** (cola hacia valores bajos).
> - $g_p \approx 0$ → distribución aproximadamente simétrica.

## Ejemplo

```python
import numpy as np

# Asimétrica a la derecha: un valor alto estira la cola
x = np.array([10, 11, 11, 12, 12, 12, 13, 30])
media, mediana, s = np.mean(x), np.median(x), np.std(x, ddof=1)
g_p = 3 * (media - mediana) / s
print(media, mediana, round(s, 2), round(g_p, 2))
# 13.875 12.0 6.58 0.85   -> g_p > 0: asimetría a la derecha

# Asimétrica a la izquierda: un valor bajo estira la cola
y = np.array([20, 30, 31, 31, 32, 32, 33, 33])
media2, mediana2, s2 = np.mean(y), np.median(y), np.std(y, ddof=1)
g_p2 = 3 * (media2 - mediana2) / s2
print(media2, mediana2, round(s2, 2), round(g_p2, 2))
# 30.25 31.5 4.27 -0.88   -> g_p < 0: asimetría a la izquierda
```

En el primer caso, la media (13.9) queda muy por encima de la mediana (12) por el valor extremo 30 — exactamente lo que $g_p=0{,}85 > 0$ está cuantificando. En el segundo, la media (30.25) queda por debajo de la mediana (31.5), reflejado en $g_p=-0{,}88 < 0$.

> [!example] Formas reales de asimetría
> La duración del embarazo humano es un caso real de asimetría a la izquierda: la mayoría de los nacimientos ocurre cerca de las 39 semanas, pero los partos prematuros extienden la distribución hacia valores bajos, mientras que muy pocos embarazos superan las 43 semanas — el peso al nacer sigue un patrón similar. El ingreso de los hogares, en cambio, es un caso clásico de asimetría a la derecha: la mayoría gana montos moderados, pero una cola de ingresos muy altos estira la media hacia arriba sin mover demasiado la mediana. *Fuentes: [[Think Stats – Exploratory Data Analysis in Python]], cap. 2; [[Practical Statistics for Data Scientists]] (Bruce & Bruce), cap. 1-2.*

## Por qué esta versión es robusta (y otra versión no lo es)

El coeficiente de Pearson hereda la robustez de la mediana (ver [[robustez estadística]]): un valor extremo aislado mueve algo la media y el desvío, pero no descontrola el cociente. Existe una versión alternativa, el **tercer momento estandarizado** ($\frac{1}{n}\sum \left(\frac{y_i-\bar y}{s}\right)^3$), que es la definición "clásica" de skewness en muchos libros y software — pero al elevar al **cubo** cada desvío estandarizado, un solo valor atípico puede dominar completamente el resultado. Es **no robusta**, justo en el escenario (datos con atípicos o colas largas) donde medir la asimetría es más relevante. Para los mismos datos del ejemplo de arriba, `scipy.stats.skew()` da 2.72 para la primera muestra — un valor mucho más extremo que el $g_p=0{,}85$ de Pearson, producto exclusivamente del único dato atípico (30) elevado al cubo.

## Relacionado
- [[histograma]]
- [[robustez estadística]]
- [[medidas de posición]]
- [[medidas de dispersión]]
- [[valores atípicos]]
- [[02 - El estudio de la variabilidad]]
- [[03 - Estadistica descriptiva]]
