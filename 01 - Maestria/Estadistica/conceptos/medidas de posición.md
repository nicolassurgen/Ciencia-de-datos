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

> [!example] Por qué importa la robustez: ingreso típico por barrio
> Comparar el ingreso familiar típico de dos barrios usando la **media** puede dar un resultado completamente distorsionado si en uno de ellos vive una persona con un patrimonio extremo (el ejemplo clásico: comparar dos barrios de Seattle, donde uno de ellos incluye la casa de Bill Gates). La media de ese barrio se dispara y dice muy poco sobre el ingreso de un hogar "típico" ahí. La **mediana**, en cambio, da prácticamente el mismo resultado con o sin ese caso extremo — por eso es la medida preferida cuando se sospecha la presencia de valores atípicos o de una fuerte asimetría. *Fuente: [[Practical Statistics for Data Scientists]] (Bruce & Bruce), cap. 1.*

> [!definition] Promedio truncado (trimmed mean)
> Se elimina un porcentaje de datos en **cada extremo** de la distribución y se promedian los restantes (p. ej. `trim = 0.1` descarta el 10 % de cada lado). Compromiso entre aprovechar casi todos los datos y ganar robustez.

> [!definition] Moda
> El valor o categoría **más frecuente**. Es la única medida de centro que sirve también para variables cualitativas nominales.
>
> Para una variable **cuantitativa continua sin agrupar**, calcular la moda directamente casi nunca tiene sentido: al no repetirse casi ningún valor exactamente, "el más frecuente" suele ser un artefacto de la precisión de medición, no un centro real de la distribución. En ese caso conviene primero agrupar en intervalos (ver [[distribución de frecuencias]]) y hablar de la **clase modal**, o directamente describir la forma con un [[histograma]].

> [!definition] Media geométrica
> $$\bar{y}_G = \sqrt[n]{\prod_{i=1}^{n} y_i} = \left(y_1 \cdot y_2 \cdots y_n\right)^{1/n}$$
> Solo se define para valores **positivos**. Es menos sensible a valores atípicos que la media aritmética, aunque su interpretación es menos intuitiva ("¿qué significa multiplicar diámetros entre sí?"). Se usa para promediar **índices o tasas de crecimiento relativas** (p. ej. índices de capacidad de un proceso, tasas de crecimiento período a período), donde lo que importa es el efecto multiplicativo acumulado y no la suma. *Fuente: [[Estadística para la resolución de problemas en Ingeniería]], cap. 2.*

> [!info] Material complementario (no visto en clase) — Media y mediana ponderadas
> $$\bar{y}_w = \frac{\sum_i w_i y_i}{\sum_i w_i}$$
> Igual que la media, pero cada dato **pesa distinto** según su importancia relativa (`w_i`) en vez de pesar todos por igual. Útil cuando algunos grupos están sobre o subrepresentados en la muestra respecto de la población, o cuando algunos datos son intrínsecamente más variables (y conviene darles menos peso). La **mediana ponderada** aplica la misma idea: se ordenan los datos y se busca el punto donde la suma de pesos se reparte mitad y mitad, en vez de contar observaciones. Ambas siguen siendo **robustas** si la mediana lo es.
>
> *Ejemplo:* para calcular la tasa de homicidios **promedio de un país** a partir de la tasa de cada estado, promediar directamente las tasas estatales trata a un estado chico igual que a uno grande — hay que ponderar cada tasa por la población del estado. Sobre datos de EE.UU., la media ponderada por población da 4.45 (homicidios cada 100.000 habitantes), cercana a la mediana ponderada de 4.4 — ambas más representativas del país en su conjunto que el promedio simple de las tasas estatales. *Fuente: [[Practical Statistics for Data Scientists]] (Bruce & Bruce), cap. 1.*

## Qué medida usar según la escala

- **Nominal** → solo **moda**.
- **Ordinal** → moda y **mediana / percentiles**.
- **Cuantitativa (intervalo/razón)** → todas (media, mediana, truncado, moda).

Ver [[escalas de medición]] para el detalle de las escalas.

## Percentiles y cuartiles

Con la misma lógica de la mediana se definen otros cortes de la distribución ordenada:

- **Cuartiles** → dividen en 4 partes: $q_1$ (25 %), $q_2$ = mediana (50 %), $q_3$ (75 %).
- **Percentiles** → dividen en 100 partes: $P_{35}$ acumula el 35 % de los datos.
- **Quintiles y deciles** → dividen en 5 y 10 partes respectivamente. Aparecen seguido al describir distribuciones de ingreso ("el quintil más rico", "el decil más pobre"), donde reportar directamente la media tendría poco sentido por la fuerte asimetría típica de esos datos.

**Cálculo (algoritmo):** para el percentil de orden $\alpha$ (ej. $\alpha=0{,}25$ para $q_1$), sobre $n$ datos ordenados: se calcula $E = \alpha \cdot n$. Si $E$ tiene parte decimal no nula, el percentil es el dato en la posición $E$ redondeada hacia arriba, $y_{[E+1]}$. Si $E$ es un entero exacto, el percentil se calcula promediando $y_{[E]}$ y $y_{[E+1]}$. *Fuente: [[Estadística para la resolución de problemas en Ingeniería]], cap. 2.*

> [!warning] No siempre hay un valor exacto
> Especialmente en variables discretas, puede no existir un dato que acumule *exactamente* ese porcentaje. Existen distintos métodos de interpolación (el de arriba es uno de varios posibles), y por eso software distinto puede dar valores levemente distintos.

> [!tip] Percentil vs. rango percentil — dos preguntas inversas
> Es fácil confundir dos preguntas relacionadas pero opuestas: **"¿qué valor corresponde al percentil 90?"** (dado un rango, encontrar el valor — la función `Percentile`) es la inversa de **"¿en qué percentil queda este valor de 39 semanas?"** (dado un valor, encontrar su rango — la función `PercentileRank`, esencialmente la CDF evaluada en ese punto). La primera pregunta parte de una proporción y busca un dato; la segunda parte de un dato y busca una proporción. *Fuente: [[Think Stats – Exploratory Data Analysis in Python]], cap. 4.*

## Qué le pasa a la media ante una transformación lineal

Si a cada dato se le aplica una transformación lineal $x_i = a + b\,y_i$ (por ejemplo, pasar de °C a °F, o restar una referencia y reescalar), la media se transforma **de la misma forma** que los datos: $\bar{x} = a + b\,\bar{y}$. Lo mismo vale para la mediana y la moda. Esta propiedad es la base de la **estandarización** (z-score): ver [[valores atípicos]] para su aplicación concreta a la detección de atípicos, y [[medidas de dispersión]] para qué le pasa a la dispersión bajo la misma transformación.

## Robustez: tabla resumen

| Medida | ¿Robusta? |
|---|:---:|
| Media | ❌ |
| Mediana | ✅ |
| Promedio truncado | ✅ (parcial) |
| Media geométrica | ✅ (parcial) |

> [!tip] Combiná centro + dispersión coherentes
> Si describís con la **media**, acompañala con el **desvío estándar**. Si usás la **mediana**, acompañala con el **RIQ**. Ver [[medidas de dispersión]].

> [!tip] "Estimar" vs. "medir" — un matiz de vocabulario entre disciplinas
> Un estadístico suele decir que **estima** una medida de centro (el foco está en la incertidumbre de esa estimación respecto del verdadero valor poblacional); un data scientist suele decir que la **mide** (el foco está en un objetivo de negocio concreto, no en la incertidumbre). Son la misma cuenta, con énfasis distinto según el contexto — ver también [[parámetro vs estadístico]]. *Fuente: [[Practical Statistics for Data Scientists]] (Bruce & Bruce), cap. 1.*

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
