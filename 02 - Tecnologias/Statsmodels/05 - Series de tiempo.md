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

estadistico, p_valor, *_ = adfuller(ventas_mensuales)
p_valor   # 0.62 -> p > 0.05: no se puede rechazar que la serie NO es estacionaria (tiene tendencia)
```

El test de Dickey-Fuller aumentado (ADF) evalúa si una serie es **estacionaria** (su media y varianza no cambian con el tiempo) — la versión formal de preguntar si la serie tiene solo [[causas comunes y causas especiales|causas comunes]] actuando, o si hay una tendencia/quiebre (causas especiales) que la hace no estacionaria.

## Descomponer: tendencia, estacionalidad, residuo

```python
from statsmodels.tsa.seasonal import STL

resultado = STL(ventas_mensuales, period=12).fit()   # period=12 -> estacionalidad anual, datos mensuales
resultado.plot()
```

Devuelve tres series del mismo largo que la original: `resultado.trend` (la tendencia de fondo, sin el vaivén mensual), `resultado.seasonal` (el patrón que se repite cada 12 meses) y `resultado.resid` (lo que queda después de sacar ambas — el ruido).

> [!tip] Qué mirar en `resultado.plot()`
> El método dibuja **cuatro paneles apilados**, todos con el mismo eje x (tiempo) y cada uno con su propia escala en el eje y: la serie original arriba, después `trend`, después `seasonal`, y `resid` abajo. Leerlos de arriba hacia abajo es leer "cuánto de la serie original queda explicado en cada paso": si `trend` sube sostenidamente, hay una tendencia real de fondo; si `seasonal` muestra un patrón que se repite idéntico cada 12 puntos, la estacionalidad es fuerte y estable; y si `resid` se ve como ruido disperso alrededor de cero, sin ningún patrón visible, la descomposición capturó bien la estructura — un patrón que **todavía** se nota en el residuo (otra tendencia, otra estacionalidad) significa que `period` o el modelo elegido no alcanzan para explicar toda la serie.

Separa una serie en tres componentes: **tendencia** (el promedio móvil que ya se calcula con `.rolling()` de Pandas, ver [[series de tiempo]]), **estacionalidad** (el patrón que se repite cada `period` observaciones) y **residuo** (lo que sobra, análogo a los residuos de una regresión).

## Autocorrelación: ¿un valor depende de los anteriores?

```python
from statsmodels.graphics.tsaplots import plot_acf, plot_pacf

plot_acf(ventas_mensuales)    # ¿el valor de este mes se parece al de 1, 2, 3... meses atrás?
plot_pacf(ventas_mensuales)   # lo mismo, pero descontando el efecto de los lags intermedios
```

Mide qué tan correlacionado está cada valor de la serie con sus propios valores pasados (*lags*) — información clave para elegir cuántos términos autorregresivos necesita un modelo ARIMA.

> [!tip] Qué mirar en un correlograma (ACF/PACF)
> El eje x es el **lag** (cuántos períodos atrás: 1, 2, 3 meses...); el eje y es el coeficiente de correlación (entre -1 y 1) entre la serie y su versión desplazada ese lag. Cada barra vertical es la autocorrelación en ese lag específico, y el **área sombreada horizontal** alrededor de cero es la banda de significancia (aprox. 95%): una barra que sobresale de la banda indica una autocorrelación estadísticamente distinta de cero en ese lag; una barra dentro de la banda es indistinguible de ruido.
> - Si el **ACF decae lentamente** (muchos lags seguidos fuera de la banda, cayendo poco a poco) y el **PACF corta abruptamente** después de un lag $p$ (nada significativo después), es la firma típica de un proceso **AR(p)**.
> - Si es al revés —el **PACF decae lentamente** y el **ACF corta** después de un lag $q$—, es la firma típica de un proceso **MA(q)**.
> - Picos regulares cada 12 lags (con datos mensuales) son la marca de estacionalidad anual todavía sin remover — la misma que separa `STL` en `seasonal`.

## Modelar y pronosticar: ARIMA

```python
from statsmodels.tsa.arima.model import ARIMA

modelo = ARIMA(ventas_mensuales, order=(1, 1, 1)).fit()   # (AR, diferenciación, MA)
modelo.forecast(steps=3)
# 2027-01    418.2
# 2027-02    422.7
# 2027-03    425.1
```

`ARIMA` combina autoregresión (el valor depende de valores pasados), diferenciación (para volver estacionaria una serie que no lo es) y promedio móvil de errores pasados. `ExponentialSmoothing` y `AutoReg` son alternativas más simples cuando no hace falta tanta flexibilidad.

> [!tip] La diferenciación es una derivada discreta
> $y_t - y_{t-1}$ (la diferenciación de la serie) es la misma idea que la tasa de cambio promedio $\frac{f(x+h)-f(x)}{h}$ de [[02 - Derivadas]], con $h=1$ (un período) en vez de $h\to0$: mide cuánto cambió la serie de un momento al siguiente. Por eso diferenciar "quita tendencia" — una serie que crece en línea recta tiene una diferencia casi constante, igual que la derivada de una función lineal es una constante.

## Relacionado
- [[01 - Introduccion a statsmodels]]
- [[series de tiempo]]
- [[causas comunes y causas especiales]]
- [[distribución de frecuencias]]
