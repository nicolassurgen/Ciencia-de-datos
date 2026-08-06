---
titulo: Coeficiente de variación
materia: Estadística
tipo: concepto
tags:
  - estadistica
  - maestria
  - concepto
  - tema/variabilidad
fecha: 2026-08-03
---

# Coeficiente de variación

> [!definition] Coeficiente de variación (CV)
> Medida de dispersión **relativa** y **adimensional**, que expresa el desvío estándar como porcentaje de la media:
> $$CV = \frac{s}{\bar{y}} \times 100\ \%$$

## Para qué sirve

A diferencia del desvío estándar (que tiene las mismas unidades que la variable), el CV **no tiene unidades**, lo que permite **comparar la variabilidad de variables distintas** o medidas en escalas distintas — por ejemplo, ¿varía proporcionalmente más el diámetro o el peso de una pieza?

> [!tip] Un mismo desvío "pesa" distinto según la media
> Un desvío estándar de 5 es enorme si la media es 10, pero irrelevante si la media es 10.000. El CV normaliza esa comparación.

## Limitaciones

- Solo tiene sentido para variables en **escala de razón** (con cero absoluto): en escala de intervalo (p. ej. temperatura en °C), dividir por la media no es interpretable porque el cero es arbitrario. Ver [[escalas de medición]].
- Si la media está **cerca de cero**, el CV se vuelve inestable (puede dispararse o cambiar de signo).

## En Python

Se calcula como:
```python
import numpy as np

CV = np.std(x, ddof=1) * 100 / np.mean(x)
```

> [!warning] Ojo con `ddof`
> `numpy.std()` por defecto divide por $n$ (varianza poblacional). Para replicar el `sd()` de R —que usa $n-1$, ver [[grados de libertad]]— hay que pasar `ddof=1` explícitamente. Si tu profesora comparte una salida calculada en R y tratás de reproducirla en Python sin este detalle, el número te va a quedar levemente distinto.

> [!tip] La versión de una sola función
> `scipy.stats.variation(x)` (ver [[03 - Estadistica descriptiva]]) calcula lo mismo directo, sin armarlo a mano — aunque ojo, no multiplica por 100: devuelve el cociente crudo.

## Relacionado
- [[02 - El estudio de la variabilidad]]
- [[medidas de dispersión]]
- [[escalas de medición]]
- [[04 - Agregaciones y estadistica descriptiva]]
- [[03 - Estadistica descriptiva]]
