---
titulo: "Matplotlib - Escalas, ticks y guardar figuras"
materia: Matplotlib
tipo: apunte
tags:
  - matplotlib
  - tecnologias
  - python
  - tema/personalizacion
fuente: "Matplotlib.pdf (documentación oficial, release 3.11.1)"
---

# Escalas, ticks y guardar figuras

## Límites de los ejes

```python
ax.set_xlim(0, 10)
ax.set_ylim(-2, 2)
```

Si no los fijás, Matplotlib los calcula automáticamente para que entren todos los datos con un margen chico.

## Escalas: lineal vs logarítmica

Por defecto, los ejes son **lineales**. Para datos que varían en varios órdenes de magnitud (muy chicos y muy grandes en el mismo gráfico), una escala logarítmica suele ser más legible:

```python
fig, axs = plt.subplots(1, 2, figsize=(8, 3))

axs[0].plot(x, datos_exponenciales)
axs[0].set_title('Escala lineal')

axs[1].plot(x, datos_exponenciales)
axs[1].set_yscale('log')
axs[1].set_title('Escala logarítmica')
```
**Qué genera:** dos paneles lado a lado con los mismos datos exponenciales — a la izquierda la curva se dispara casi vertical y aplasta los valores chicos contra el eje X; a la derecha (escala log), la misma curva se ve como una línea mucho más recta y legible, con los valores chicos ahora distinguibles.

Atajos directos cuando **ambos** ejes necesitan log: `ax.loglog()`. Para uno solo: `ax.semilogx()` / `ax.semilogy()`.

## Ticks manuales

`set_xticks()` / `set_yticks()` controlan **dónde** van las marcas y, opcionalmente, qué texto llevan:

```python
ax.set_xticks([0, 30, 60, 90], ['cero', '30', 'sesenta', '90'])
ax.set_yticks([-1.5, 0, 1.5])   # sin el segundo argumento, quedan los números tal cual
```

> [!warning] Trampa clásica: strings donde esperabas números
> Si tus categorías del eje X vienen de un archivo leído como texto (aunque parezcan números), Matplotlib las va a tratar como **categorías**, no como valores numéricos — te va a poner un tick por cada string distinto, en el orden en que aparecen. Esto pasa mucho al graficar directamente una columna de un CSV sin convertirla antes con `pd.to_numeric()`.

## Fechas en el eje X

Matplotlib entiende arrays de fechas (`numpy.datetime64`, o una columna `datetime` de Pandas) y les pone automáticamente un formato legible:

```python
from matplotlib.dates import ConciseDateFormatter

fig, ax = plt.subplots()
ax.plot(fechas, valores)
ax.xaxis.set_major_formatter(ConciseDateFormatter(ax.xaxis.get_major_locator()))
```

`ConciseDateFormatter` evita el problema típico de fechas superpuestas o repetidas de más ("2024-01-01", "2024-01-01", "2024-01-02"...) — ajusta automáticamente cuánto detalle mostrar según el rango de fechas.

## Guardar la figura: `savefig()`

```python
fig.savefig('mi_grafico.png', dpi=200, bbox_inches='tight')
```

- **`dpi=`** (*dots per inch*) → resolución. `200` es un buen default para incluir en un informe; `300` para calidad de impresión. Si no lo especificás, usa el dpi que tenga configurada la figura (habitualmente 100, que se ve pixelado si lo agrandás mucho).
- **`bbox_inches='tight'`** → recorta los márgenes sobrantes alrededor del gráfico. Es, en la práctica, casi obligatorio: sin esto es común que se guarde con un margen blanco grande de un lado y las etiquetas cortadas del otro.
- **El formato lo decide la extensión del archivo**: `.png`, `.pdf`, `.svg`, `.jpg` — Matplotlib elige el exportador automáticamente. Para un informe/tesis, `.pdf` o `.svg` (formatos vectoriales) se ven nítidos a cualquier tamaño; `.png` es el estándar para compartir online.

```python
fig.savefig('grafico_vectorial.pdf')          # vectorial, ideal para imprimir/LaTeX
fig.savefig('grafico_para_slack.png', dpi=150)  # raster, para compartir rápido
```

> [!tip] Combo recomendado por defecto
> ```python
> fig.savefig('nombre.png', dpi=200, bbox_inches='tight')
> ```
> Te va a dar un buen resultado en el 90 % de los casos sin tener que pensarlo dos veces.

> [!note] `plt.savefig()` vs `fig.savefig()`
> Si usás el [[03 - Estilos de codigo (OO vs pyplot)|estilo OO]] (recomendado), guardá con `fig.savefig()`. `plt.savefig()` (estilo pyplot) guarda la figura "activa" — funciona, pero es menos explícito sobre cuál figura estás guardando si tenés varias abiertas.

## Relacionado
- [[02 - Anatomia de una figura]]
- [[07 - Subplots y multiples ejes]]
- [[05 - Personalizacion - color, estilo y marcadores]]
