---
titulo: "Matplotlib - Estilos de código: OO vs pyplot"
materia: Matplotlib
tipo: apunte
tags:
  - matplotlib
  - tecnologias
  - python
  - tema/introduccion
fuente: "Matplotlib.pdf (documentación oficial, release 3.11.1)"
---

# Estilos de código: OO vs pyplot

Si buscás ejemplos de Matplotlib en internet, vas a encontrar código que se ve **distinto** para hacer lo mismo. No es que uno esté mal — Matplotlib tiene, literalmente, dos formas oficiales de escribir el mismo gráfico. Conviene reconocer ambas desde el principio para no confundirse.

## Las dos formas

> [!definition] Estilo orientado a objetos (OO)
> Creás explícitamente la `Figure` y el `Axes`, y llamás **métodos sobre esos objetos**.

```python
x = np.linspace(0, 2, 100)

fig, ax = plt.subplots(figsize=(5, 2.7), layout='constrained')
ax.plot(x, x, label='linear')
ax.plot(x, x**2, label='quadratic')
ax.plot(x, x**3, label='cubic')
ax.set_xlabel('x label')
ax.set_ylabel('y label')
ax.set_title("Simple Plot")
ax.legend()
```
**Qué genera:** tres curvas crecientes desde el origen — la lineal (recta), la cuadrática y la cúbica se separan cada vez más a medida que `x` crece, con una leyenda identificando cuál es cuál.

> [!definition] Estilo pyplot (implícito)
> Nunca creás `ax` a mano: dejás que `pyplot` mantenga una figura y un `Axes` "actuales" por detrás de escena, y llamás **funciones sueltas** del módulo `plt`.

```python
x = np.linspace(0, 2, 100)

plt.figure(figsize=(5, 2.7), layout='constrained')
plt.plot(x, x, label='linear')
plt.plot(x, x**2, label='quadratic')
plt.plot(x, x**3, label='cubic')
plt.xlabel('x label')
plt.ylabel('y label')
plt.title("Simple Plot")
plt.legend()
```

**Ambos bloques producen exactamente el mismo gráfico.** Fijate el patrón: `ax.set_xlabel()` ↔ `plt.xlabel()`, `ax.set_title()` ↔ `plt.title()`, `ax.plot()` ↔ `plt.plot()`. La correspondencia es casi siempre `ax.set_algo()` → `plt.algo()`.

## ¿Cuál usar?

> [!tip] Recomendación de la documentación oficial (y la que conviene seguir como principiante)
> Usá el **estilo OO** como default, especialmente para cualquier cosa que no sea trivial o que vayas a reutilizar (funciones, scripts, notebooks de análisis real). Reservá el estilo `pyplot` para pruebas rápidas de una sola línea en una consola interactiva.

¿Por qué OO y no pyplot, si pyplot es más corto? Porque el estilo pyplot depende de un estado "actual" oculto (la figura y el Axes activos en ese momento). Eso funciona bien en un script lineal, pero se vuelve confuso apenas necesitás **más de un gráfico a la vez** ([[07 - Subplots y multiples ejes]]): con `ax1`, `ax2` explícitos siempre sabés sobre cuál Axes estás actuando; con `plt.algo()` tenés que acordarte cuál está "activo" en ese momento.

> [!warning] Un estilo que NO tenés que usar
> Vas a encontrarte ejemplos viejos con `from pylab import *`. Es un tercer estilo, **desaconsejado hace años** por la propia documentación — importa todo (`numpy` incluido) al espacio de nombres global, lo que genera conflictos de nombres difíciles de rastrear. Si un tutorial lo usa, es una señal de que es antiguo.

## Tabla de equivalencias rápida

| Estilo OO (`ax.`) | Estilo pyplot (`plt.`) |
|---|---|
| `ax.plot(x, y)` | `plt.plot(x, y)` |
| `ax.set_title("...")` | `plt.title("...")` |
| `ax.set_xlabel("...")` | `plt.xlabel("...")` |
| `ax.set_ylabel("...")` | `plt.ylabel("...")` |
| `ax.set_xlim(a, b)` | `plt.xlim(a, b)` |
| `ax.legend()` | `plt.legend()` |
| `ax.grid(True)` | `plt.grid(True)` |

De acá en adelante, en el resto de estas notas vamos a usar **el estilo OO** (`ax.algo()`) como convención — es el que te va a servir mejor a medida que los gráficos se vuelvan más complejos.

## Relacionado
- [[02 - Anatomia de una figura]]
- [[01 - Introduccion y primer grafico]]
- [[07 - Subplots y multiples ejes]]
