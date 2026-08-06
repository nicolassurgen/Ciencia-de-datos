---
titulo: Pandas - Series de tiempo
materia: Pandas
tipo: apunte
tags:
  - pandas
  - tecnologias
  - python
  - tema/series-de-tiempo
fuente: "Python Data Science Handbook (Jake VanderPlas) — Parte III"
---

# Series de tiempo

Ya viste en Estadística que cuando los datos tienen [[series de tiempo|dimensión temporal]] no se los puede tratar como una distribución de frecuencias cualquiera: el orden importa, y hace falta respetarlo. Pandas tiene un tipo de índice dedicado exactamente a esto.

## `Timestamp` y `DatetimeIndex`

```python
fecha = pd.to_datetime("4th of July, 2021")   # pd.Timestamp('2021-07-04 00:00:00')

fechas = pd.to_datetime(['2021-07-03', '2021-07-04', '2021-07-06'])
serie = pd.Series([10, 15, 12], index=fechas)   # el índice es un DatetimeIndex
```

Una vez que el índice es un `DatetimeIndex`, Pandas te habilita indexado y slicing **por fecha**, en el mismo estilo `.loc` que ya conocés de [[02 - Indexado y seleccion (loc, iloc)]]:

```python
serie['2021-07-04']              # un día puntual
serie['2021-07-01':'2021-07-05']  # un rango de fechas (¡inclusive en ambos extremos, como loc!)
serie['2021']                     # ¡todo un año! Pandas entiende la fecha "parcial"
```

## Crear un rango de fechas: `pd.date_range`

```python
pd.date_range('2021-07-01', '2021-07-10')          # un timestamp por día
pd.date_range('2021-07-01', periods=8, freq='D')     # 8 días desde una fecha inicial
pd.date_range('2021-01-01', periods=12, freq='ME')   # 12 fines de mes
```

| `freq=` | Significa |
|---|---|
| `'D'` | día |
| `'W'` | semana |
| `'ME'` | fin de mes |
| `'YE'` | fin de año |
| `'h'` | hora |
| `'min'` | minuto |

## Remuestrear: `.resample()`

La operación más importante de esta nota. Cambia la **frecuencia** de una serie de tiempo, agregando (si vas de más detalle a menos, ej. de diario a mensual) o interpolando (si vas al revés):

```python
serie_diaria.resample('ME').mean()    # promedio mensual, a partir de datos diarios
serie_diaria.resample('W').sum()       # suma semanal
```

> [!important] `.resample()` es un `groupby` disfrazado
> Es exactamente el mismo concepto de [[06 - Agregacion y groupby|split-apply-combine]] que ya viste — solo que en vez de agrupar por una columna categórica (`'A'`, `'B'`, `'C'`), agrupa por **intervalos de tiempo**. `serie.resample('ME')` es conceptualmente `serie.groupby(mes_de_cada_fecha)`.

> [!tip] `.resample()` vs `.asfreq()`
> `.resample()` **agrega** (aplica una función: mean, sum, etc.) — cambia cuántos puntos hay. `.asfreq()` simplemente **selecciona** el valor que cae en cada nueva fecha, sin calcular nada — si no hay un dato exacto en esa fecha, te da `NaN` (ver [[04 - Datos faltantes]]).

## Ventanas móviles: `.rolling()`

Para suavizar una serie ruidosa (promedio móvil, muy común antes de graficar una tendencia):

```python
serie.rolling(7).mean()    # promedio móvil de 7 períodos
```

Cada valor de salida es el promedio de **esa observación y las 6 anteriores** — la forma estándar de separar la tendencia de fondo del ruido día a día, conectando con la distinción de [[causas comunes y causas especiales]] de Estadística (causas comunes = variación de corto plazo que un promedio móvil suaviza; una causa especial rompe esa suavidad de forma visible).

## Relacionado
- [[series de tiempo]]
- [[causas comunes y causas especiales]]
- [[06 - Agregacion y groupby]]
- [[02 - Indexado y seleccion (loc, iloc)]]
