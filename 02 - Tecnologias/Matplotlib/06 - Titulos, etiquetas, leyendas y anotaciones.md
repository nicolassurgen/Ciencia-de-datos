---
titulo: "Matplotlib - Títulos, etiquetas, leyendas y anotaciones"
materia: Matplotlib
tipo: apunte
tags:
  - matplotlib
  - tecnologias
  - python
  - tema/personalizacion
fuente: "Matplotlib.pdf (documentación oficial, release 3.11.1)"
---

# Títulos, etiquetas, leyendas y anotaciones

Un gráfico sin título ni etiquetas de ejes no le sirve a nadie más que a vos, y a los dos días tampoco a vos. Estos son los métodos que lo hacen legible — ver [[02 - Anatomia de una figura]] para ubicar cada uno dentro de la figura.

## Título y etiquetas de los ejes

```python
fig, ax = plt.subplots()
ax.plot(x, y)
ax.set_title("Título del gráfico")
ax.set_xlabel("x label")
ax.set_ylabel("y label")
```
**Qué genera:** el mismo gráfico de línea de siempre, pero ahora con un título centrado arriba y nombres en los ejes X e Y — la diferencia entre un gráfico que solo vos entendés y uno que se explica solo.

Los tres métodos devuelven un objeto `Text`, así que se pueden personalizar con los mismos parámetros que cualquier texto:

```python
ax.set_xlabel('mis datos', fontsize=14, color='red')
```

## Texto libre dentro del gráfico

`ax.text(x, y, "mensaje")` escribe texto en una posición **arbitraria** dentro del área de datos (a diferencia de `set_title`/`set_xlabel`, que van en posiciones fijas):

```python
fig, ax = plt.subplots()
n, bins, patches = ax.hist(x, 50, density=True, facecolor='C0', alpha=0.75)
ax.set_xlabel('Longitud [cm]')
ax.set_ylabel('Probabilidad')
ax.set_title('Longitud de hormigueros\n(no realmente)')
ax.text(75, .025, r'$\mu=115,\ \sigma=15$')
ax.grid(True)
```

Fijate el `\n` en el título — funciona igual que en cualquier string de Python, para partir el texto en dos líneas.

## Expresiones matemáticas (LaTeX liviano)

Matplotlib entiende expresiones tipo LaTeX en cualquier texto, si las escribís entre signos `$`:

```python
ax.set_title(r'$\sigma_i=15$')
```

> [!important] La `r` antes de las comillas no es un detalle menor
> `r'...'` es un **raw string** de Python: le dice al intérprete que **no** trate las barras invertidas (`\`) como caracteres de escape. Como las expresiones matemáticas de Matplotlib usan `\` todo el tiempo (`\sigma`, `\mu`, `\frac{}{}`...), si te olvidás la `r` vas a tener errores raros o símbolos que no se ven. Poné `r` **siempre** que el string tenga una fórmula.

## Anotaciones (flecha + texto apuntando a un punto)

Para señalar un punto específico del gráfico con una flecha:

```python
fig, ax = plt.subplots()
t = np.arange(0.0, 5.0, 0.01)
s = np.cos(2 * np.pi * t)
ax.plot(t, s, lw=2)

ax.annotate('máximo local', xy=(2, 1), xytext=(3, 1.5),
            arrowprops=dict(facecolor='black', shrink=0.05))
ax.set_ylim(-2, 2)
```
**Qué genera:** la curva de coseno de siempre, con una flecha negra que sale del texto "máximo local" (ubicado más arriba y a la derecha) y apunta exactamente al pico de la curva en `x=2` — el patrón clásico para señalar un punto de interés sin que el texto tape la curva.

- `xy=` → el punto exacto al que apunta la flecha (en coordenadas de datos).
- `xytext=` → dónde va el texto.
- `arrowprops=` → un diccionario con las propiedades de la flecha (sin este argumento, no se dibuja ninguna flecha, solo el texto).

## Leyenda

Cuando graficás más de una serie, `label=` + `ax.legend()` es lo que arma la leyenda:

```python
fig, ax = plt.subplots()
ax.plot(x, datos1, label='serie 1')
ax.plot(x, datos2, label='serie 2')
ax.legend()
```
**Qué genera:** dos líneas de colores distintos y, superpuesto sobre el gráfico (por defecto en la esquina que menos tapa a los datos), un recuadro con los nombres "serie 1" y "serie 2" junto a una muestra del color/estilo de cada línea.

> [!tip] Si algún `ax.plot()` no lleva `label=`, no aparece en la leyenda
> Es una forma útil de "ocultar" a propósito una serie auxiliar (por ejemplo, una línea de referencia) de la leyenda: simplemente no le pongas `label`.

`ax.legend()` acepta parámetros para controlar la ubicación:

```python
ax.legend(loc='upper right')   # también: 'lower left', 'best', etc.
```

`loc='best'` (el default) hace que Matplotlib elija automáticamente el lugar que menos tape los datos.

## Relacionado
- [[02 - Anatomia de una figura]]
- [[05 - Personalizacion - color, estilo y marcadores]]
- [[04 - Tipos de graficos basicos]]
