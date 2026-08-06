---
titulo: "SciPy.stats - Tests de hipótesis (una y dos muestras)"
materia: SciPy
tipo: apunte
tags:
  - scipy
  - tecnologias
  - python
  - tema/inferencia
fuente: "SciPy Reference Guide — scipy.stats (docs.scipy.org/doc/scipy/reference/stats.html)"
---

# Tests de hipótesis: una y dos muestras

> [!info] Contenido a futuro
> La materia Estadística todavía no dio inferencia formal (intervalos de confianza, pruebas de hipótesis) — esta nota queda como referencia para cuando el curso llegue a ese tema. La [[diseño de experimentos|nota de diseño de experimentos]] ya lo anticipa: *"decidir si la diferencia observada entre tratamientos es real o puede deberse al azar [...] eso es exactamente lo que hacen las pruebas de hipótesis"*.

## La lógica común a todos los tests

Un test de hipótesis de `scipy.stats` siempre devuelve dos números: un **estadístico de prueba** (qué tan extremo es lo observado, en las unidades propias del test) y un **p-valor** (la probabilidad de ver un resultado así de extremo si en realidad no hay efecto). Por convención, `p < 0.05` suele tomarse como evidencia suficiente para rechazar la hipótesis de "no hay diferencia".

## Comparar una muestra contra un valor de referencia

```python
from scipy import stats

stats.ttest_1samp(muestra, popmean=100)   # ¿la media de la muestra difiere de 100?
```

## Comparar dos muestras independientes

```python
maquina_1 = [39.1, 39.5, 40.3, 36.7, 39.3]
maquina_2 = [41.2, 40.8, 42.1, 39.9, 40.5]

stats.ttest_ind(maquina_1, maquina_2)          # t-test: ¿difieren las medias?
stats.mannwhitneyu(maquina_1, maquina_2)        # alternativa no paramétrica (sin asumir normalidad)
stats.levene(maquina_1, maquina_2)              # ¿tienen varianzas iguales? (supuesto del t-test)
```

Es el caso exacto de los *dotplots* de diámetro de las Máquinas 1 y 2 de la [[02 - El estudio de la variabilidad|clase 2]]: ahí se comparaban **visualmente** centro y dispersión; `ttest_ind` da una respuesta **numérica** a si esa diferencia visual es estadísticamente significativa.

## Comparar tres o más grupos: ANOVA

```python
stats.f_oneway(maquina_1, maquina_2, maquina_3)   # ANOVA de una vía
stats.kruskal(maquina_1, maquina_2, maquina_3)     # alternativa no paramétrica
```

Generaliza `ttest_ind` a más de dos grupos — la herramienta que la nota de [[diseño de experimentos]] menciona explícitamente para cuando hay 3 o más tratamientos.

## Verificar el supuesto de normalidad

```python
stats.shapiro(muestra)      # test de Shapiro-Wilk
stats.normaltest(muestra)   # test de D'Agostino-Pearson
```

Muchos tests (el t-test entre ellos) asumen que los datos siguen aproximadamente una [[02 - Distribuciones de probabilidad|distribución normal]]. Estos tests lo verifican formalmente, en vez de solo mirar la forma de un [[histograma]] a ojo.

> [!note] El parámetro `df` reaparece acá
> Los resultados de `ttest_1samp`/`ttest_ind` incluyen `df` (grados de libertad) en su salida detallada — el mismo concepto de [[grados de libertad]] visto en el cálculo de la varianza muestral, reutilizado acá para definir la forma exacta de la distribución t contra la que se compara el estadístico.

## Relacionado
- [[01 - Introduccion a SciPy.stats]]
- [[diseño de experimentos]]
- [[grados de libertad]]
- [[parámetro vs estadístico]]
