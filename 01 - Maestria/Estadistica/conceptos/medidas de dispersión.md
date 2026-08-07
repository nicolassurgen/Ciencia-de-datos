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
> donde $q_1$ (primer cuartil) es el valor que deja el 25 % de los datos por debajo, y $q_3$ (tercer cuartil) el que deja el 75 % por debajo — ver [[medidas de posición]] para su definición completa. El RIQ es la amplitud del **50 % central** de los datos. **Robusto**: al ignorar el 25 % de cada extremo, no lo afectan los atípicos. Es el compañero natural de la mediana (ver [[medidas de posición]]) y es el largo de la caja en un [[boxplot]].

### Construyendo la varianza desde cero

El rango y el RIQ resumen la dispersión mirando solo un par de puntos (los extremos, o los cuartiles). Una medida más completa debería usar **todos** los datos: la distancia de cada observación a la media, $y_i - \bar{y}$ (el **desvío**).

El primer intento natural sería promediar esos desvíos. Pero eso no funciona: por cómo se define la media, los desvíos positivos y negativos se cancelan exactamente, y el promedio da **siempre cero** — sin importar cuánto varíen realmente los datos:

$$\sum_{i=1}^{n}(y_i - \bar{y}) = 0 \quad \text{siempre}$$

Elevar cada desvío al cuadrado resuelve ese problema: $(y_i - \bar{y})^2$ es siempre positivo, así que ya no se cancela, y además **penaliza más los desvíos grandes** que los chicos (un dato que se aparta el doble de la media pesa cuatro veces más en la suma). Esa suma de cuadrados, promediada, es la varianza:

> [!definition] Varianza y desvío estándar
> $$s^{2} = \frac{\sum_{i=1}^{n}(y_i - \bar{y})^{2}}{n-1}$$
> $$s = \sqrt{s^{2}}$$
> $s^2$ queda en **unidades al cuadrado** de la variable original (si $y$ está en mm, $s^2$ está en mm²) — una consecuencia directa de haber elevado al cuadrado, y por eso no es fácil de interpretar directamente. Sacar la raíz cuadrada, el **desvío estándar** $s$, devuelve el resultado a las unidades originales, y se interpreta como un "promedio" de cuánto se aparta cada dato de la media. Es **NO robusto** (se calcula a partir de la media y de cuadrados, que amplifican los extremos). Sobre el $n-1$ del denominador (en vez de $n$), ver [[grados de libertad]].

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
