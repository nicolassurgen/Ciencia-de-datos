---
titulo: Series de tiempo
materia: Estadística
tipo: concepto
tags:
  - estadistica
  - maestria
  - concepto
  - tema/variabilidad
fecha: 2026-08-03
---

# Series de tiempo

> [!definition] Serie de tiempo
> Conjunto de datos de una variable registrados **a lo largo del tiempo**, en el que el **orden temporal es información relevante** y no puede ignorarse sin perder lo esencial del fenómeno.

## Cuándo NO construir una distribución de frecuencias

Cuando la variable se registra a través del tiempo y **no muestra un comportamiento estable**, no tiene sentido resumirla en una [[distribución de frecuencias]]: aplastar el tiempo en una tabla borra justamente la información más importante (la evolución, las tendencias, los picos).

> [!example] El diagrama de Nightingale (guerra de Crimea)
> El gráfico de mortalidad del ejército británico mostrado por Florence Nightingale (causas de muerte antes/después de la comisión sanitaria) es un ejemplo clásico de serie de tiempo, no de distribución de frecuencias. Lo relevante ahí es cómo **cae la mortalidad tras la intervención sanitaria**, algo que solo se ve respetando el eje temporal.

## Regla práctica

> [!tip] Si hay tiempo y el proceso no es estable → graficá contra el tiempo
> Un gráfico de secuencia/serie (valor vs. tiempo) es la herramienta apropiada. Las distribuciones de frecuencias y las medidas de resumen (media, desvío, etc.) suponen datos **sin estructura temporal relevante**, o al menos un proceso **estable** en el tiempo.

## Conexión con estabilidad del proceso

La pregunta de si "conviene" tratar los datos como una distribución de frecuencias o como una serie de tiempo está ligada a la distinción entre [[causas comunes y causas especiales]]: si el proceso solo tiene variabilidad por causas comunes (estable), el orden temporal aporta poco extra y una distribución resume bien los datos. Si hay causas especiales actuando (tendencias, quiebres, rachas), el tiempo es la dimensión que las revela.

> [!note] En código
> `DatetimeIndex` + `.resample()` en Pandas (ver [[08 - Series de tiempo]]) es la herramienta central para esto: agrupa por intervalos de tiempo en vez de por categoría, y `.rolling()` calcula el promedio móvil que separa la tendencia del ruido de corto plazo. Cuando haga falta ir más allá de describir la serie y **modelarla** (pronosticar, testear si es estacionaria, separar tendencia/estacionalidad formalmente), esa es la función de `statsmodels.tsa` — ver [[05 - Series de tiempo]] de statsmodels.

## Relacionado
- [[02 - El estudio de la variabilidad]]
- [[distribución de frecuencias]]
- [[causas comunes y causas especiales]]
- [[08 - Series de tiempo]]
- [[05 - Series de tiempo]]
