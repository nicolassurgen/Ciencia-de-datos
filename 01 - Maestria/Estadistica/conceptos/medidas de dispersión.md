---
titulo: Medidas de dispersión (variabilidad)
materia: Estadística
tipo: concepto
tags:
  - estadistica
  - maestria
  - concepto
  - tema/variabilidad
fecha: 2026-08-03
---

# Medidas de dispersión (variabilidad)

Responden a la pregunta **¿cuánto se dispersa** la distribución?

> [!definition] Rango
> $$\text{rango} = x_{\max} - x_{\min}$$
> Simple, pero **muy NO robusto**: depende únicamente de los dos valores más extremos.

> [!definition] Rango intercuartílico (RIQ / IQR)
> $$\text{RIQ} = q_3 - q_1$$
> Amplitud del **50 % central** de los datos. **Robusto**: al ignorar el 25 % de cada extremo, no lo afectan los atípicos. Es el compañero natural de la mediana (ver [[medidas de posición]]) y es el largo de la caja en un [[boxplot]].

> [!definition] Varianza y desvío estándar
> $$s^{2} = \frac{\sum_{i=1}^{n}(y_i - \bar{y})^{2}}{n-1}$$
> $$s = \sqrt{s^{2}}$$
> El desvío estándar se interpreta como un "promedio" de cuánto se aparta cada dato de la media, y tiene las **mismas unidades** que la variable. Es **NO robusto** (se calcula a partir de la media y de cuadrados, que amplifican los extremos). Sobre el $n-1$ del denominador, ver [[grados de libertad]].

> [!definition] Coeficiente de variación (CV)
> Ver nota aparte: [[coeficiente de variación]].

> [!info] Material complementario (no visto en clase) — Desviación absoluta mediana (MAD)
> $$\text{MAD} = \text{mediana}(\,|y_i - \text{mediana}(y)|\,)$$
> La mediana de las distancias absolutas de cada dato a la mediana. Es, en cierto sentido, el robusto **más robusto**: mientras el RIQ ignora el 25 % de cada extremo, el MAD tolera hasta la **mitad** de los datos siendo atípicos sin distorsionarse (su *breakdown point* es 50 %, el máximo posible). Es el análogo, para la dispersión, de lo que la mediana es para el centro. *Fuente: [[Practical Statistics for Data Scientists]] (Bruce & Bruce), cap. 1.*

## Robustez: tabla resumen

| Medida | ¿Robusta? | Va de la mano con |
|---|:---:|---|
| Rango | ❌ | — |
| RIQ | ✅ | Mediana |
| Varianza / Desvío estándar | ❌ | Media |
| MAD | ✅ (la más robusta de todas) | Mediana |

> [!tip] Combiná centro + dispersión coherentes
> Si describís con la **media**, acompañala con el **desvío estándar**. Si usás la **mediana** (por atípicos o asimetría), acompañala con el **RIQ**. Mezclar media con RIQ, o mediana con desvío, es menos coherente.

> [!note] En código
> `np.std(x, ddof=1)`, `np.var(x, ddof=1)` (ver [[04 - Agregaciones y estadistica descriptiva]] de NumPy) calculan estas medidas — ojo con `ddof=1` para la varianza **muestral**. El RIQ tiene función propia en [[03 - Estadistica descriptiva|`scipy.stats.iqr(x)`]], que ya usa la clase 2 sin desarrollar. `df.describe()` de Pandas ya incluye desvío estándar y cuartiles por columna. El MAD se calcula con `scipy.stats.median_abs_deviation(x)`.

## Relacionado
- [[02 - El estudio de la variabilidad]]
- [[medidas de posición]]
- [[coeficiente de variación]]
- [[grados de libertad]]
- [[boxplot]] · [[valores atípicos]]
- [[04 - Agregaciones y estadistica descriptiva]]
- [[03 - Estadistica descriptiva]]
- [[Practical Statistics for Data Scientists]]
