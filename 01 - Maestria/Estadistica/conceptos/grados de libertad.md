---
titulo: Grados de libertad
materia: Estadística
tipo: concepto
tags:
  - estadistica
  - maestria
  - concepto
  - tema/variabilidad
fecha: 2026-08-03
---

# Grados de libertad

> [!definition] Grados de libertad
> Cantidad de valores de un conjunto de datos que son **libres de variar** una vez que se han impuesto ciertas restricciones (como fijar la media). En el cálculo de la varianza muestral, se usan $n - 1$ grados de libertad.

## ¿Por qué se divide por $n-1$ y no por $n$?

$$s^{2} = \frac{\sum_{i=1}^{n}(y_i - \bar{y})^{2}}{n-1}$$

Cuando los datos son una **muestra** y se usa $\bar{y}$ (estimada a partir de los propios datos) para estimar la variabilidad de la población, dividir por $n$ **subestima** la varianza poblacional. Dividir por $n-1$ corrige ese sesgo.

Intuición: una vez que se fija $\bar{y}$, solo $n-1$ de los $n$ desvíos $(y_i - \bar{y})$ son "libres" — el último queda determinado por los demás, porque la suma de todos los desvíos respecto de la media es siempre 0. Por eso quedan $n-1$ grados de libertad, no $n$.

## Población vs. muestra

> [!info] Distinta notación según el caso
> - **Muestra** → estadístico $s^2$ (varianza), $s$ (desvío), divide por $n-1$.
> - **Población completa** → parámetro $\sigma^2$ (varianza poblacional), $\sigma$ (desvío poblacional), divide por $N$. Ver [[parámetro vs estadístico]].

Cuando se trabaja con **toda** la población no hace falta corregir nada: no se está estimando la media a partir de datos parciales, se la conoce exactamente.

> [!note] En código
> Es el `ddof=1` que ya viste en [[coeficiente de variación]] y en [[medidas de dispersión]]: `np.std(x, ddof=1)` / `np.var(x, ddof=1)` en NumPy (ver [[04 - Agregaciones y estadistica descriptiva]]) dividen por $n-1$; sin `ddof=1`, NumPy divide por $n$ por defecto.

> [!info] A futuro: el mismo concepto en los tests de hipótesis
> Cuando la materia llegue a inferencia, los grados de libertad van a reaparecer como parámetro de la **distribución t** que usan los tests de una y dos muestras (`scipy.stats.ttest_ind`, ver [[06 - Tests de hipotesis - una y dos muestras]] de SciPy) y en la tabla `.summary()` de un modelo de `statsmodels` (`Df Residuals`, ver [[04 - Diagnostico de modelos]]).

## Relacionado
- [[02 - El estudio de la variabilidad]]
- [[parámetro vs estadístico]]
- [[medidas de dispersión]]
- [[04 - Agregaciones y estadistica descriptiva]]
- [[06 - Tests de hipotesis - una y dos muestras]]
