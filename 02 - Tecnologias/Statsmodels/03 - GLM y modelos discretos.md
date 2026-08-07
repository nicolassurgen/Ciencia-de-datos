---
titulo: "statsmodels - GLM y modelos discretos"
materia: statsmodels
tipo: apunte
tags:
  - statsmodels
  - tecnologias
  - python
  - tema/regresion
fuente: "statsmodels documentation — API reference (statsmodels.org/stable/api.html)"
---

# GLM y modelos discretos

> [!info] Contenido a futuro
> Requiere haber visto [[02 - Regresion lineal (OLS y WLS)]] primero. Todavía no se dio en Estadística.

## El problema que resuelven

`OLS` asume que la variable de respuesta es continua y sus residuos aproximadamente normales. Eso deja de ser razonable cuando la respuesta es **binaria** (sí/no), un **conteo** (cantidad de eventos) u otra variable con una escala distinta.

## GLM: modelos lineales generalizados

```python
import statsmodels.api as sm
import statsmodels.formula.api as smf

modelo = smf.glm('exito ~ dosis', data=df, family=sm.families.Binomial()).fit()
```

`GLM` generaliza `OLS` permitiendo elegir una **familia** de distribución (`Binomial`, `Poisson`, `Gamma`, …) y una **función de enlace** que conecta el predictor lineal con la escala de la respuesta. Es el marco general del que `Logit` y `Poisson` (abajo) son casos particulares con nombre propio.

## Logit: respuesta binaria

```python
modelo = smf.logit('aprobado ~ horas_estudio', data=df).fit()

modelo.params
# Intercept         -4.08
# horas_estudio      0.85    -> cada hora extra de estudio aumenta el "log-odds" de aprobar

modelo.predict(pd.DataFrame({'horas_estudio': [5]}))
# 0  0.61   -> con 5 horas de estudio, el modelo estima 61% de probabilidad de aprobar
```

Modela la **probabilidad** de un resultado binario (aprobado/no aprobado, defectuoso/no defectuoso) en función de una o más predictoras. Conecta directo con las variables **binarias** vistas en [[tipos primitivos en Python]] de Algoritmos (`bool`) y con la escala **nominal** de [[escalas de medición]].

## Poisson y modelos de conteo

```python
modelo = smf.poisson('cant_imperfecciones ~ turno', data=df).fit()

modelo.params
# Intercept        0.34
# turno[T.noche]   0.62   -> en el turno noche se espera exp(0.62) ≈ 1.86 veces más imperfecciones
```

Para variables de respuesta que son **conteos** (cuántas veces ocurre algo) — el caso de las "imperfecciones por pieza" de la [[02 - El estudio de la variabilidad|clase 2 de Estadística]], que es una variable **cuantitativa discreta** que surge de contar. `NegativeBinomial` es la alternativa cuando el conteo tiene más variabilidad de la que Poisson permite (sobredispersión).

## Relacionado
- [[01 - Introduccion a statsmodels]]
- [[02 - Regresion lineal (OLS y WLS)]]
- [[escalas de medición]]
- [[tipos primitivos en Python]]
