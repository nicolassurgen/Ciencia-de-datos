---
titulo: "Matplotlib - Colorbars y mapas de color"
materia: Matplotlib
tipo: apunte
tags:
  - matplotlib
  - tecnologias
  - python
  - tema/visualizacion
fuente: "Matplotlib — Choosing Colormaps (matplotlib.org/stable/users/explain/colors/colormaps.html); Python Data Science Handbook (Jake VanderPlas) — Parte IV"
---

# Colorbars y mapas de color

## El problema: codificar una tercera variable con color

Un scatter de dos variables ya usa los dos ejes. Si querés mostrar una **tercera variable continua** (por ejemplo, `masa_g` en un scatter de `largo_pico_mm` vs. `ancho_pico_mm`), el color de cada punto es el recurso natural — pero a diferencia de la [[06 - Titulos, etiquetas, leyendas y anotaciones|leyenda]] (que identifica categorías discretas), una escala continua de color necesita una **colorbar**: una referencia visual de qué valor representa cada tono.

```python
plt.scatter(df["largo_pico_mm"], df["ancho_pico_mm"], c=df["masa_g"], cmap="viridis")
plt.colorbar(label="Masa (g)")
```

`c=` mapea una columna numérica a color; `cmap=` elige la paleta; `plt.colorbar()` agrega la referencia.

## Elegir el mapa de color según el tipo de variable

> [!important] La elección del cmap no es estética — depende de la escala de medición
> Igual que [[escalas de medición|el tipo de variable]] decide qué gráfico y qué medida de resumen corresponden, decide también qué **categoría** de mapa de color usar:

| Categoría | Cuándo usarla | Ejemplos | Variable que codifica |
|---|---|---|---|
| **Secuencial** | La variable tiene un orden natural de "menos" a "más" | `viridis`, `Blues` | Cuantitativa (continua o discreta) |
| **Divergente** | Hay un punto central significativo (cero, un promedio) y lo que importa es desviarse para un lado u otro | `RdBu`, `PuOr` | Cuantitativa con un punto de referencia (ej. desvíos respecto de la media) |
| **Cualitativa** | No hay orden entre los valores — son categorías | `tab10`, `Set2` | Cualitativa (nominal) |

> [!warning] Un mapa de color mal elegido puede mentir
> Usar un cmap **cualitativo** (como el viejo default `jet`) para una variable **cuantitativa** es engañoso: esos mapas no tienen una progresión uniforme de brillo, así que dos valores cercanos pueden verse tan distintos como dos valores lejanos. Es el equivalente visual de tratar una variable [[escalas de medición|nominal como si fuera de razón]]: se pierde (o se inventa) información de orden que no corresponde.

## Personalizar la colorbar

```python
plt.colorbar(label="Masa (g)", extend="both")   # flechas en los extremos si hay datos fuera de rango
plt.clim(3000, 6000)                             # fijar el rango de colores manualmente
```

## Relacionado
- [[05 - Personalizacion - color, estilo y marcadores]]
- [[06 - Titulos, etiquetas, leyendas y anotaciones]]
- [[escalas de medición]]
- [[04 - Relaciones entre variables (scatterplot, lineplot)]]
