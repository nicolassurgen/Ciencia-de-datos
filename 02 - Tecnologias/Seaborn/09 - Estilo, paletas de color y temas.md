---
titulo: "Seaborn - Estilo, paletas de color y temas"
materia: Seaborn
tipo: apunte
tags:
  - seaborn
  - tecnologias
  - python
  - tema/personalizacion
fuente: "seaborn.pydata.org (documentación oficial)"
---

# Estilo, paletas de color y temas

## El tema general

```python
sns.set_theme()                                  # el default: fondo gris, grilla blanca
sns.set_theme(style="whitegrid", palette="muted") # personalizado
```

`style` controla el fondo y la grilla (`"white"`, `"dark"`, `"whitegrid"`, `"darkgrid"`, `"ticks"`); `palette` fija la paleta de colores por defecto para toda la sesión. Es el equivalente de [[05 - Personalizacion - color, estilo y marcadores|`plt.style.use()`]] en Matplotlib, pero pensado específicamente para gráficos estadísticos.

## Elegir la paleta correcta no es estética — es comunicar bien

> [!important] La elección de paleta depende del **tipo de variable**, ni más ni menos
> Esto es, directamente, la [[escalas de medición|clasificación de variables]] de Estadística aplicada al color. Usar el tipo de paleta equivocado no solo se ve peor — **comunica algo falso** sobre tus datos (por ejemplo, sugerir un orden donde no lo hay).

### Cualitativa → paleta *qualitative*

Para variables categóricas (`smoker`, `species`, `day`). Los colores varían en **tono** (hue), no en intensidad, para que ningún grupo "parezca" más importante que otro.

```python
sns.color_palette("deep")       # la paleta por defecto, 10 colores distintos
sns.color_palette("Set2")       # ColorBrewer, buena para pocas categorías
sns.color_palette("colorblind") # segura para daltonismo — buen default si no estás seguro
# Qué genera cada línea: una franja de swatches de color (se ve así en un notebook, sin
# necesidad de plt.show()) — "deep" da colores saturados y distintos entre sí, "Set2" da
# tonos pastel más suaves, "colorblind" prioriza que los colores se distingan aun con
# daltonismo (evita, por ejemplo, poner rojo y verde uno al lado del otro).
```

### Cuantitativa continua → paleta *sequential*

Para una variable numérica que va de menor a mayor (`total_bill`, una densidad, un conteo) — como en el eje X de un [[05 - Distribuciones (histplot, kdeplot, ecdfplot)|histograma]]. Acá el color varía en **luminancia**: claro = valores bajos, oscuro = valores altos.

```python
sns.color_palette("rocket", as_cmap=True)
sns.color_palette("flare", as_cmap=True)     # mejor contraste para líneas/puntos
sns.light_palette("seagreen", as_cmap=True)  # rampa personalizada, de claro a un color
```

### Cuantitativa con un punto de referencia natural → paleta *diverging*

Para una variable numérica donde **el cero (u otro valor) tiene un significado especial** — una correlación (de $-1$ a $1$, con 0 = "sin relación"), una diferencia respecto de una media, un cambio porcentual.

```python
sns.color_palette("vlag", as_cmap=True)
sns.color_palette("icefire", as_cmap=True)
sns.diverging_palette(220, 20, as_cmap=True)   # armás la tuya desde dos matices
```

> [!tip] El ejemplo de manual: un heatmap de correlación
> Ya lo viste en [[08 - Grids y comparaciones multiples|la nota anterior]]: `sns.heatmap(corr, cmap="coolwarm", center=0)`. Una correlación de $-0.8$ y una de $+0.8$ son **igual de fuertes**, solo que en sentido opuesto — una paleta secuencial (todo en una sola dirección de color) escondería esa simetría; la diverging la muestra de inmediato.

## Tabla resumen

| Tipo de variable (Estadística) | Tipo de paleta | Función típica |
|---|---|---|
| Cualitativa (nominal/ordinal con pocos niveles) | Qualitative | `color_palette("deep")` |
| Cuantitativa (sin punto de referencia especial) | Sequential | `color_palette("rocket", as_cmap=True)` |
| Cuantitativa con un cero/centro con significado | Diverging | `color_palette("vlag", as_cmap=True)` |

## Aplicar una paleta a un gráfico puntual

No hace falta cambiar el default global — la mayoría de las funciones aceptan `palette=` directamente:

```python
sns.catplot(data=tips, x="day", y="total_bill", hue="day", palette="Set2")
```

## Relacionado
- [[05 - Personalizacion - color, estilo y marcadores]]
- [[escalas de medición]]
- [[08 - Grids y comparaciones multiples]]
