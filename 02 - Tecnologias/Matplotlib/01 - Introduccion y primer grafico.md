---
titulo: Matplotlib - Introducción y primer gráfico
materia: Matplotlib
tipo: apunte
tags:
  - matplotlib
  - tecnologias
  - python
  - tema/introduccion
fuente: "Matplotlib.pdf (documentación oficial, release 3.11.1)"
---

# Introducción y primer gráfico

> [!definition] Matplotlib
> Una librería de Python para crear visualizaciones **estáticas, animadas e interactivas**. Es la librería de gráficos más antigua y más usada del ecosistema científico de Python — casi todo lo demás (Pandas `.plot()`, Seaborn) se construye **encima** de Matplotlib.

## Instalación

```bash
pip install matplotlib
```

O si trabajás con conda:

```bash
conda install -c conda-forge matplotlib
```

## La forma en que siempre vas a importarla

Por convención (universal, la vas a ver en el 100 % de los ejemplos que existen), Matplotlib se importa así:

```python
import matplotlib.pyplot as plt
import numpy as np
```

`pyplot` es el módulo con el que se arma casi todo. `numpy` no es parte de Matplotlib, pero siempre aparece al lado porque Matplotlib espera que los datos vengan como arrays (ver [[distribución de frecuencias]] y [[medidas de posición]] de Estadística para el tipo de datos que normalmente vas a graficar).

## Tu primer gráfico

```python
fig, ax = plt.subplots()          # crea una Figura con un solo Axes
ax.plot([1, 2, 3, 4], [1, 4, 2, 3])   # dibuja los datos sobre ese Axes
plt.show()                        # muestra la figura
```
**Qué genera:** una línea quebrada que conecta 4 puntos en zigzag: sube de (1,1) a (2,4), baja a (3,2), y vuelve a subir a (4,3) — una imagen simple, sin título ni etiquetas todavía (eso viene en [[06 - Titulos, etiquetas, leyendas y anotaciones]]).

Tres líneas, tres ideas distintas:

1. **`plt.subplots()`** crea el "lienzo" — una `Figure` (la ventana/imagen completa) que contiene un `Axes` (el área donde efectivamente se dibujan los datos). Ver [[02 - Anatomia de una figura]] para entender esta distinción a fondo, porque es la base de **todo** lo que sigue.
2. **`ax.plot(x, y)`** dibuja la serie de datos sobre ese `Axes`.
3. **`plt.show()`** renderiza y muestra la figura en pantalla.

> [!tip] En Jupyter Notebook `plt.show()` casi nunca hace falta
> Los notebooks muestran automáticamente cualquier figura creada en una celda. `plt.show()` importa sobre todo cuando corrés un script `.py` desde la terminal — sin esa línea, el script termina y no llegás a ver nada.

## ¿Qué son exactamente `fig` y `ax`?

> [!important] La distinción más importante para arrancar
> - **`fig`** (`Figure`) → la figura completa: el "papel" donde entra todo (uno o más gráficos, títulos generales, etc.).
> - **`ax`** (`Axes`) → un gráfico individual dentro de esa figura: el área con ejes X/Y donde se dibujan los datos.
>
> Una `Figure` puede contener **varios** `Axes` (varios gráficos uno al lado del otro) — eso es justamente lo que se arma con [[07 - Subplots y multiples ejes|subplots]].

## Datos de entrada: ¿listas o arrays?

Matplotlib espera `numpy.array` (o algo convertible a uno) como entrada. Las listas comunes de Python funcionan porque se convierten solas, pero si usás Pandas, lo más prolijo es pasar directamente las columnas del `DataFrame`:

```python
import pandas as pd

df = pd.DataFrame({"x": [1, 2, 3, 4], "y": [1, 4, 2, 3]})
fig, ax = plt.subplots()
ax.plot(df["x"], df["y"])
plt.show()
```

## Recorrido de estas notas

Este es el orden pensado para ir de cero a poder armar tus propios gráficos:

1. **Introducción y primer gráfico** *(esta nota)*
2. [[02 - Anatomia de una figura]] — Figure, Axes, Axis, Artist: el vocabulario que se usa en todo lo demás.
3. [[03 - Estilos de codigo (OO vs pyplot)]] — por qué vas a ver código de Matplotlib escrito de dos formas distintas.
4. [[04 - Tipos de graficos basicos]] — plot, scatter, bar, hist, pie, boxplot.
5. [[05 - Personalizacion - color, estilo y marcadores]] — colores, líneas, marcadores, `plt.style.use()`.
6. [[06 - Titulos, etiquetas, leyendas y anotaciones]] — hacer que un gráfico se entienda solo.
7. [[07 - Subplots y multiples ejes]] — más de un gráfico por figura.
8. [[08 - Escalas, ticks y guardar figuras]] — escala log, ticks manuales, `savefig()`.
9. [[09 - Colorbars y mapas de color]] — codificar una tercera variable continua con color.

## Relacionado
- [[02 - Anatomia de una figura]]
- [[03 - Estilos de codigo (OO vs pyplot)]]
- [[04 - Tipos de graficos basicos]]
