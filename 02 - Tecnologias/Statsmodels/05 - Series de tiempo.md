---
titulo: "statsmodels - Series de tiempo"
materia: statsmodels
tipo: apunte
tags:
  - statsmodels
  - tecnologias
  - python
  - tema/series-de-tiempo
fuente: "statsmodels documentation — tsa.api (statsmodels.org/stable/api.html)"
---

# Series de tiempo

Esta es la nota de statsmodels con el puente **más directo** hacia Estadística: [[series de tiempo|la nota de la materia]] ya define qué es una serie de tiempo y por qué no conviene resumirla con una [[distribución de frecuencias]] cuando el proceso no es estable — `statsmodels.tsa` es el conjunto de herramientas que trabaja formalmente con esa estructura temporal.

> [!info] Contenido a futuro
> El curso todavía no llegó a modelado de series de tiempo (solo a graficarlas y reconocerlas conceptualmente). Esta nota queda como referencia.

## Antes del modelo: ¿es estacionaria?

```python
from statsmodels.tsa.stattools import adfuller

estadistico, p_valor, *_ = adfuller(serie)
```

El test de Dickey-Fuller aumentado (ADF) evalúa si una serie es **estacionaria** (su media y varianza no cambian con el tiempo) — la versión formal de preguntar si la serie tiene solo [[causas comunes y causas especiales|causas comunes]] actuando, o si hay una tendencia/quiebre (causas especiales) que la hace no estacionaria.

## Descomponer: tendencia, estacionalidad, residuo

```python
from statsmodels.tsa.seasonal import STL

resultado = STL(serie, period=12).fit()
resultado.trend, resultado.seasonal, resultado.resid
```

Separa una serie en tres componentes: **tendencia** (el promedio móvil que ya se calcula con `.rolling()` de Pandas, ver [[series de tiempo]]), **estacionalidad** (el patrón que se repite cada `period` observaciones) y **residuo** (lo que sobra, análogo a los residuos de una regresión).

## Autocorrelación: ¿un valor depende de los anteriores?

```python
from statsmodels.graphics.tsaplots import plot_acf, plot_pacf

plot_acf(serie)    # autocorrelación
plot_pacf(serie)   # autocorrelación parcial
```

Mide qué tan correlacionado está cada valor de la serie con sus propios valores pasados (*lags*) — información clave para elegir cuántos términos autorregresivos necesita un modelo ARIMA.

## Modelar y pronosticar: ARIMA

```python
from statsmodels.tsa.arima.model import ARIMA

modelo = ARIMA(serie, order=(1, 1, 1)).fit()   # (AR, diferenciación, MA)
modelo.forecast(steps=12)
```

`ARIMA` combina autoregresión (el valor depende de valores pasados), diferenciación (para volver estacionaria una serie que no lo es) y promedio móvil de errores pasados. `ExponentialSmoothing` y `AutoReg` son alternativas más simples cuando no hace falta tanta flexibilidad.

## Relacionado
- [[01 - Introduccion a statsmodels]]
- [[series de tiempo]]
- [[causas comunes y causas especiales]]
- [[distribución de frecuencias]]
