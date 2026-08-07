---
titulo: "statsmodels - Diagnóstico de modelos"
materia: statsmodels
tipo: apunte
tags:
  - statsmodels
  - tecnologias
  - python
  - tema/regresion
fuente: "statsmodels documentation — gettingstarted (statsmodels.org/stable)"
---

# Diagnóstico de modelos

> [!info] Contenido a futuro
> Continúa [[02 - Regresion lineal (OLS y WLS)]]. Todavía no se dio en Estadística.

## Un modelo no se evalúa solo por el $R^2$

Un `R^2` alto no garantiza que el modelo sea confiable: puede haber problemas en los **residuos** (la diferencia entre el valor observado y el predicho) que invaliden las conclusiones. Diagnosticar un modelo es, en esencia, aplicar [[medidas de posición|estadística descriptiva]] y [[medidas de dispersión|de dispersión]] a esos residuos.

## Mirar los residuos

```python
modelo.resid.describe()
# mean      -0.00   -> los residuos se centran en 0, como se espera
# std      612.30
# min    -1420.10
# max     1680.40
```

> [!important] Los residuos deberían "no decir nada"
> Si el modelo captura bien la relación, lo que sobra (los residuos) debería ser puro ruido: sin patrón, centrado en 0, con dispersión constante. Un residuo con estructura (una tendencia, una forma de embudo) es evidencia de que al modelo le falta algo.

## Homocedasticidad: ¿la dispersión de los residuos es constante?

```python
from statsmodels.stats.diagnostic import het_breuschpagan

lm_stat, lm_pvalue, f_stat, f_pvalue = het_breuschpagan(modelo.resid, modelo.model.exog)
lm_pvalue   # 0.03 -> p < 0.05: hay evidencia de heterocedasticidad, convendría WLS
```

Comprueba si la [[medidas de dispersión|dispersión]] de los residuos es la misma en todo el rango de las predictoras (homocedasticidad) o si varía (heterocedasticidad) — en cuyo caso conviene `WLS` en vez de `OLS` (ver [[02 - Regresion lineal (OLS y WLS)]]).

## Autocorrelación: Durbin-Watson

```python
from statsmodels.stats.stattools import durbin_watson

durbin_watson(modelo.resid)   # 1.98 -> muy cerca de 2, sin evidencia de autocorrelación
```

Chequea si un residuo está correlacionado con el siguiente — algo esperable si los datos tienen estructura temporal no capturada (ver [[05 - Series de tiempo]]) y que invalida los supuestos de independencia de `OLS`.

> [!note] `Df Residuals` en el summary
> La tabla de `.summary()` incluye `Df Model` y `Df Residuals`: los mismos [[grados de libertad]] vistos en el cálculo de la varianza muestral, acá repartidos entre "cuántos coeficientes estimó el modelo" y "cuántos quedan libres para estimar la variabilidad residual".

## Multicolinealidad: VIF

```python
from statsmodels.stats.outliers_influence import variance_inflation_factor

X = pinguinos[["largo_pico_mm", "ancho_pico_mm"]]
for i, columna in enumerate(X.columns):
    print(columna, variance_inflation_factor(X.values, i))
# largo_pico_mm   1.2
# ancho_pico_mm   1.2   -> ambos bajos (<10): no hay problema de multicolinealidad
```

Si dos predictoras están muy correlacionadas entre sí, sus coeficientes individuales se vuelven inestables y difíciles de interpretar. Un VIF alto (regla de dedo: > 10) señala ese problema.

## Regresión robusta: cuando hay atípicos

```python
modelo_robusto = smf.rlm('masa_g ~ largo_pico_mm', data=df).fit()
```

`RLM` (*Robust Linear Model*) es a `OLS` lo que la mediana es a la media (ver [[robustez estadística]]): un ajuste que no se deja arrastrar tanto por observaciones extremas.

## Relacionado
- [[01 - Introduccion a statsmodels]]
- [[02 - Regresion lineal (OLS y WLS)]]
- [[grados de libertad]]
- [[robustez estadística]]
