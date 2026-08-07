---
titulo: "statsmodels - Modelos multivariados y otros"
materia: statsmodels
tipo: apunte
tags:
  - statsmodels
  - tecnologias
  - python
  - tema/regresion
fuente: "statsmodels documentation — API reference (statsmodels.org/stable/api.html)"
---

# Modelos multivariados y otros

> [!info] Contenido a futuro
> Requiere lo visto en [[02 - Regresion lineal (OLS y WLS)]]. Todavía no se dio en Estadística.

## Modelos mixtos: cuando los datos tienen grupos

```python
import statsmodels.formula.api as smf

modelo = smf.mixedlm('masa_g ~ largo_pico_mm', data=df, groups=df['maquina']).fit()

modelo.params
# Intercept       -2980.1
# largo_pico_mm     178.4     -> efecto de largo_pico_mm, ya controlando la máquina
modelo.random_effects
# {'maquina_1': -35.2, 'maquina_2': 12.7, 'maquina_3': 22.5}   -> cuánto se corre cada máquina del promedio
```

`MixedLM` (*modelo lineal mixto*) modela datos que vienen **agrupados** — el mismo escenario que [[estratificación]] describe en Estadística (pesos medidos por distintas máquinas, cada una con su propio centro). En vez de ignorar los grupos (como haría `OLS`) o estratificar "a mano" y analizar cada grupo por separado, `MixedLM` modela la variabilidad **entre** grupos y **dentro** de cada grupo a la vez, con un término de efecto aleatorio por grupo.

## Reducción de dimensionalidad: PCA y Factor

```python
from statsmodels.multivariate.pca import PCA

medidas = pinguinos[["largo_pico_mm", "ancho_pico_mm", "largo_aleta_mm", "masa_g"]]
resultado = PCA(medidas, ncomp=2)

resultado.rsquare
# comp 0    0.68   -> el primer componente ya explica el 68% de la variabilidad de las 4 medidas
# comp 1    0.88   -> con 2 componentes se explica el 88%
```

`PCA` (*componentes principales*) resume muchas variables correlacionadas en unas pocas combinaciones lineales que capturan la mayor parte de la variabilidad total. `Factor` (análisis factorial) es una técnica emparentada, pensada para cuando se asume que unas pocas variables **latentes** (no observadas directamente) explican las correlaciones entre las variables medidas.

## MANOVA: ANOVA con varias variables de respuesta

```python
from statsmodels.multivariate.manova import MANOVA

resultado = MANOVA.from_formula('masa_g + largo_pico_mm ~ especie', data=df).mv_test()
print(resultado)
# especie: Wilks' lambda = 0.31, p < 0.001
# -> masa_g y largo_pico_mm juntas difieren significativamente entre especies
```

Generaliza el ANOVA de una vía (ver [[06 - Tests de hipotesis - una y dos muestras]] de scipy.stats) a **varias** variables de respuesta analizadas en conjunto, en vez de una por vez.

## Regresión por cuantiles

```python
modelo = smf.quantreg('masa_g ~ largo_pico_mm', data=df).fit(q=0.5)   # regresión de la MEDIANA

modelo.params
# Intercept       -2890.4
# largo_pico_mm     175.2   -> parecido al de OLS acá, pero menos sensible si hay pingüinos atípicos
```

`OLS` modela cómo cambia la **media** de la respuesta según las predictoras. `QuantReg` modela cómo cambia un **percentil** cualquiera (por defecto, `q=0.5` es la mediana) — la versión regresión de la distinción entre [[medidas de posición|media y mediana]] ya vista en Estadística: útil cuando interesa el "caso típico" robusto, o cómo cambia la variabilidad completa de la distribución y no solo su centro.

## Relacionado
- [[01 - Introduccion a statsmodels]]
- [[estratificación]]
- [[medidas de posición]]
- [[06 - Tests de hipotesis - una y dos muestras]]
