---
titulo: Función de distribución acumulada (CDF empírica)
materia: Estadística
tipo: concepto
tags:
  - estadistica
  - maestria
  - concepto
  - tema/variabilidad
fecha: 2026-08-08
---

# Función de distribución acumulada (CDF empírica)

Comparar dos [[histograma|histogramas]] a simple vista es más difícil de lo que parece: dos distribuciones con formas parecidas pero centradas en valores levemente distintos pueden verse casi idénticas en un histograma, sobre todo si tienen pocos datos o los intervalos de clase no coinciden entre ambos gráficos. Hace falta una forma de resumir la distribución que no dependa de cómo se cortaron los intervalos, y que muestre con más claridad las diferencias sistemáticas entre dos conjuntos de datos.

> [!definition] Función de distribución acumulada empírica (ECDF / ojiva)
> Para un conjunto de $n$ datos, la función que a cada valor $x$ le asigna la **proporción de datos menores o iguales a $x$**:
> $$F(x) = \frac{\text{cantidad de datos} \le x}{n}$$
> Es una función **creciente** (nunca baja), que empieza en 0 (antes del dato mínimo) y termina en 1 (después del dato máximo). En el vocabulario de control de calidad esta misma curva se llama **ojiva**, y ya aparece mencionada de pasada en [[distribución de frecuencias]] como la versión gráfica de la frecuencia relativa acumulada $H_i$; esta nota la desarrolla como herramienta propia.

## Cómo leerla

- Un **tramo casi vertical** (la curva sube rápido) indica una zona donde **muchos datos están concentrados** en un rango chico de valores.
- Un **tramo casi horizontal** (la curva casi no sube) indica una zona donde **hay pocos o ningún dato** — un "vacío" en la distribución.
- El valor de $F(x)$ en cualquier punto **es**, por definición, el rango percentil de $x$: leer la CDF en un punto es exactamente responder "¿qué porcentaje de los datos es menor o igual a este valor?" (ver [[medidas de posición]]).

## Ejemplo: comparar dos muestras chicas

Diámetros (mm) de piezas de dos máquinas, mismo ejemplo de [[02 - El estudio de la variabilidad|la clase 2]]:

```python
import numpy as np

maquina_1 = np.array([98, 99, 99, 100, 100, 101, 101, 102])
maquina_2 = np.array([99, 100, 101, 101, 102, 102, 103, 104])

def ecdf(x, val):
    return np.mean(x <= val)

for val in [99, 100, 101, 102]:
    print(val, ecdf(maquina_1, val), ecdf(maquina_2, val))
# 99  0.375 0.125
# 100 0.625 0.250
# 101 0.875 0.500
# 102 1.000 0.750
```

En cada valor de diámetro, la proporción acumulada de la Máquina 1 es **mayor** que la de la Máquina 2 (0.375 vs. 0.125 en 99 mm; 0.875 vs. 0.5 en 101 mm). Eso significa que la curva de la Máquina 1 queda sistemáticamente **a la izquierda** de la curva de la Máquina 2: la Máquina 1 produce piezas de diámetro **más chico**, en todo el rango de valores, no solo en el promedio (100.0 mm contra 101.5 mm). Esta lectura —una curva completa corrida respecto de la otra— es más difícil de apreciar comparando dos histogramas de 8 datos cada uno, donde el ruido de los intervalos puede tapar el patrón.

> [!important] La CDF no pierde información al no agrupar
> A diferencia del histograma, que necesita elegir un ancho de intervalo (una decisión que puede cambiar la forma aparente del gráfico — ver la regla práctica para elegirlo en [[02 - El estudio de la variabilidad]]), la CDF empírica se calcula directo sobre los datos sin agrupar nada — dos personas que la calculen sobre el mismo dataset siempre obtienen exactamente la misma curva.

## Relación con los percentiles

Leer la CDF "de adentro hacia afuera" (dado un valor, encontrar su proporción acumulada) es la misma idea que el rango percentil (`PercentileRank`); leerla "al revés" (dado una proporción, encontrar el valor que la alcanza) es exactamente el cálculo de un percentil (`Percentile`) — ver [[medidas de posición]] para la distinción completa entre ambas preguntas.

> [!note] En código
> `sns.ecdfplot(data=df, x="columna", hue="grupo")` en Seaborn (ver [[05 - Distribuciones (histplot, kdeplot, ecdfplot)]]) dibuja la ECDF directamente, con una curva por grupo si se pasa `hue=`. `scipy.stats.cumfreq()` (ver [[04 - Frecuencias, cuantiles y percentiles]]) da la versión agrupada en bins, más cercana a la ojiva clásica de la clase.

## Relacionado
- [[02 - El estudio de la variabilidad]]
- [[distribución de frecuencias]]
- [[medidas de posición]]
- [[histograma]]
- [[diagrama de puntos (dot plot)]]
- [[05 - Distribuciones (histplot, kdeplot, ecdfplot)]]
- [[04 - Frecuencias, cuantiles y percentiles]]
