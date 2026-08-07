---
titulo: "Seaborn - Distribuciones: histplot, kdeplot, ecdfplot"
materia: Seaborn
tipo: apunte
tags:
  - seaborn
  - tecnologias
  - python
  - tema/distribuciones
fuente: "seaborn.pydata.org (documentación oficial)"
---

# Distribuciones: histplot, kdeplot, ecdfplot

Esta nota es, directamente, el capítulo de [[histograma|Estadística sobre distribuciones]] hecho código — con la diferencia de que acá tenés **tres** formas distintas de visualizar lo mismo, y elegir entre ellas es parte del análisis.

> [!important] La pregunta estadística detrás de este gráfico
> "¿Cómo se reparten los valores de una variable?" — la misma pregunta que resolvías con una [[distribución de frecuencias|tabla de frecuencias]] o un [[histograma]] a mano en Estadística.

## `histplot()`: la tabla de frecuencias, dibujada

```python
sns.displot(data=penguins, x="flipper_length_mm", bins=20)
```
**Qué genera:** 20 barras azules pegadas mostrando la distribución del largo de aleta — la forma es **bimodal** (dos "jorobas"): un grupo de pingüinos con aletas más cortas (~190mm) y otro con aletas más largas (~215mm), reflejando que hay más de una especie mezclada en los datos (ver [[estratificación]]).

Es, literalmente, el [[histograma]] que ya conocés: agrupa los datos en intervalos de clase ([[distribución de frecuencias]]) y dibuja una barra por cada uno.

| Parámetro | Qué controla |
|---|---|
| `bins` / `binwidth` | Cantidad de intervalos, o el ancho de cada uno |
| `hue` | Un histograma separado (o superpuesto) por categoría |
| `stat` | Normalizar: `"count"` (default), `"density"`, `"probability"` |
| `multiple` | Cómo combinar grupos: `"layer"`, `"stack"`, `"dodge"` |
| `discrete` | Centra las barras sobre valores enteros (para variables discretas, ver [[variables]]) |

## `kdeplot()`: la versión "suavizada"

```python
sns.displot(data=penguins, x="flipper_length_mm", kind="kde", bw_adjust=.25)
```
**Qué genera:** la versión curva y suave del histograma de arriba — sin barras, una línea continua con dos picos bien marcados (por el `bw_adjust=.25`, que muestra más detalle) en las mismas dos zonas donde el histograma tenía sus dos grupos.

> [!definition] KDE (*Kernel Density Estimation*)
> En vez de agrupar en intervalos rígidos como el histograma, estima una **curva continua** de densidad de probabilidad a partir de los datos. `bw_adjust` controla el suavizado: valores chicos (`0.25`) muestran más detalle (y más ruido); valores grandes (`2`) simplifican la forma.

> [!warning] El KDE puede "mentir" con datos discretos
> La documentación oficial lo advierte directamente: el KDE **falla** con datos discretos, o cuando ciertos valores están sobrerrepresentados — dibuja una curva suave donde en realidad hay "escalones". Si tu variable es discreta (conteos, categorías numéricas), un histograma con `discrete=True` es más honesto que un KDE.

## `ecdfplot()`: sin decisiones de por medio

```python
sns.displot(data=penguins, x="flipper_length_mm", kind="ecdf")
```
**Qué genera:** una curva escalonada creciente que va de 0 a 1 — se lee directamente "qué proporción de pingüinos tiene una aleta más corta que X mm" para cualquier punto del eje X, sin las barras ni la curva suavizada de los dos gráficos anteriores.

> [!definition] ECDF (función de distribución acumulada empírica)
> Para cada valor de X, muestra qué **proporción** de los datos es menor o igual a ese valor — el eje Y va de 0 a 1. Es exactamente la $H_i$ (frecuencia relativa acumulada) que ya calculaste a mano en [[distribución de frecuencias]] de Estadística.

> [!tip] La ventaja de la ECDF: no hay nada que ajustar
> A diferencia del histograma (`bins`) y el KDE (`bw_adjust`), la ECDF **no tiene ningún parámetro de suavizado** — representa los datos exactamente como son, sin ninguna decisión subjetiva del analista de por medio. Es la opción más "honesta" cuando no querés que la elección de un parámetro cambie la interpretación.

## Cuál elegir

| Si necesitás... | Usá |
|---|---|
| La forma clásica, fácil de explicar a cualquiera | `histplot` |
| Comparar la forma general entre varios grupos sin el ruido de los bins | `kdeplot` |
| Leer percentiles exactos, o evitar cualquier decisión de suavizado | `ecdfplot` |
| Ver relación entre 2 variables continuas a la vez (bivariado) | `displot(x=..., y=..., kind="kde")` |

## `displot()`: la interfaz unificada

Las tres son, en el fondo, la misma función de figura con distinto `kind=` (ver [[02 - Funciones de figura vs funciones de ejes]]):

```python
sns.displot(data=penguins, x="bill_length_mm", y="bill_depth_mm", kind="kde")   # bivariado
```

Con `x` **y** `y` especificados, obtenés un mapa de densidad 2D — el equivalente visual de preguntarte si dos variables numéricas tienden a moverse juntas, antes incluso de calcular una correlación o ajustar una [[07 - Regresion y relaciones estadisticas|regresión]].

## Relacionado
- [[histograma]]
- [[distribución de frecuencias]]
- [[valores atípicos]]
- [[06 - Variables categoricas (boxplot, violinplot, barplot)]]
