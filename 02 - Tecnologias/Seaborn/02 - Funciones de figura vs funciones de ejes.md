---
titulo: "Seaborn - Funciones de figura vs funciones de ejes"
materia: Seaborn
tipo: apunte
tags:
  - seaborn
  - tecnologias
  - python
  - tema/introduccion
fuente: "seaborn.pydata.org (documentación oficial)"
---

# Funciones de figura vs funciones de ejes

Esta es, sin exagerar, **la distinción más importante de toda la librería**. Si la tenés clara desde el principio, te ahorrás la mayoría de la confusión típica de quien recién arranca con Seaborn (¿por qué a veces me da un `FacetGrid` y a veces un `Axes`? ¿por qué `figsize` a veces no funciona?).

![[Figura vs ejes.png]]

## Las dos familias

> [!definition] Función de ejes (*axes-level*)
> Dibuja sobre **un único** `Axes` de Matplotlib (ver [[02 - Anatomia de una figura]]) y lo devuelve. Es, literalmente, un reemplazo directo de una función de Matplotlib: `sns.scatterplot(ax=ax)` funciona exactamente como esperarías si ya conocés `ax.scatter()`.

> [!definition] Función de figura (*figure-level*)
> No dibuja sobre un `Axes` que le pases — **es dueña de toda la figura**. Por dentro usa un objeto propio de Seaborn (`FacetGrid`, ver [[08 - Grids y comparaciones multiples]]) para armar uno o varios `Axes`, y ahí adentro llama a la función de ejes correspondiente.

Cada "familia" de gráficos tiene **una sola** función de figura, que sirve de interfaz unificada a varias funciones de ejes:

| Familia | Función de figura | Funciones de ejes que envuelve |
|---|---|---|
| Relacional | `relplot()` | `scatterplot()`, `lineplot()` |
| Distribución | `displot()` | `histplot()`, `kdeplot()`, `ecdfplot()` |
| Categórica | `catplot()` | `stripplot()`, `swarmplot()`, `boxplot()`, `violinplot()`, `barplot()`, `countplot()`, `pointplot()`, `boxenplot()` |

El parámetro `kind=` es el que elige, dentro de una función de figura, cuál función de ejes se usa por debajo:

```python
sns.displot(data=penguins, x="flipper_length_mm", kind="kde")   # -> por dentro llama a kdeplot
sns.catplot(data=tips, x="day", y="total_bill", kind="box")      # -> por dentro llama a boxplot
```

## La misma idea, escrita de las dos formas

```python
# Axes-level: vos armás la figura, Seaborn dibuja sobre TU Axes
f, axs = plt.subplots(1, 2, figsize=(8, 4))
sns.scatterplot(data=penguins, x="flipper_length_mm", y="bill_length_mm", ax=axs[0])
sns.histplot(data=penguins, x="species", ax=axs[1])
# Qué genera: dos paneles lado a lado dentro de la MISMA figura de Matplotlib -> a la
# izquierda un scatter, a la derecha un histograma de conteo por especie. Esto solo es
# posible porque scatterplot/histplot son funciones de EJES (aceptan ax=); no funcionaría
# con relplot/displot, que son funciones de FIGURA y exigen ser dueñas de toda la figura.

# Figure-level: Seaborn arma la figura por vos
sns.displot(data=penguins, x="flipper_length_mm", kind="kde")
```

## Cómo elegir

> [!important] Reglas prácticas
> - ¿Necesitás **combinar** el gráfico de Seaborn con otros `Axes` que armaste vos (por ejemplo, dentro de un [[07 - Subplots y multiples ejes|subplot]] de Matplotlib con varios paneles distintos)? → **axes-level**, y pasále `ax=`.
> - ¿Necesitás **facetar** — repetir el mismo gráfico separado por una variable categórica (una columna por sexo, una fila por año)? → **figure-level**, con `col=`/`row=` (ver [[08 - Grids y comparaciones multiples]]).
> - ¿Es una exploración rápida de una sola relación, sin necesidad de combinarla con nada más? → cualquiera de las dos funciona; la mayoría de los ejemplos de esta guía usan la función de figura porque es más corta de escribir.

## Las 4 diferencias que te van a generar dudas

> [!warning] Tamaño: `height`/`aspect` vs. `figsize`
> Las funciones de figura **no** aceptan `figsize`. Usan `height` (alto de **cada** subplot, en pulgadas) y `aspect` (ancho relativo al alto). Si facetaste en 3 columnas, el ancho total termina siendo `height × aspect × 3` — no lo fijás vos directamente.

> [!warning] Lo que te devuelven es distinto
> `sns.scatterplot(...)` devuelve un `Axes` de Matplotlib — podés seguir llamando `ax.set_xlabel(...)` normalmente. `sns.relplot(...)` devuelve un `FacetGrid` — para tocar los ejes desde ahí se usa `g.set_axis_labels(...)` o `g.ax.set_title(...)` (si hay un solo panel) / `g.axes` (si hay varios).

> [!warning] La leyenda aparece en otro lugar
> Las funciones de figura ponen la leyenda de `hue`/`size`/`style` **afuera** del área de gráfico por defecto. Las funciones de ejes la ponen adentro, como cualquier `ax.legend()` de Matplotlib.

## Relacionado
- [[01 - Introduccion a Seaborn]]
- [[04 - Relaciones entre variables (scatterplot, lineplot)]]
- [[08 - Grids y comparaciones multiples]]
- [[02 - Anatomia de una figura]]
