---
titulo: "statsmodels - Regresión lineal (OLS y WLS)"
materia: statsmodels
tipo: apunte
tags:
  - statsmodels
  - tecnologias
  - python
  - tema/regresion
fuente: "statsmodels documentation — gettingstarted (statsmodels.org/stable)"
---

# Regresión lineal (OLS y WLS)

> [!info] Contenido a futuro
> La regresión formal todavía no se dio en Estadística — [[07 - Regresion y relaciones estadisticas|Seaborn ya dibuja]] la recta de `sns.lmplot()`, pero sin el modelo estadístico completo detrás. Esta nota es ese modelo.

## OLS: mínimos cuadrados ordinarios

```python
import statsmodels.formula.api as smf

modelo = smf.ols('masa_g ~ largo_pico_mm', data=pinguinos).fit()
print(modelo.summary())
```

```
                            OLS Regression Results
==============================================================================
Dep. Variable:                 masa_g   R-squared:                       0.418
Method:                 Least Squares   F-statistic:                     37.9
==============================================================================
                     coef    std err          t      P>|t|      [0.025    0.975]
------------------------------------------------------------------------------
Intercept        -3038.5      957.3     -3.174      0.003    -4980.1   -1096.9
largo_pico_mm       181.9       29.6      6.148      0.000      121.9     241.9
==============================================================================
```

`OLS` (*Ordinary Least Squares*) ajusta la recta que minimiza la suma de los residuos al cuadrado — no probando pendientes al azar, sino resolviendo la fórmula cerrada $\hat\beta=(X^TX)^{-1}X^Ty$ (con $X$ la matriz de diseño: una fila por observación, una columna por predictora), desarrollada en [[02 - Matrices]] y [[03 - Optimizacion]] de Matemática. Leyendo la tabla: por cada mm extra de largo de pico, el modelo estima **+181.9 g** de masa (`coef`), y ese efecto es significativo (`P>|t| = 0.000`, muy por debajo de 0.05). El `R-squared = 0.418` dice que el largo del pico explica el 42% de la variabilidad de la masa — el resto es ruido u otras variables no incluidas.

## Por qué esto resuelve lo que Seaborn no resuelve

> [!important] Controlar una variable de confusión con regresión múltiple
> [[variable de confusión|La nota de Estadística sobre variables de confusión]] señala que `sns.lmplot()` **no protege** de que una relación aparente se deba a un tercer factor. Agregar ese factor **como predictora adicional** al modelo es, precisamente, la forma de **controlarlo**:
> ```python
> modelo2 = smf.ols('masa_g ~ largo_pico_mm + especie', data=pinguinos).fit()
> ```
> Ahora el coeficiente de `largo_pico_mm` queda estimado *ya teniendo en cuenta* la especie, en vez de mezclar ambos efectos — probablemente va a cambiar respecto del +181.9 g de arriba, porque parte de lo que antes le "cargaba" a `largo_pico_mm` en realidad era diferencia entre especies.

## Leer los resultados sin imprimir toda la tabla

```python
modelo.params
# Intercept       -3038.5
# largo_pico_mm     181.9

modelo.pvalues
# Intercept        0.003
# largo_pico_mm    0.000    -> significativo: p < 0.05

modelo.rsquared
# 0.418
```

> [!note] $R^2$ y la variabilidad de Estadística
> El $R^2$ responde "¿qué proporción de la [[medidas de dispersión|variabilidad]] de la variable respuesta explica el modelo?" — acá, $R^2 = 0{,}418$: el 42 % de la variabilidad de `masa_g` queda explicada por `largo_pico_mm`, y el 58 % restante es variabilidad no explicada (ruido, u otras variables no incluidas, como la especie).

## WLS: cuando la varianza no es constante

```python
# si se sospecha que la dispersión de masa_g crece con el largo del pico,
# se le da menos peso a esas observaciones más "ruidosas":
pesos = 1 / (pinguinos["largo_pico_mm"] ** 2)
modelo_wls = smf.wls('masa_g ~ largo_pico_mm', data=pinguinos, weights=pesos).fit()
```

`OLS` asume que la dispersión de los residuos es **constante** en todo el rango de las predictoras (homocedasticidad, ver [[04 - Diagnostico de modelos]]). Cuando no lo es, `WLS` (*Weighted Least Squares*) le da menos peso a las observaciones con más varianza esperada.

## Relacionado
- [[01 - Introduccion a statsmodels]]
- [[variable de confusión]]
- [[medidas de dispersión]]
- [[07 - Regresion y relaciones estadisticas]]
- [[04 - Diagnostico de modelos]]
