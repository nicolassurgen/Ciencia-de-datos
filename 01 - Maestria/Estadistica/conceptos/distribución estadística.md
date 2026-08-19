---
titulo: Distribución estadística
materia: Estadística
tipo: concepto
tags:
  - estadistica
  - maestria
  - concepto
  - tema/variabilidad
fecha: 2026-08-19
---

# Distribución estadística

Antes de calcular una media, un desvío estándar o dibujar un histograma, hace falta un concepto que los englobe a todos: la idea de que una variable tiene una **distribución** — un patrón de cómo se reparten sus valores. Media, desvío, histograma y percentiles no son cosas distintas entre sí: son formas distintas de **describir** una misma distribución.

> [!definition] Distribución
> Describe **cómo se reparten** los valores de una variable en un conjunto de datos: qué valores aparecen y con qué frecuencia aparece cada uno. Es el concepto paraguas del que se derivan la [[distribución de frecuencias|tabla de frecuencias]], el [[histograma]] y toda medida de resumen.

> [!quote] Definición formal
> "One of the best ways to describe a variable is to report the values that appear in the dataset and how many times each value appears. This description is called the **distribution** of the variable." *Fuente: [[Think Stats – Exploratory Data Analysis in Python]], cap. 2.*

## De los datos en bruto a la distribución

El libro de cátedra no define "distribución" en abstracto antes de la tabla de frecuencias — pasa directo de la [[matriz de datos|planilla de volcado]] (los datos en bruto, fila por unidad) a la [[distribución de frecuencias|tabla de distribución de frecuencias]] (los datos resumidos, valor por valor o intervalo por intervalo). Esa tabla es la representación **más directa** de una distribución: para cada valor posible, cuántas veces se repite.

```
Datos en bruto (matriz de datos)     →     Distribución de frecuencias
[7, 8, 7, 9, 7, 8, 6, 7, ...]              7 → 4 veces
n filas, 1 por unidad                      8 → 2 veces
                                            6 → 1 vez  ...
```

> [!important] El mismo dato, dos sentidos de "distribución"
> Conviene distinguir dos usos del término, que se van a volver a cruzar más adelante en la materia: la **distribución de los datos** (cómo se reparten los valores observados de una variable, el tema de esta nota) y la **distribución muestral** (cómo se repartirían los valores de un *estadístico*, como la media, si se repitiera el muestreo muchas veces — el objeto central de la inferencia). Son dos preguntas distintas sobre "distribución": una describe los datos que ya tenés, la otra describe la incertidumbre de un estimador. *Fuente: [[Think Stats – Exploratory Data Analysis in Python]], cap. 8.*

## Las tres preguntas que describen una distribución

Una vez que se acepta que una variable "tiene una distribución", el trabajo de la estadística descriptiva se organiza en torno a tres preguntas, que forman una tríada — cada una con su propia familia de notas en este vault:

1. **¿Dónde se centra?** → [[medidas de posición]] (media, mediana, moda).
2. **¿Cuánto se dispersa alrededor de ese centro?** → [[medidas de dispersión]] (varianza, desvío estándar, rango intercuartílico).
3. **¿Qué forma tiene?** → [[forma de una distribución]] (simetría, asimetría, colas, modalidad).

Ningún resumen de una distribución está completo si responde solo una de las tres. Reportar únicamente el centro (por ejemplo, "el promedio es 100") sin decir nada de la dispersión puede esconder que la mitad de los datos está entre 90 y 110, o entre 10 y 190 — dos situaciones radicalmente distintas con el mismo centro.

## Representaciones de una distribución

La misma distribución se puede mostrar de formas distintas según el tipo de variable y qué se quiera resaltar — todas son "vistas" del mismo objeto:

- **Tabla** → [[distribución de frecuencias]] ($f_i$, $h_i$, acumuladas).
- **Gráfico**, según el tipo de variable → [[gráfico de barras]] o [[diagrama de Pareto]] (cualitativa), [[diagrama de bastones]] (cuantitativa discreta), [[histograma]] o [[diagrama de tallo y hoja]] (cuantitativa continua).
- **Acumulada** → [[función de distribución acumulada (CDF empírica)]], que responde "¿qué proporción de datos es menor o igual a *x*?" en vez de "¿cuántos datos valen exactamente *x*?".

> [!tip] Distribución vs. serie de tiempo: cuándo cada una tiene sentido
> Construir cualquiera de estas representaciones presupone que tiene sentido "aplastar" el orden en el que se recolectaron los datos y mirarlos solo como un conjunto. Eso solo es válido si el proceso que los generó es **estable** — ver [[estabilidad de un proceso]]. Si no lo es, hay que mirar primero la [[series de tiempo|serie de tiempo]].

> [!note] En código
> `df['columna'].value_counts()` (categórica) o `sns.histplot()` / `sns.kdeplot()` (numérica, ver [[05 - Distribuciones (histplot, kdeplot, ecdfplot)]] de Seaborn) son las formas más directas de ver la distribución de una variable en una línea. `df.describe()` (ver [[01 - Introduccion a Series y DataFrame]] de Pandas) da de una sola vez varias de las medidas de las tres preguntas de arriba.

## Relacionado
- [[02 - El estudio de la variabilidad]]
- [[distribución de frecuencias]]
- [[medidas de posición]] · [[medidas de dispersión]] · [[forma de una distribución]]
- [[variabilidad estadística]]
- [[matriz de datos]]
- [[función de distribución acumulada (CDF empírica)]]
