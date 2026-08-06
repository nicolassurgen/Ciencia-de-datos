---
titulo: "Matplotlib - Personalización: color, estilo y marcadores"
materia: Matplotlib
tipo: apunte
tags:
  - matplotlib
  - tecnologias
  - python
  - tema/personalizacion
fuente: "Matplotlib.pdf (documentación oficial, release 3.11.1)"
---

# Personalización: color, estilo y marcadores

Casi todos los métodos de gráfico (`plot`, `scatter`, `bar`, `hist`...) aceptan los mismos parámetros de estilo. Aprendértelos una vez te sirve para todos.

## Color

Se pasa con el argumento `color` (en `scatter`, además, existen `facecolor`/`edgecolor` para separar el relleno del borde):

```python
fig, ax = plt.subplots()
ax.plot(x, y, color='blue')
ax.scatter(x2, y2, facecolor='C0', edgecolor='k')
```

> [!note] Formas válidas de especificar un color
> - Nombre: `'blue'`, `'red'`, `'black'`...
> - Código corto: `'b'`, `'r'`, `'k'` (negro), `'g'`, `'c'`, `'m'`, `'y'`, `'w'`.
> - Ciclo por defecto: `'C0'`, `'C1'`, `'C2'`... — los colores que Matplotlib usa automáticamente cuando no especificás ninguno (así es como cada `ax.plot()` sucesivo sale de un color distinto sin que hagas nada).
> - Hexadecimal: `'#1f77b4'`.
> - Escala de grises: un string con un número entre `'0'` (negro) y `'1'` (blanco), ej. `'0.75'`.

## Grosor y estilo de línea

```python
ax.plot(x, y, color='blue', linewidth=3, linestyle='--')
```

| `linestyle` | Resultado |
|---|---|
| `'-'` (default) | ─────── |
| `'--'` | ╌╌╌╌╌╌╌ |
| `'-.'` | ─·─·─·─ |
| `':'` | ········ |

`linewidth` se mide en puntos tipográficos (1 pt = 1/72 pulgada). También podés cambiar el estilo **después** de crear la línea:

```python
linea, = ax.plot(x, y)   # ojo la coma: plot() devuelve una LISTA de líneas
linea.set_linestyle(':')
```

> [!note] ¿Por qué `linea, = ax.plot(...)` y no `linea = ax.plot(...)`?
> `ax.plot()` siempre devuelve una **lista** de objetos `Line2D` (puede dibujar más de una línea de una sola llamada si le pasás varias columnas). La coma después de `linea` es *desempaquetado* — como el que ya conocés de tuplas en Python (ver [[listas, tuplas, diccionarios y conjuntos]] de Algoritmos) — y te da directamente el primer (y único) elemento en vez de la lista completa.

## Marcadores

Para resaltar cada punto de dato individual, no solo la línea que los conecta:

```python
ax.plot(x, y, marker='o')          # línea + círculos en cada punto
ax.plot(x, y, 'o')                 # solo los marcadores, sin línea
```

| `marker` | Forma |
|---|---|
| `'o'` | círculo |
| `'s'` | cuadrado |
| `'^'` | triángulo |
| `'d'` | rombo |
| `'x'` | cruz |
| `'v'` | triángulo invertido |

En `scatter`, el tamaño del marcador se controla con `s=` (proporcional al **área** del punto); en `plot`, con `markersize=` (proporcional al **diámetro**).

## El atajo de formato: string de estilo abreviado

Matplotlib permite combinar color + marcador + línea en un solo string corto — lo vas a ver todo el tiempo en ejemplos:

```python
ax.plot(x, y, 'ro--')   # rojo, marcador circular, línea punteada
```

Es cómodo para probar rápido, pero para código que otra persona (o vos mismo en tres meses) va a tener que leer, es más claro usar los argumentos explícitos (`color=`, `marker=`, `linestyle=`).

## Transparencia

```python
ax.hist(datos, alpha=0.75)
```

`alpha` va de `0` (totalmente transparente) a `1` (opaco). Muy útil cuando superponés varias series y necesitás ver dónde se solapan.

## Un atajo para todo el gráfico: `plt.style.use()`

Si lo que buscás es un cambio de "look" completo sin tocar cada gráfico línea por línea, Matplotlib trae temas predefinidos:

```python
plt.style.use('ggplot')      # imita el estilo de ggplot2 (R)
fig, ax = plt.subplots()
ax.plot(x, y)
```

Otros estilos comunes: `'seaborn-v0_8'`, `'bmh'`, `'dark_background'`, `'fivethirtyeight'`. Para ver todos los disponibles: `plt.style.available`.

> [!tip] `plt.style.use()` afecta a **todos** los gráficos que crees después de esa línea, en toda la sesión. Si solo querés cambiar un gráfico puntual, usá los parámetros explícitos (`color=`, `linestyle=`, etc.) en vez de un style sheet global.

## Relacionado
- [[04 - Tipos de graficos basicos]]
- [[06 - Titulos, etiquetas, leyendas y anotaciones]]
- [[listas, tuplas, diccionarios y conjuntos]]
