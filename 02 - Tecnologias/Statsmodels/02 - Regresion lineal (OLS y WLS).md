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

modelo = smf.ols('masa_g ~ largo_pico_mm + especie', data=pinguinos).fit()
print(modelo.summary())
```

`OLS` (*Ordinary Least Squares*) ajusta una recta (o un hiperplano, con más de una variable predictora) que minimiza la suma de los residuos al cuadrado. `.summary()` imprime una tabla con los coeficientes estimados, su error estándar, el estadístico t de cada uno, su p-valor, el $R^2$ del modelo completo y varios diagnósticos — la salida "tipo R" que menciona la [[01 - Introduccion a statsmodels|introducción]] de esta carpeta.

## Por qué esto resuelve lo que Seaborn no resuelve

> [!important] Controlar una variable de confusión con regresión múltiple
> [[variable de confusión|La nota de Estadística sobre variables de confusión]] señala que `sns.lmplot()` **no protege** de que una relación aparente se deba a un tercer factor. Agregar ese factor **como predictora adicional** en el modelo (`masa_g ~ largo_pico_mm + especie` en vez de solo `masa_g ~ largo_pico_mm`) es, precisamente, la forma de **controlarlo**: el coeficiente de `largo_pico_mm` queda estimado *ya teniendo en cuenta* la especie, en vez de mezclar ambos efectos.

## Leer los resultados

```python
modelo.params        # coeficientes estimados
modelo.pvalues        # p-valor de cada coeficiente
modelo.rsquared        # proporción de la variabilidad explicada por el modelo
modelo.conf_int()      # intervalos de confianza de cada coeficiente
```

> [!note] $R^2$ y la variabilidad de Estadística
> El $R^2$ responde "¿qué proporción de la [[medidas de dispersión|variabilidad]] de la variable respuesta explica el modelo?" — un $R^2 = 0{,}70$ significa que el 70 % de la variabilidad de `masa_g` queda explicada por las predictoras, y el 30 % restante es variabilidad no explicada (ruido, u otras variables no incluidas).

## WLS: cuando la varianza no es constante

```python
modelo_wls = smf.wls('masa_g ~ largo_pico_mm', data=pinguinos, weights=1/varianza_estimada).fit()
```

`OLS` asume que la dispersión de los residuos es **constante** en todo el rango de las predictoras (homocedasticidad, ver [[04 - Diagnostico de modelos]]). Cuando no lo es, `WLS` (*Weighted Least Squares*) le da menos peso a las observaciones con más varianza esperada.

## Relacionado
- [[01 - Introduccion a statsmodels]]
- [[variable de confusión]]
- [[medidas de dispersión]]
- [[07 - Regresion y relaciones estadisticas]]
- [[04 - Diagnostico de modelos]]
