---
titulo: "Seaborn - Relaciones entre variables: scatterplot, lineplot"
materia: Seaborn
tipo: apunte
tags:
  - seaborn
  - tecnologias
  - python
  - tema/relaciones
fuente: "seaborn.pydata.org (documentación oficial)"
---

# Relaciones entre variables: scatterplot, lineplot

> [!important] La pregunta estadística detrás de este gráfico
> "¿Cómo se relacionan **dos variables numéricas**?" — el equivalente visual de mirar un coeficiente de correlación. Es el punto de partida casi obligado de cualquier análisis exploratorio con más de una variable cuantitativa (ver [[04 - Agregaciones y estadistica descriptiva|medidas descriptivas de NumPy]] y [[medidas de dispersión]] de Estadística).

## Scatterplot: la relación punto por punto

```python
sns.relplot(data=tips, x="total_bill", y="tip")
```

Cada punto es una observación (una fila del DataFrame, ver [[03 - Forma de los datos (long-form vs wide-form)]]). Es el gráfico natural cuando **ambas** variables son cuantitativas continuas — el mismo caso de uso que [[04 - Tipos de graficos basicos|`ax.scatter()` de Matplotlib]], pero con el mapeo de columnas resuelto automáticamente.

## Lineplot: cuando el orden importa

```python
sns.relplot(data=dowjones, x="Date", y="Price", kind="line")
```

Usalo cuando el eje X tiene un **orden natural** — típicamente tiempo. Es la versión Seaborn de lo que en Estadística llamamos [[series de tiempo]]: **no** tiene sentido tratar esos datos como una nube de puntos sin conexión, porque perdés la información de la trayectoria.

> [!warning] No confundir "se puede ordenar" con "hay que usar lineplot"
> Si X es una variable numérica pero **no** representa una secuencia natural (por ejemplo, `total_bill`), conectar los puntos con una línea no agrega información — al revés, sugiere una continuidad que no existe. Usá `lineplot` cuando el eje X es tiempo o cualquier secuencia ordenada real; `scatterplot` para el resto.

## Mapeos semánticos: agregar más variables sin cambiar de gráfico

Esto es lo que separa a Seaborn de armar el mismo scatter en Matplotlib a mano: podés representar **hasta 3 variables extra** (además de X e Y) cambiando cómo se ve cada punto — sin tocar la estructura del gráfico.

```python
sns.relplot(data=tips, x="total_bill", y="tip", hue="smoker")                          # color por categoría
sns.relplot(data=tips, x="total_bill", y="tip", hue="smoker", style="smoker")          # + forma del marcador
sns.relplot(data=tips, x="total_bill", y="tip", size="size", sizes=(15, 200))          # tamaño del punto
```

| Mapeo | Qué codifica | Sirve mejor para |
|---|---|---|
| `hue` | Color | Variables categóricas (o numéricas, con un gradiente) |
| `style` | Forma del marcador / tipo de línea | Variables categóricas con pocos niveles |
| `size` | Tamaño del punto/grosor de línea | Variables numéricas |

> [!tip] Esto es, en el fondo, [[06 - Agregacion y groupby|estratificar]] visualmente
> Separar por `hue` es la versión gráfica de un `df.groupby('smoker')` ([[06 - Agregacion y groupby|Pandas]]) o de la [[estratificación|estratificación]] que viste en Estadística: en vez de calcular una medida resumen por grupo, dejás que el ojo compare los grupos directamente en el mismo gráfico.

## Relacionado
- [[02 - Funciones de figura vs funciones de ejes]]
- [[03 - Forma de los datos (long-form vs wide-form)]]
- [[series de tiempo]]
- [[07 - Regresion y relaciones estadisticas]]
