---
titulo: Diagrama de bastones
materia: Estadística
tipo: concepto
tags:
  - estadistica
  - maestria
  - concepto
  - tema/variabilidad
fecha: 2026-08-19
---

# Diagrama de bastones

Una variable cuantitativa discreta (que surge de **contar**, como el número de imperfecciones en una pieza) no encaja del todo ni en el gráfico de barras (pensado para categorías sin orden numérico) ni en el histograma (pensado para agrupar en intervalos). Tiene su propio gráfico, construido específicamente para valores enteros aislados.

> [!definition] Diagrama de bastones
> "En este gráfico, los diferentes valores de la variable, $y_j$, se presentan en el eje de abscisas y sus frecuencias ($n_j$ o $f_j$) en el eje de ordenadas. Para cada valor se levanta una línea vertical (bastón) de altura igual a su frecuencia." *Fuente: [[Estadística para la resolución de problemas en Ingeniería]], cap. 2.*

## Cuándo usarlo

> [!important] El criterio: continua → histograma, discreta → bastones
> "El histograma es el gráfico para el caso de variables continuas. Si se trata de una variable discreta, corresponde utilizar un gráfico de bastones." *Fuente: [[Estadística para la resolución de problemas en Ingeniería]], cap. 2.*

## Por qué no son barras anchas pegadas

> [!warning] Los valores son puntos aislados, no intervalos
> A diferencia del [[histograma]] (barras pegadas, porque representan intervalos contiguos) o incluso del [[gráfico de barras]] (barras con cierto ancho visual, aunque separadas), el diagrama de bastones usa una línea fina — un "palito" — porque cada valor de una variable discreta es un **punto aislado** en la recta numérica, no un intervalo. Dibujar barras anchas sugeriría, incorrectamente, que hay valores intermedios posibles entre, por ejemplo, 1 y 2 imperfecciones — cuando en realidad no los hay.

## Ejemplo aplicado: imperfecciones por pieza

Retomando el caso ya usado en [[02 - El estudio de la variabilidad|la clase]]: muestra de 50 piezas metálicas, se cuenta el número de imperfecciones de cada una.

| Nº imperf. | $f_i$ |
|---:|---:|
| 0 | 23 |
| 1 | 17 |
| 2 | 7 |
| 3 | 1 |
| 4 | 2 |

![[Diagrama de bastones - imperfecciones por pieza.png]]

```python
import matplotlib.pyplot as plt

valores = [0, 1, 2, 3, 4]
frecuencias = [23, 17, 7, 1, 2]

fig, ax = plt.subplots()
ax.vlines(valores, 0, frecuencias, linewidth=2)
ax.plot(valores, frecuencias, "o")
ax.set_xlabel("Número de imperfecciones")
ax.set_ylabel("Frecuencia absoluta ($f_i$)")
```

La forma —claramente asimétrica a la derecha, con la mayoría de las piezas en 0 o 1 imperfecciones y una cola corta hacia valores más altos— es la misma lectura de [[forma de una distribución]] aplicada acá a una variable discreta. Estos mismos datos, junto con su [[boxplot]] y [[distribución de frecuencias|tabla de frecuencias acumuladas]], se retoman en [[medidas de dispersión]] para ilustrar la detección de atípicos por el criterio 1.5·RIQ.

## Dónde reaparece más adelante

> [!info] El mismo gráfico, para la función de probabilidad puntual
> Este gráfico no es exclusivo de la estadística descriptiva: la misma forma (un bastón por valor, altura = frecuencia relativa) se usa más adelante en la materia para representar la **función de probabilidad puntual** de una variable aleatoria discreta — ahí la altura de cada bastón ya no es una frecuencia observada sino una probabilidad teórica. *Fuente: [[Estadística para la resolución de problemas en Ingeniería]], cap. 3.*

> [!note] En código
> `ax.vlines(valores, 0, frecuencias)` combinado con `ax.plot(valores, frecuencias, "o")` en Matplotlib (como en el ejemplo de arriba) es la forma más directa. `sns.stripplot` o un `stem plot` (`plt.stem()`) son alternativas equivalentes.

## Relacionado
- [[distribución de frecuencias]]
- [[gráfico de barras]]
- [[histograma]]
- [[forma de una distribución]]
- [[función de distribución acumulada (CDF empírica)]]
- [[02 - El estudio de la variabilidad]]
