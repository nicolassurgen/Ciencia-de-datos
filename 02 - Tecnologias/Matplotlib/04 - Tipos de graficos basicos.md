---
titulo: Matplotlib - Tipos de gráficos básicos
materia: Matplotlib
tipo: apunte
tags:
  - matplotlib
  - tecnologias
  - python
  - tema/tipos-de-grafico
fuente: "Matplotlib.pdf (documentación oficial, release 3.11.1)"
---

# Tipos de gráficos básicos

Todos estos métodos se llaman igual: `ax.algo(datos)` (ver [[03 - Estilos de codigo (OO vs pyplot)|estilo OO]]). Lo único que cambia es el nombre del método y qué forma de datos espera.

## Línea — `ax.plot()`

El gráfico por defecto de Matplotlib. Ideal para **series continuas** u ordenadas (evolución en el tiempo, una función matemática).

```python
fig, ax = plt.subplots()
x = np.linspace(0, 10, 100)
ax.plot(x, np.sin(x))
plt.show()
```
**Qué genera:** una curva azul continua que sube y baja como una ola entre -1 y 1, cruzando el cero cada π unidades — la onda seno clásica sobre 100 puntos equiespaciados entre 0 y 10.

Con más de una serie, cada llamado a `ax.plot()` agrega una línea nueva al mismo `Axes`:

```python
fig, ax = plt.subplots()
ax.plot(x, np.sin(x), label='seno')
ax.plot(x, np.cos(x), label='coseno')
ax.legend()
```
**Qué genera:** las dos ondas (seno y coseno) superpuestas en los mismos ejes, cada una de un color distinto por defecto, con una leyenda en una esquina identificando cuál es cuál. El coseno arranca en 1 (no en 0, como el seno) y las dos curvas se cruzan periódicamente.

## Dispersión (*scatter*) — `ax.scatter()`

Para ver la **relación entre dos variables numéricas**, punto por punto — el equivalente gráfico de comparar dos columnas de un dataset. Ver [[medidas de posición]] y [[medidas de dispersión]] de Estadística para lo que suele acompañar a este tipo de análisis.

```python
fig, ax = plt.subplots()
ax.scatter(data['a'], data['b'], c=data['c'], s=data['d'])
```
**Qué genera:** una nube de puntos, uno por fila del dataset, ubicado según `a` (eje x) y `b` (eje y) — pero además cada punto tiene un **color** distinto según su valor de `c` (con una escala continua, ver [[09 - Colorbars y mapas de color]]) y un **tamaño** distinto según `d`. Es un scatter codificando 4 variables a la vez: dos en posición, una en color, una en tamaño.

- `c=` → color de cada punto (puede ser una variable, para codificar una tercera dimensión).
- `s=` → tamaño de cada punto (también puede ser una variable).

> [!tip] `plot` con marcador vs `scatter`
> `ax.plot(x, y, 'o')` (sin conectar los puntos) también dibuja una dispersión, y es más rápido para muchísimos puntos. Usá `scatter` cuando necesitás variar color o tamaño punto por punto — si no, `plot(..., 'o')` alcanza y sobra.

## Barras — `ax.bar()` / `ax.barh()`

Para **comparar cantidades entre categorías** (ver [[distribución de frecuencias]] de Estadística: es el gráfico natural para una variable cualitativa).

```python
fig, ax = plt.subplots()
categorias = ['A', 'B', 'C', 'D']
valores = [23, 45, 12, 38]
ax.bar(categorias, valores)        # barras verticales
# ax.barh(categorias, valores)     # barras horizontales
```
**Qué genera:** 4 barras verticales, una por categoría (A, B, C, D), con altura proporcional a `valores` — la más alta es "B" (45), la más baja "C" (12). Con `barh()` sería lo mismo pero horizontal, útil cuando los nombres de categoría son largos y no entran legibles en el eje x.

> [!warning] Cuidado con listas de strings largas
> Si le pasás 1000 strings distintos en el eje X, Matplotlib los va a tratar como 1000 categorías y te va a llenar el gráfico de ticks ilegibles. Esto pasa seguido sin querer al leer un CSV donde una columna numérica quedó cargada como texto.

## Histograma — `ax.hist()`

Para ver la **distribución de una variable cuantitativa** — el mismo concepto que [[histograma]] en Estadística, ahora en código.

```python
fig, ax = plt.subplots()
datos = np.random.randn(1000)
ax.hist(datos, bins=30, density=True, facecolor='C0', alpha=0.75)
ax.set_xlabel('Valor')
ax.set_ylabel('Densidad')
```
**Qué genera:** 30 barras azules semitransparentes pegadas entre sí, con forma de campana centrada en 0 (porque `datos` viene de una normal estándar) — más altas cerca del centro, achicándose hacia los extremos entre aproximadamente -3 y 3.

- `bins=` → cantidad de intervalos (ver [[distribución de frecuencias]] — es la misma decisión que agrupar en intervalos de clase).
- `density=True` → normaliza para que el área total sea 1 (una densidad, no un conteo).
- `alpha=` → transparencia (0 = invisible, 1 = opaco).

## Torta — `ax.pie()`

Muestra la **composición** de un total en categorías. Usar con moderación: un [[diagrama de Pareto|gráfico de barras]] casi siempre comunica mejor que una torta cuando hay más de 3-4 categorías (ver la nota de Estadística sobre gráficos apropiados por tipo de variable).

```python
fig, ax = plt.subplots()
ax.pie(valores, labels=categorias, autopct='%1.1f%%')
```
**Qué genera:** un círculo dividido en 4 porciones (A, B, C, D), cada una ocupando el ángulo proporcional a su valor sobre el total de 118 — "B" es la porción más grande (~38%), "C" la más chica (~10%), con el porcentaje impreso dentro de cada porción.

## Boxplot — `ax.boxplot()`

El [[boxplot|diagrama de caja y bigotes]] de Estadística, calculado y dibujado automáticamente:

```python
fig, ax = plt.subplots()
ax.boxplot(datos)
```
**Qué genera:** una caja centrada cerca de 0 (la mediana de `datos`, la normal estándar de arriba) con bigotes que se extienden hacia ±2 aproximadamente, y algunos puntos sueltos más allá de los bigotes marcando los valores que el criterio 1.5·RIQ considera atípicos.

Matplotlib calcula los cuartiles y detecta atípicos con el mismo criterio 1.5·RIQ que ya conocés.

## Tabla de referencia rápida

| Quiero mostrar... | Método | Tipo de dato de entrada |
|---|---|---|
| Una serie / tendencia | `ax.plot(x, y)` | Numérico ordenado |
| Relación entre 2 variables | `ax.scatter(x, y)` | Numérico |
| Comparar categorías | `ax.bar(cat, val)` | Categórico + numérico |
| Distribución de una variable | `ax.hist(x)` | Numérico |
| Composición de un total | `ax.pie(val)` | Numérico (proporciones) |
| Resumen de 5 números + atípicos | `ax.boxplot(x)` | Numérico |

## Relacionado
- [[01 - Introduccion y primer grafico]]
- [[05 - Personalizacion - color, estilo y marcadores]]
- [[distribución de frecuencias]]
- [[histograma]] · [[boxplot]]
