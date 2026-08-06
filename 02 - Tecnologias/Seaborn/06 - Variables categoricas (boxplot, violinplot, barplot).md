---
titulo: "Seaborn - Variables categóricas: boxplot, violinplot, barplot"
materia: Seaborn
tipo: apunte
tags:
  - seaborn
  - tecnologias
  - python
  - tema/categoricas
fuente: "seaborn.pydata.org (documentación oficial)"
---

# Variables categóricas: boxplot, violinplot, barplot

> [!important] La pregunta estadística detrás de este gráfico
> "¿Cómo cambia una variable numérica **según el grupo** al que pertenece cada observación?" — comparar el diámetro entre Máquina 1 y Máquina 2, la propina entre días de la semana, la supervivencia entre clases del Titanic. Es la [[estratificación|estratificación]] de Estadística, convertida en el eje X de un gráfico.

Seaborn organiza los gráficos categóricos en **tres familias**, según qué tanto resumen los datos. Todas se acceden con la función de figura `catplot(kind=...)` (ver [[02 - Funciones de figura vs funciones de ejes]]).

## Familia 1 — Dispersión categórica: ver cada observación

> [!definition] `stripplot()` / `swarmplot()`
> Muestran **cada punto individual**, resolviendo el problema de que todos comparten la misma posición X (la categoría). No resumen nada — es la forma más honesta de mostrar los datos crudos.

```python
sns.catplot(data=tips, x="day", y="total_bill")                    # stripplot (default): jitter aleatorio
sns.catplot(data=tips, x="day", y="total_bill", kind="swarm")      # swarmplot: acomoda los puntos para que no se toquen
```

`stripplot` separa los puntos con un poco de ruido aleatorio (*jitter*); `swarmplot` usa un algoritmo que los acomoda para que no se superpongan — más prolijo, pero solo funciona bien con datasets chicos/medianos.

## Familia 2 — Distribución por grupo: resumir la forma

> [!definition] `boxplot()` / `violinplot()` / `boxenplot()`
> Resumen la **distribución completa** de cada grupo, no solo un punto.

```python
sns.catplot(data=tips, x="day", y="total_bill", kind="box")       # los 5 números + atípicos, ver [[boxplot]]
sns.catplot(data=tips, x="day", y="total_bill", kind="violin")    # boxplot + forma de la densidad (KDE)
```

`boxplot` es exactamente el [[boxplot|diagrama de caja y bigotes]] que ya conocés de Estadística: cuartiles, mediana, y atípicos con el criterio 1.5·RIQ. `violinplot` agrega la **forma** de la distribución (como un [[05 - Distribuciones (histplot, kdeplot, ecdfplot)|kdeplot]] rotado a cada lado del boxplot) — útil cuando sospechás que un grupo es bimodal, algo que un boxplot por sí solo puede ocultar. `boxenplot` es una variante pensada para datasets grandes, con más detalle en las colas.

## Familia 3 — Estimaciones puntuales: resumir a un solo número

> [!definition] `barplot()` / `pointplot()` / `countplot()`
> Colapsan cada grupo a **un valor** (por defecto, la media) con una barra de error o intervalo de confianza.

```python
sns.catplot(data=titanic, x="sex", y="survived", hue="class", kind="bar")     # media + IC bootstrap
sns.catplot(data=titanic, x="sex", y="survived", hue="class", kind="point")   # lo mismo, pero como puntos conectados
sns.catplot(data=titanic, x="deck", kind="count")                              # frecuencia absoluta por categoría
```

> [!warning] `barplot` no es un histograma de conteos
> Es un error común de principiante confundirlos. `barplot(y="variable_numerica")` grafica la **media** (u otro estimador) de una variable numérica por grupo, con un intervalo de confianza. `countplot()` (sin `y`) grafica **cuántas filas** hay en cada categoría — es la [[distribución de frecuencias|frecuencia absoluta]] de una variable cualitativa. Si lo que querés es "cuántos casos hay de cada tipo", es `countplot`, no `barplot`.

`pointplot` es especialmente bueno para ver **interacciones**: cuando las líneas que conectan los puntos de distintos `hue` no son paralelas, es una señal visual de que el efecto de una variable depende del nivel de la otra.

## Cuál elegir, según cuánto querés mostrar

| Necesitás... | Familia |
|---|---|
| Ver todos los datos crudos, sin resumir nada | `stripplot` / `swarmplot` |
| Comparar mediana, dispersión y atípicos entre grupos | `boxplot` |
| Comparar la forma completa de la distribución (¿es bimodal?) | `violinplot` |
| Comunicar una comparación simple con incertidumbre | `barplot` / `pointplot` |
| Contar frecuencias de una variable cualitativa | `countplot` |

> [!tip] Combinar capas
> Como todas son funciones de ejes que también existen en versión figura, es común superponer un `stripplot` (los datos crudos) sobre un `boxplot` (el resumen) en el mismo `Axes`, para no perder ni el detalle ni el resumen.

## Relacionado
- [[boxplot]]
- [[medidas de posición]]
- [[medidas de dispersión]]
- [[estratificación]]
- [[distribución de frecuencias]]
