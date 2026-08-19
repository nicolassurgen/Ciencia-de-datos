---
titulo: Matriz de datos
materia: Estadística
tipo: concepto
tags:
  - estadistica
  - maestria
  - concepto
  - tema/introduccion
fecha: 2026-08-19
---

# Matriz de datos

Sea cual sea el fenómeno que se estudia —piezas, pacientes, encuestados, embarazos—, terminada la recolección los datos casi siempre terminan en la misma forma: una tabla rectangular, con una fila por unidad y una columna por variable. Esa estructura, aparentemente simple, es el punto de encuentro entre tres cosas que hasta ahora vivían en materias separadas: la estadística, el álgebra lineal y Pandas.

> [!definition] Matriz de datos
> Estructura rectangular donde **cada fila** contiene la información de un individuo (unidad elemental) y **cada columna** contiene los valores de una variable. Es el resultado de la etapa de recolección del [[el ciclo estadístico (PPDAC)|ciclo PPDAC]], y el punto de partida de la etapa de análisis. En el libro de cátedra se la llama **planilla de volcado**.

> [!quote] La definición del libro de cátedra
> "En la primera columna de la planilla de volcado se ubican los individuos o unidades elementales analizadas. Cada fila contiene información de un individuo, de modo que la cantidad de filas coincide con el tamaño de la población (N) o de la muestra (n) [...] En las columnas restantes se ubican los valores de las variables estudiadas. El número de variables consideradas en el estudio se simboliza con $p$, y cada una de ellas se corresponde con una columna." *Fuente: [[Estadística para la resolución de problemas en Ingeniería]], cap. 1.*

$$
\begin{pmatrix}
x_{1} & y_{1} & \cdots & z_{1} \\
x_{2} & y_{2} & \cdots & z_{2} \\
\vdots & \vdots & \ddots & \vdots \\
x_{n} & y_{n} & \cdots & z_{n}
\end{pmatrix}
\begin{matrix} n \text{ filas} \\ \text{(individuos)} \end{matrix}
\qquad
\underbrace{\phantom{x_1\; y_1\; \cdots\; z_1}}_{p \text{ columnas (variables)}}
$$

## El mismo objeto, con otro nombre, en ciencia de datos

> [!quote] Rectangular data
> "Rectangular data is essentially a two-dimensional matrix with rows indicating records (cases) and columns indicating features (variables) [...] The doesn't always start in this form: unstructured data (e.g., text) must be processed and manipulated so that it can be represented as a set of features in the rectangular data." *Fuente: [[Practical Statistics for Data Scientists]] (Bruce & Bruce), cap. 1.*

Vale la pena notar que la terminología cambia según la disciplina, aunque el objeto sea el mismo:

> [!tip] Un mismo concepto, tres vocabularios
> "For a statistician, predictor variables are used in a model to predict a response or dependent variable. For a data scientist, features are used to predict a target. One synonym is particularly confusing: computer scientists will use the term sample for a single row; a sample to a statistician means a collection of rows." *Fuente: [[Practical Statistics for Data Scientists]] (Bruce & Bruce), cap. 1.* Estadística clásica: individuo/unidad → fila, variable → columna. Ciencia de datos: *record*/*case* → fila, *feature* → columna. Al pasar de un libro a otro, o de esta materia a Algoritmos o Python, conviene tener presente que "muestra" para un estadístico es un conjunto de filas, y para alguien de programación puede referirse a **una sola** fila — la palabra cambia de significado según quién la usa.

## Tres puentes en uno

Esta nota conecta tres representaciones del mismo objeto, cada una desarrollada en su propia materia:

- **Estadística** (esta nota) → matriz de datos / planilla de volcado, filas = individuos, columnas = variables.
- **Álgebra lineal** → la misma estructura rectangular es, formalmente, una [[02 - Matrices|matriz]]. Las operaciones de álgebra lineal (transposición, multiplicación, la [[02 - Matrices#Matriz de covarianza|matriz de covarianza]] entre variables) se aplican directamente sobre una matriz de datos.
- **Python (Pandas)** → en código, es un `DataFrame`.

> [!note] En código
> `pd.DataFrame(...)` (ver [[01 - Introduccion a Series y DataFrame]]) es la materialización directa de la matriz de datos: `df.shape` da $(n, p)$ — filas y columnas —, `df.index` identifica a cada individuo, `df.columns` a cada variable. Un ejemplo real con dimensiones concretas: la encuesta NSFG usada en [[Think Stats – Exploratory Data Analysis in Python]] arma un `DataFrame` de 13.593 filas (una por embarazo registrado) × 244 columnas (una por variable relevada) — *"the shape of the DataFrame, which is 13593 rows/records and 244 columns/variables"* (cap. 1).

## No todos los datos empiezan siendo rectangulares

Vale la pena tener presente que la matriz de datos es el **resultado** de un proceso de estructuración, no siempre el punto de partida:

> [!warning] Datos no rectangulares
> Texto libre, imágenes, datos de grafos/redes (ver [[grafos y recorridos (DFS, BFS)]] de Algoritmos) o series temporales de alta frecuencia no llegan naturalmente en forma de tabla — hay que procesarlos y extraer variables (*features*) antes de que encajen en una matriz de datos. Gran parte del trabajo previo al análisis, en la práctica, consiste exactamente en esa transformación. *Fuente: [[Practical Statistics for Data Scientists]] (Bruce & Bruce), cap. 1.*

## Relacionado
- [[01 - Como dar sentido a los datos]]
- [[02 - Matrices]]
- [[01 - Introduccion a Series y DataFrame]]
- [[trazabilidad de datos]]
- [[tratamiento primario]]
- [[variables]]
