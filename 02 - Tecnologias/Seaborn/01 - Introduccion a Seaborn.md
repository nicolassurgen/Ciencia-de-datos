---
titulo: Seaborn - Introducción a Seaborn
materia: Seaborn
tipo: apunte
tags:
  - seaborn
  - tecnologias
  - python
  - tema/introduccion
fuente: "seaborn.pydata.org (documentación oficial)"
---

# Introducción a Seaborn

> [!definition] Seaborn
> Una librería de Python para hacer **gráficos estadísticos**. Se construye **sobre** [[01 - Introduccion y primer grafico|Matplotlib]] e integra directamente con [[01 - Introduccion a Series y DataFrame|Pandas]]. La propia documentación lo resume así: *"su API declarativa y orientada a datos te deja enfocarte en qué significan los elementos de tu gráfico, en vez de en los detalles de cómo dibujarlos"*.

## ¿Por qué no alcanza con Matplotlib solo?

Ya viste en las notas de Matplotlib cómo armar un gráfico eligiendo vos, a mano, cada color, cada línea, cada marcador. Eso te da **control total**, pero para las preguntas típicas de un análisis estadístico ("¿cómo se relacionan estas dos variables según el grupo?", "¿cómo es la distribución de esta variable?") terminás escribiendo el mismo código repetitivo una y otra vez.

> [!important] La diferencia de fondo
> Con Matplotlib, vos le decís a la computadora **cómo dibujar** (qué color, qué posición X, qué posición Y). Con Seaborn, vos le decís **qué variables de tu DataFrame representan qué** (`x="total_bill"`, `hue="smoker"`) y Seaborn decide el resto. Es la diferencia entre programar imperativamente y programar declarativamente — la misma distinción que ya viste entre el [[03 - Estilos de codigo (OO vs pyplot)|estilo OO y el estilo pyplot]] de Matplotlib, pero un nivel más arriba.

Seaborn **no reemplaza** a Matplotlib — lo usa por debajo. Por eso todo lo que aprendiste de Matplotlib (`fig`, `ax`, [[02 - Anatomia de una figura|Figure/Axes]], `savefig`) te sigue sirviendo cuando necesitás ajustar un detalle fino que Seaborn no expone directamente.

## Instalación e import

```bash
pip install seaborn
```

```python
import seaborn as sns
import matplotlib.pyplot as plt
```

`sns` es la convención universal (por *Samuel Norman Seaborn*, un personaje de la serie *The West Wing* — la librería se llama así en su honor).

## Datasets de ejemplo

Seaborn trae varios datasets clásicos ya cargados, ideales para practicar:

```python
tips = sns.load_dataset("tips")          # propinas en un restaurante
penguins = sns.load_dataset("penguins")  # el mismo dataset que ya usaste en Algoritmos
titanic = sns.load_dataset("titanic")     # pasajeros del Titanic
```

Cada uno vuelve como un `DataFrame` de Pandas — todo lo que ya sabés de [[01 - Introduccion a Series y DataFrame]] aplica directo.

## El tema visual por defecto

```python
sns.set_theme()
```

Una sola línea que cambia el aspecto de **todos** los gráficos de Matplotlib de la sesión (fondo gris con grilla blanca, paleta de colores prolija) — sin esta línea, Seaborn dibuja igual, pero con el estilo default de Matplotlib. Ver [[09 - Estilo, paletas de color y temas]] para personalizarlo.

## Tu primer gráfico

```python
sns.set_theme()
tips = sns.load_dataset("tips")

sns.relplot(data=tips, x="total_bill", y="tip")
plt.show()
```

Comparalo con lo que hacía falta en Matplotlib puro para un scatter equivalente ([[04 - Tipos de graficos basicos|Tipos de gráficos básicos]]): acá no armaste `fig, ax` a mano, no llamaste `ax.scatter()`, no pusiste labels — Seaborn tomó los nombres de columna (`total_bill`, `tip`) y los usó directo como etiquetas de los ejes.

> [!tip] `data=` primero, siempre
> El patrón `sns.funcion(data=df, x="columna1", y="columna2", ...)` se repite en **todas** las funciones de Seaborn. Acostumbrate a pensar primero "¿cuál es mi DataFrame?" y después "¿qué columnas quiero mapear a qué?" — es la forma de pensar que te va a servir para el resto de estas notas.

## Recorrido de estas notas

1. **Introducción a Seaborn** *(esta nota)*
2. [[02 - Funciones de figura vs funciones de ejes]] — la distinción más importante de toda la librería.
3. [[03 - Forma de los datos (long-form vs wide-form)]] — cómo tiene que estar organizado tu DataFrame.
4. [[04 - Relaciones entre variables (scatterplot, lineplot)]] — comparar dos variables numéricas, con `hue`/`size`/`style`.
5. [[05 - Distribuciones (histplot, kdeplot, ecdfplot)]] — la distribución de una variable, tres formas de verla.
6. [[06 - Variables categoricas (boxplot, violinplot, barplot)]] — comparar una variable numérica entre grupos.
7. [[07 - Regresion y relaciones estadisticas]] — ajustar y visualizar un modelo lineal.
8. [[08 - Grids y comparaciones multiples]] — facetar por variable, matrices de dispersión, correlación.
9. [[09 - Estilo, paletas de color y temas]] — hacer que el gráfico se vea bien y comunique bien.

## Relacionado
- [[01 - Introduccion y primer grafico]]
- [[01 - Introduccion a Series y DataFrame]]
- [[01 - Como dar sentido a los datos]]
