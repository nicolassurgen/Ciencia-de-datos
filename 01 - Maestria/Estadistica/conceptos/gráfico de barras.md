---
titulo: Gráfico de barras
materia: Estadística
tipo: concepto
tags:
  - estadistica
  - maestria
  - concepto
  - tema/variabilidad
fecha: 2026-08-19
---

# Gráfico de barras

Es, junto con el histograma, uno de los gráficos más reconocibles de la estadística — pero se lo suele confundir con su primo, el histograma, aunque sirven para variables de naturaleza distinta. La diferencia no es solo estética: tiene que ver con qué tipo de variable representa cada uno.

> [!definition] Gráfico de barras
> Gráfico para una variable **cualitativa** (categórica) construido a partir de una [[distribución de frecuencias|tabla de frecuencias]]. A cada categoría se le asigna una barra cuya altura es proporcional a su frecuencia. *Fuente: [[Estadística para la resolución de problemas en Ingeniería]], cap. 2.*

## Reglas de construcción

> [!important] Todas las barras iguales, separadas, y el eje empieza en cero
> "A cada clase se le asigna una barra cuya altura es proporcional a la frecuencia. Todas las barras tienen el mismo ancho y color y están separadas entre sí por el mismo espacio. La escala del eje donde se representan las frecuencias debe comenzar en 0 para evitar que las interpretaciones se distorsionen." *Fuente: [[Estadística para la resolución de problemas en Ingeniería]], cap. 2.*

> [!quote] Practical Statistics for Data Scientists
> "Bar charts are a common visual tool for displaying a single categorical variable [...] Categories are listed on the x-axis, and frequencies or proportions on the y-axis." *Fuente: [[Practical Statistics for Data Scientists]] (Bruce & Bruce), cap. 1.*

## Gráfico de barras vs. histograma: la diferencia real

> [!warning] No son el mismo gráfico con otro nombre
> "Histograms and bar charts are similar, except that the categories on the x-axis in the bar chart are not ordered." *Fuente: [[Practical Statistics for Data Scientists]] (Bruce & Bruce), cap. 1.* En un [[histograma]], las barras van **pegadas** entre sí porque representan intervalos contiguos de una variable numérica continua — hay un orden natural de izquierda a derecha. En un gráfico de barras, las barras van **separadas** porque las categorías no tienen un orden intrínseco (o, si lo tienen, ese orden no es lo que el eje representa por defecto) — el orden en que aparecen las categorías es una elección de quien grafica, no una propiedad de los datos.

## Ejemplo aplicado: motivos de queja de una ferretería

Retomando el mismo caso ya usado en [[02 - El estudio de la variabilidad|la clase]] y en [[diagrama de Pareto]] — 350 quejas registradas, clasificadas por motivo principal (variable nominal):

![[Grafico de barras - motivos de queja.png]]

```python
import matplotlib.pyplot as plt

motivos = ["Factura no\ncorresponde", "Envases en\nmalas cond.", "Dimensiones\nincorrectas",
           "Manchas\no poros", "Golpes o\nabolladuras", "Envío no\ncoincidente", "Pedido con\nretraso"]
frecuencias = [115, 76, 58, 40, 25, 21, 15]

fig, ax = plt.subplots(figsize=(8, 5))
ax.bar(motivos, frecuencias)
ax.set_ylabel("Frecuencia absoluta ($f_i$)")
```

Este gráfico usa el **mismo orden** en que aparecen los motivos en la tabla original — a diferencia del [[diagrama de Pareto]], que ordena las barras de mayor a menor frecuencia a propósito para hacer visible el "codo" del 80/20. Es la misma información, con un ordenamiento distinto según lo que se quiera resaltar.

## Cuándo preferirlo sobre el gráfico de torta

> [!tip] Barras en vez de torta
> Aunque el gráfico de torta (circular) es una alternativa habitual para variables cualitativas, se tiende a evitarlo en la práctica: comparar **ángulos o áreas** de porciones es visualmente más difícil que comparar la **altura** de barras alineadas sobre un mismo eje. Un gráfico de barras casi siempre comunica la misma información con menos ambigüedad — más aún cuantas más categorías haya. *Fuente: [[Estadística para la resolución de problemas en Ingeniería]], cap. 2; [[Practical Statistics for Data Scientists]] (Bruce & Bruce), cap. 1.*

> [!note] En código
> `sns.countplot(data=df, x="columna")` en Seaborn (ver [[06 - Variables categoricas (boxplot, violinplot, barplot)]]) o `df['columna'].value_counts().plot.bar()` en Pandas. `ax.bar()` en Matplotlib (ver [[04 - Tipos de graficos basicos]]) es la versión de bajo nivel usada en el ejemplo de arriba.

## Relacionado
- [[distribución de frecuencias]]
- [[diagrama de Pareto]]
- [[diagrama de bastones]]
- [[histograma]]
- [[02 - El estudio de la variabilidad]]
