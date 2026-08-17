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

Hay dos razonamientos distintos que se relacionan pero **no son el mismo argumento**: uno cuenta cuántos desvíos son "libres" (grados de libertad, en sentido literal); el otro muestra que dividir por $n$ produce una subestimación sistemática (corrección de sesgo). Vale la pena separarlos.

### Argumento 1 — Conteo: cuántos desvíos son "libres"

Una vez que se fija $\bar{y}$, solo $n-1$ de los $n$ desvíos $(y_i - \bar{y})$ pueden tomar cualquier valor: el último queda automáticamente determinado por los demás, porque la suma de todos los desvíos respecto de la media es siempre cero ($\sum_{i=1}^n (y_i - \bar y) = 0$, por construcción de la media). Elegidos los primeros $n-1$ desvíos libremente, el último es forzado. Por eso hay $n-1$ grados de libertad, no $n$ — este es el argumento que le da nombre al concepto, y es puramente combinatorio: no dice todavía nada sobre si el resultado final está sesgado o no.

### Argumento 2 — Por qué usar $\bar{y}$ en vez de $\mu$ produce una subestimación

Este segundo argumento sí explica el sesgo, y parte de una propiedad de la media que conviene dejar explícita: $\bar{y}$ es, de todas las constantes posibles $c$, la que **minimiza** la suma de cuadrados de los desvíos:

$$\bar{y} = \arg\min_{c} \sum_{i=1}^{n} (y_i - c)^2$$

(Es un problema de minimización sin restricciones —un $\arg\min$— en el mismo sentido formal que [[03 - Optimizacion]] de Matemática; derivando la suma respecto de $c$ e igualando a cero (ver [[02 - Derivadas]]) se llega directo a que el minimizador es $c=\bar y$. Es la misma idea de mínimos cuadrados que aparece en regresión lineal — ver [[02 - Matrices]]. Es también, no por casualidad, la misma propiedad que explica por qué la mediana es robusta y la media no: la mediana minimiza la suma de **errores absolutos** en vez de al cuadrado — ver [[robustez estadística]] para el desarrollo completo de ese paralelismo.) Una consecuencia directa es que, para **cualquier** otra constante — en particular, la verdadera media poblacional $\mu$, que en general no coincide exactamente con $\bar{y}$ —, la suma de cuadrados no puede ser menor que la calculada con $\bar{y}$:

$$\sum_{i=1}^{n} (y_i - \bar{y})^2 \; \le \; \sum_{i=1}^{n} (y_i - \mu)^2$$

Es decir: **usar $\bar{y}$ en lugar de $\mu$ para calcular los desvíos hace que la suma de cuadrados salga artificialmente más chica** de lo que saldría si se conociera la media poblacional real. Como la varianza muestral usa $\bar{y}$ (porque $\mu$ es, en la práctica, desconocido), esa suma de cuadrados ya arranca "encogida" — y dividirla por $n$, como si no hubiera pasado nada, subestima la varianza poblacional en promedio.

Formalmente, se puede probar que:

$$E\left[\sum_{i=1}^{n}(y_i - \bar{y})^2\right] = (n-1)\,\sigma^2$$

(usando que $E[\bar y] = \mu$ y $\text{Var}(\bar y) = \sigma^2/n$, resultados de [[población y muestra]]). Dividir por $n$ daría entonces $E[s_n^2] = \frac{n-1}{n}\sigma^2$, un valor sistemáticamente **menor** que $\sigma^2$: un **estimador sesgado**. Dividir por $n-1$ en cambio da $E[s^2] = \sigma^2$ exactamente — un **estimador insesgado** de la varianza poblacional. Esa es la corrección real; el conteo de grados de libertad del Argumento 1 explica **de dónde sale** el número $n-1$, pero no por sí solo demuestra que dividir por él corrige el sesgo.

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
- [[robustez estadística]]
- [[04 - Agregaciones y estadistica descriptiva]]
- [[06 - Tests de hipotesis - una y dos muestras]]
