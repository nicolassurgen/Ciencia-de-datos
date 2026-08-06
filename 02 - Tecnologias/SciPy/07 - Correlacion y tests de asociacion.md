---
titulo: "SciPy.stats - Correlación y tests de asociación"
materia: SciPy
tipo: apunte
tags:
  - scipy
  - tecnologias
  - python
  - tema/inferencia
fuente: "SciPy Reference Guide — scipy.stats (docs.scipy.org/doc/scipy/reference/stats.html)"
---

# Correlación y tests de asociación

> [!info] Contenido a futuro
> La correlación como tema formal todavía no se dio en Estadística. Esta nota queda como referencia para cuando el curso llegue a relaciones entre variables.

## Elegir el test según la escala de medición

`scipy.stats` ofrece varias medidas de asociación entre dos variables, y **cuál corresponde depende directamente de la [[escalas de medición|escala de medición]]** de esas variables — la misma tabla nominal/ordinal/intervalo/razón de la clase 1, aplicada ahora a elegir un test en vez de una medida de resumen.

| Escala de las variables | Función | Qué mide |
|---|---|---|
| Razón / Intervalo, relación lineal | `stats.pearsonr(x, y)` | Correlación de Pearson |
| Ordinal (o no-lineal monótona) | `stats.spearmanr(x, y)` | Correlación de Spearman (por rangos) |
| Ordinal, muestras chicas | `stats.kendalltau(x, y)` | Tau de Kendall |
| Nominal (tabla de contingencia) | `stats.chi2_contingency(tabla)` | Test chi-cuadrado de independencia |

```python
from scipy import stats

r, p_valor = stats.pearsonr(diametro, peso)   # r entre -1 y 1, p_valor de la hipótesis r=0
```

## Correlación no es causalidad — y acá aparece explícito

> [!warning] El mismo problema de siempre: variable de confusión
> Un `r` alto entre dos variables **no prueba** que una cause la otra: podría haber una [[variable de confusión]] detrás explicando ambas a la vez. `sns.lmplot()` de Seaborn dibuja la recta, pero (como ya señala esa nota) **no protege** de esto — el número de `pearsonr` tampoco. Separar por grupo (`hue=` en Seaborn) o controlar la variable sospechosa en un modelo (ver [[02 - Regresion lineal (OLS y WLS)]] de statsmodels) son las formas de acercarse a una respuesta más limpia.

## Tabla de contingencia: dos variables nominales

```python
tabla = pd.crosstab(df["motivo_queja"], df["region"])
chi2, p_valor, gl, esperado = stats.chi2_contingency(tabla)
```

Responde si dos variables **cualitativas** están asociadas (p. ej., ¿el motivo de queja depende de la región?) — el equivalente categórico de `pearsonr`. El `gl` que devuelve son, otra vez, [[grados de libertad]].

## Regresión lineal simple, la versión rápida

```python
resultado = stats.linregress(x, y)
resultado.slope, resultado.intercept, resultado.rvalue   # pendiente, ordenada, r
```

Ajusta una recta $y = mx + b$ por mínimos cuadrados y de paso da el coeficiente de correlación. Es la versión mínima de lo que [[02 - Regresion lineal (OLS y WLS)|statsmodels hace en profundidad]], con diagnósticos y soporte para más de una variable predictora.

## Relacionado
- [[01 - Introduccion a SciPy.stats]]
- [[escalas de medición]]
- [[variable de confusión]]
- [[02 - Regresion lineal (OLS y WLS)]]
