---
titulo: Medidas de posición (centrado)
materia: Estadística
tipo: concepto
tags:
  - estadistica
  - maestria
  - concepto
  - tema/variabilidad
fecha: 2026-08-03
---

# Medidas de posición (centrado)

Responden a la pregunta **¿dónde se centra** la distribución?

> [!definition] Media (promedio)
> $$\bar{y} = \frac{1}{n}\sum_{i=1}^{n} y_i$$
> Usa **toda** la información, pero es **NO robusta**: un solo valor atípico la puede correr mucho. Ver [[robustez estadística]].

> [!definition] Mediana
> Valor que **acumula el 50 %** de las observaciones ordenadas: $F(x^{*}) = 0{,}50$. Es **robusta**: no la afectan los valores extremos.

> [!definition] Promedio truncado (trimmed mean)
> Se elimina un porcentaje de datos en **cada extremo** de la distribución y se promedian los restantes (p. ej. `trim = 0.1` descarta el 10 % de cada lado). Compromiso entre aprovechar casi todos los datos y ganar robustez.

> [!definition] Moda
> El valor o categoría **más frecuente**. Es la única medida de centro que sirve también para variables cualitativas nominales.

> [!info] Material complementario (no visto en clase) — Media y mediana ponderadas
> $$\bar{y}_w = \frac{\sum_i w_i y_i}{\sum_i w_i}$$
> Igual que la media, pero cada dato **pesa distinto** según su importancia relativa (`w_i`) en vez de pesar todos por igual. Útil cuando algunos grupos están sobre o subrepresentados en la muestra respecto de la población, o cuando algunos datos son intrínsecamente más variables (y conviene darles menos peso). La **mediana ponderada** aplica la misma idea: se ordenan los datos y se busca el punto donde la suma de pesos se reparte mitad y mitad, en vez de contar observaciones. Ambas siguen siendo **robustas** si la mediana lo es. *Fuente: [[Practical Statistics for Data Scientists]] (Bruce & Bruce), cap. 1.*

## Qué medida usar según la escala

- **Nominal** → solo **moda**.
- **Ordinal** → moda y **mediana / percentiles**.
- **Cuantitativa (intervalo/razón)** → todas (media, mediana, truncado, moda).

Ver [[escalas de medición]] para el detalle de las escalas.

## Percentiles y cuartiles

Con la misma lógica de la mediana se definen otros cortes de la distribución ordenada:

- **Cuartiles** → dividen en 4 partes: $q_1$ (25 %), $q_2$ = mediana (50 %), $q_3$ (75 %).
- **Percentiles** → dividen en 100 partes: $P_{35}$ acumula el 35 % de los datos.

> [!warning] No siempre hay un valor exacto
> Especialmente en variables discretas, puede no existir un dato que acumule *exactamente* ese porcentaje. Existen distintos métodos de interpolación, y por eso software distinto puede dar valores levemente distintos.

## Robustez: tabla resumen

| Medida | ¿Robusta? |
|---|:---:|
| Media | ❌ |
| Mediana | ✅ |
| Promedio truncado | ✅ (parcial) |

> [!tip] Combiná centro + dispersión coherentes
> Si describís con la **media**, acompañala con el **desvío estándar**. Si usás la **mediana**, acompañala con el **RIQ**. Ver [[medidas de dispersión]].

> [!note] En código
> `np.mean()`, `np.median()`, `np.percentile()` ([[04 - Agregaciones y estadistica descriptiva]] de NumPy) calculan cada una de estas medidas sobre un array. Sobre un DataFrame completo, `df.describe()` ([[01 - Introduccion a Series y DataFrame]] de Pandas) las da todas juntas, columna por columna, de una sola vez. Para la moda y el promedio truncado (que NumPy no tiene), `scipy.stats.mode()` y `scipy.stats.trim_mean()` (ver [[03 - Estadistica descriptiva]] de SciPy) completan el resto. La media ponderada es `np.average(x, weights=w)`; la mediana ponderada no tiene función en NumPy/SciPy — `statsmodels.stats.weightstats.DescrStatsW(x, weights=w).quantile(0.5)` sí la calcula.

## Relacionado
- [[02 - El estudio de la variabilidad]]
- [[medidas de dispersión]]
- [[robustez estadística]]
- [[boxplot]]
- [[04 - Agregaciones y estadistica descriptiva]]
- [[03 - Estadistica descriptiva]]
- [[Practical Statistics for Data Scientists]]
