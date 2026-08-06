---
titulo: Matplotlib - Subplots y múltiples ejes
materia: Matplotlib
tipo: apunte
tags:
  - matplotlib
  - tecnologias
  - python
  - tema/layout
fuente: "Matplotlib.pdf (documentación oficial, release 3.11.1)"
---

# Subplots y múltiples ejes

Una `Figure` puede contener más de un `Axes` (ver [[02 - Anatomia de una figura]]). Esta nota es sobre cómo armar esos layouts.

## Grilla simple: `plt.subplots(filas, columnas)`

Es la forma más común. Devuelve la `Figure` y un **array** de `Axes` (no un solo `ax`):

```python
fig, axs = plt.subplots(2, 2, figsize=(6, 6))   # grilla de 2x2 = 4 Axes

axs[0, 0].plot(x, y)
axs[0, 0].set_title('arriba-izquierda')

axs[0, 1].scatter(x, y)
axs[1, 0].bar(categorias, valores)
axs[1, 1].hist(datos)

plt.show()
```

`axs` se indexa como una matriz de NumPy: `axs[fila, columna]`.

> [!warning] Con una sola fila o columna, `axs` es un array 1D
> `fig, axs = plt.subplots(1, 3)` te da `axs` como `[ax0, ax1, ax2]` — se indexa `axs[0]`, `axs[1]`, `axs[2]`, **sin** el segundo índice. Es un error común pedir `axs[0, 1]` cuando en realidad solo pediste una fila.

Un patrón muy usado para no pelearte con los índices es **desempaquetar** directamente:

```python
fig, (ax1, ax2) = plt.subplots(1, 2, figsize=(10, 4))
ax1.plot(x, y)
ax2.scatter(x, y)
```

## `figsize` y `layout='constrained'`

- `figsize=(ancho, alto)` — tamaño de la figura **en pulgadas**.
- `layout='constrained'` — le pide a Matplotlib que **reacomode automáticamente** los `Axes` para que los títulos y etiquetas no se pisen ni se corten. Sin esto, es común que las etiquetas de un subplot se superpongan con el título del de al lado.

```python
fig, axs = plt.subplots(2, 2, figsize=(6, 6), layout='constrained')
```

> [!tip] Si tus títulos o labels se ven cortados o pisados, esto es lo primero que hay que probar.

## Layouts más flexibles: `subplot_mosaic`

Cuando necesitás que un panel ocupe más espacio que otro (no una grilla pareja), `subplot_mosaic` arma el layout a partir de un "mapa" visual escrito como lista de listas:

```python
fig, axd = plt.subplot_mosaic([['izquierda', 'arriba_derecha'],
                                ['izquierda', 'abajo_derecha']],
                               layout='constrained')

axd['izquierda'].set_title('izquierda (ocupa las 2 filas)')
axd['arriba_derecha'].set_title('arriba derecha')
axd['abajo_derecha'].set_title('abajo derecha')
```

Cada string del "mapa" es la clave de un diccionario (`axd`), y repetir la misma clave en varias celdas hace que ese `Axes` **ocupe** todas esas celdas. Es más legible que calcular a mano qué `Axes` va en qué posición.

## Un segundo eje Y sobre el mismo gráfico: `twinx()`

Para superponer dos series con **escalas muy distintas** (por ejemplo, temperatura y precio) en el mismo `Axes` visual, pero con dos ejes Y independientes:

```python
fig, ax1 = plt.subplots()
l1, = ax1.plot(t, serie_pequeña)
ax1.set_ylabel('escala 1')

ax2 = ax1.twinx()             # nuevo Axes, comparte el eje X, eje Y propio a la derecha
l2, = ax2.plot(t, serie_grande, color='C1')
ax2.set_ylabel('escala 2')

ax2.legend([l1, l2], ['serie 1 (izq.)', 'serie 2 (der.)'])
```

`twinx()` crea un `Axes` **nuevo** que comparte el eje X con el original pero tiene su propio eje Y a la derecha (`twiny()` es el equivalente para compartir el eje Y y tener un segundo eje X).

## Varias figuras a la vez

Nada te obliga a quedarte con una sola `Figure`. Si mantenés la referencia, podés ir agregando cosas a cualquiera de ellas:

```python
fig1, ax1 = plt.subplots()
fig2, ax2 = plt.subplots()

ax1.plot(x, y)
ax2.scatter(x, y)
```

## Relacionado
- [[02 - Anatomia de una figura]]
- [[03 - Estilos de codigo (OO vs pyplot)]]
- [[08 - Escalas, ticks y guardar figuras]]
