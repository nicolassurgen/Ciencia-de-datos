---
titulo: Matplotlib - Anatomía de una Figura
materia: Matplotlib
tipo: apunte
tags:
  - matplotlib
  - tecnologias
  - python
  - tema/introduccion
fuente: "Matplotlib.pdf (documentación oficial, release 3.11.1)"
---

# Anatomía de una Figura

Entender estas cuatro palabras es la base de **todo** lo que sigue en Matplotlib. Casi cada error de principiante ("¿por qué no me aparece el título?", "¿cómo agrego un segundo gráfico?") se resuelve una vez que tenés clara esta jerarquía.

![[Anatomia de una figura.png]]

## Los cuatro niveles

> [!definition] Figure
> La figura **completa** — la ventana, el PDF, el PNG. Es el contenedor de más alto nivel: guarda referencia a todos sus `Axes` hijos y a elementos "globales" (como una leyenda o un título compartido por toda la figura).
>
> ```python
> fig = plt.figure()              # figura vacía, sin Axes
> fig, ax = plt.subplots()        # figura con un solo Axes
> fig, axs = plt.subplots(2, 2)   # figura con una grilla de 4 Axes
> ```

> [!definition] Axes
> Un **gráfico individual** dentro de la figura: el área donde efectivamente se dibujan los datos, con su título, su eje X, su eje Y (y un tercero si es 3D). Una `Figure` puede tener uno o varios `Axes`.
>
> ⚠️ **Trampa de vocabulario**: `Axes` (con "e") es "el gráfico". `Axis` (sin "e", más abajo) es "un eje" dentro de ese gráfico. Son cosas distintas y Matplotlib los distingue todo el tiempo.
>
> Casi todo lo que hacés en Matplotlib es **llamar a un método de `ax`**: `ax.plot()`, `ax.set_title()`, `ax.set_xlabel()`, `ax.legend()`, etc.

> [!definition] Axis
> Cada uno de los **ejes** (X, Y) dentro de un `Axes`. Controla la escala, los límites, y genera los **ticks** (las marcas) y sus **tick labels** (los números o texto junto a cada marca). Quién decide *dónde* van los ticks es un objeto `Locator`; quién decide *cómo se escriben* es un `Formatter`.

> [!definition] Artist
> **Todo lo que se ve** en la figura es un Artist — hasta la propia `Figure` y el propio `Axes` lo son. Una línea (`Line2D`), un texto, la leyenda, cada barra de un `bar()`: todos son Artists. Cuando Matplotlib "dibuja" la figura, en el fondo está recorriendo y renderizando esta lista de Artists.

## Por qué importa esta jerarquía

> [!important] Regla práctica
> Si querés cambiar algo de **un gráfico puntual** (su título, sus límites, sus ticks) → lo hacés sobre el `Axes` (`ax.algo()`).
> Si querés cambiar algo de **toda la figura** (guardarla, ajustar el tamaño general, agregar una leyenda compartida por varios gráficos) → lo hacés sobre la `Figure` (`fig.algo()`).

Esta es también la razón por la que casi cualquier receta de Matplotlib arranca igual:

```python
fig, ax = plt.subplots()
# ... acá van los ax.algo() ...
plt.show()
```

`fig` queda ahí por si necesitás guardar la figura entera ([[08 - Escalas, ticks y guardar figuras|savefig]]) o armar varios `Axes` ([[07 - Subplots y multiples ejes]]); `ax` es con el que trabajás el 90 % del tiempo.

## Relacionado
- [[01 - Introduccion y primer grafico]]
- [[03 - Estilos de codigo (OO vs pyplot)]]
- [[07 - Subplots y multiples ejes]]
- [[06 - Titulos, etiquetas, leyendas y anotaciones]]
