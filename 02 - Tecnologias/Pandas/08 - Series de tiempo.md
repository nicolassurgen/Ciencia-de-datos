---
titulo: Pandas - Series de tiempo
materia: Pandas
tipo: apunte
tags:
  - pandas
  - tecnologias
  - python
  - tema/series-de-tiempo
fuente: "pandas — Time series / date functionality (pandas.pydata.org/docs/user_guide/timeseries.html); Python Data Science Handbook (Jake VanderPlas) — Parte III"
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
serie['2021-07-04']              # 15  -> un día puntual

serie['2021-07-01':'2021-07-05']  # un rango de fechas (¡inclusive en ambos extremos, como loc!)
# 2021-07-03    10
# 2021-07-04    15
# dtype: int64

serie['2021']                     # ¡todo un año! Pandas entiende la fecha "parcial"
# 2021-07-03    10
# 2021-07-04    15
# 2021-07-06    12
# dtype: int64
```

## Crear un rango de fechas: `pd.date_range`

```python
pd.date_range('2021-07-01', periods=4, freq='D')     # 4 días desde una fecha inicial
# DatetimeIndex(['2021-07-01', '2021-07-02', '2021-07-03', '2021-07-04'],
#               dtype='datetime64[ns]', freq='D')
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
fechas_dia = pd.date_range('2021-07-01', periods=6, freq='D')
serie_diaria = pd.Series([10, 12, 9, 14, 11, 13], index=fechas_dia)

serie_diaria.resample('3D').mean()    # promedio cada 3 días, a partir de datos diarios
# 2021-07-01    10.333333
# 2021-07-04    12.666667
# Freq: 3D, dtype: float64
```

> [!important] `.resample()` es un `groupby` disfrazado
> Es exactamente el mismo concepto de [[06 - Agregacion y groupby|split-apply-combine]] que ya viste — solo que en vez de agrupar por una columna categórica (`'A'`, `'B'`, `'C'`), agrupa por **intervalos de tiempo**. `serie.resample('ME')` es conceptualmente `serie.groupby(mes_de_cada_fecha)`.

> [!tip] `.resample()` vs `.asfreq()`
> `.resample()` **agrega** (aplica una función: mean, sum, etc.) — cambia cuántos puntos hay. `.asfreq()` simplemente **selecciona** el valor que cae en cada nueva fecha, sin calcular nada — si no hay un dato exacto en esa fecha, te da `NaN` (ver [[04 - Datos faltantes]]).

## Ventanas móviles: `.rolling()`

Para suavizar una serie ruidosa (promedio móvil, muy común antes de graficar una tendencia):

```python
serie_diaria.rolling(3).mean()    # promedio móvil de 3 períodos
# 2021-07-01          NaN   -> no hay 2 datos anteriores todavía
# 2021-07-02          NaN
# 2021-07-03    10.333333   -> promedio de 07-01, 07-02, 07-03
# 2021-07-04    11.666667   -> promedio de 07-02, 07-03, 07-04
# 2021-07-05    11.333333
# 2021-07-06    12.666667
# Freq: D, dtype: float64
```

Cada valor de salida es el promedio de **esa observación y las 2 anteriores** (con `rolling(7)` serían las 6 anteriores) — la forma estándar de separar la tendencia de fondo del ruido día a día, conectando con la distinción de [[causas comunes y causas especiales]] de Estadística (causas comunes = variación de corto plazo que un promedio móvil suaviza; una causa especial rompe esa suavidad de forma visible).

## Relacionado
- [[series de tiempo]]
- [[causas comunes y causas especiales]]
- [[06 - Agregacion y groupby]]
- [[02 - Indexado y seleccion (loc, iloc)]]
