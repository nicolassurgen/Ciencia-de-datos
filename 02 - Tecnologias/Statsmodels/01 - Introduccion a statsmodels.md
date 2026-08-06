---
titulo: "statsmodels - Introducción"
materia: statsmodels
tipo: apunte
tags:
  - statsmodels
  - tecnologias
  - python
  - tema/introduccion
fuente: "statsmodels documentation (statsmodels.org/stable)"
---

# Introducción a statsmodels

> [!definition] statsmodels
> Librería de Python para **estimar modelos estadísticos**, correr **tests de hipótesis** y hacer **exploración de datos**, con énfasis en dar salidas detalladas al estilo de R o Stata: no solo un número, sino un resumen completo del modelo con sus diagnósticos.

> [!info] Contenido a futuro
> La materia Estadística todavía no llegó a modelos (regresión, ANOVA, series de tiempo) — casi todo lo que cubre statsmodels es, en este momento del curso, material de referencia para más adelante. Se documenta igual, con la misma profundidad que el resto de las tecnologías del vault, porque cuando la materia llegue a inferencia esta va a ser la herramienta.

## scipy.stats vs. statsmodels: ¿cuál uso?

| | `scipy.stats` | `statsmodels` |
|---|---|---|
| Unidad de trabajo | Una función, un test puntual | Un **modelo** completo, con métodos propios |
| Salida | Un estadístico y un p-valor | Un objeto de resultados con `.summary()`, `.params`, `.resid`, diagnósticos |
| Ejemplos | `ttest_ind`, `pearsonr` | `OLS`, `GLM`, `ARIMA` |
| Uso típico | "¿Esta diferencia es significativa?" | "¿Cuál es la relación entre estas variables, y qué tan bien la explica el modelo?" |

En la práctica se complementan: [[07 - Correlacion y tests de asociacion|`scipy.stats.pearsonr`]] da la correlación entre dos variables; `statsmodels.OLS` construye el modelo de regresión completo (con más de una variable predictora, diagnósticos de residuos, intervalos de confianza para cada coeficiente).

## Las dos formas de especificar un modelo

```python
import statsmodels.api as sm
import statsmodels.formula.api as smf
```

**API de fórmulas** (`smf`, estilo R, trabaja directo con un DataFrame de Pandas — ver [[01 - Introduccion a Series y DataFrame]]):

```python
modelo = smf.ols('masa_g ~ largo_pico_mm + especie', data=df).fit()
```

**API de arrays** (`sm`, más explícita, separa variable respuesta y predictoras):

```python
modelo = sm.OLS(y, X).fit()
```

> [!tip] Cuál usar
> La API de fórmulas (`smf`) es más legible y la más usada en la práctica cuando los datos ya están en un DataFrame — el `~` se lee "en función de". La API de arrays (`sm`) da más control y es la que se ve en optimización avanzada o cuando los datos no vienen de un DataFrame.

## Recorrido de estas notas

1. **Introducción** *(esta nota)*
2. [[02 - Regresion lineal (OLS y WLS)]] — el modelo más usado, la puerta de entrada a todo lo demás.
3. [[03 - GLM y modelos discretos]] — cuando la variable de respuesta no es continua.
4. [[04 - Diagnostico de modelos]] — ¿el modelo es confiable? Supuestos y residuos.
5. [[05 - Series de tiempo]] — el puente directo con [[series de tiempo]] de Estadística.
6. [[06 - Modelos multivariados y otros]] — PCA, modelos jerárquicos, regresión robusta.

## Relacionado
- [[01 - Introduccion a SciPy.stats]]
- [[01 - Introduccion a Series y DataFrame]]
