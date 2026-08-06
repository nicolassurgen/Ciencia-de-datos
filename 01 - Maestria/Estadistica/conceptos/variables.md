---
titulo: Variables y tipos de variable
materia: Estadística
tipo: concepto
tags:
  - estadistica
  - maestria
  - concepto
  - tema/introduccion
fecha: 2026-08-03
---

# Variables y tipos de variable

> [!definition] Variable
> Cualquier **característica** que puede asumir **diferentes valores** en las unidades elementales de una [[población y muestra|población o muestra]].

> [!note] ¿Por qué clasificar las variables?
> Las herramientas de análisis que se pueden aplicar dependen, entre otras cosas, del **tipo de variable** y de la [[escalas de medición|escala]] con que se mida. Por eso conviene definirlo con claridad desde el principio, antes de recolectar nada.

## Cualitativas vs. cuantitativas

- **Cualitativas** → sus "valores" son en realidad **categorías o niveles**, aunque se codifiquen con números. (Que codifiques "Sí = 1 / No = 0" no las vuelve numéricas.)
	- *Ejemplos:* máximo nivel educativo, material de construcción de una vivienda, presencia de un síntoma, opinión sobre una ley.
- **Cuantitativas** → sus valores son **numéricos** (tiene sentido operar con ellos: sumar, promediar).

## Dentro de las cuantitativas: discretas vs. continuas

- **Discretas** → sus valores se asocian a los números **enteros**, casi siempre naturales y el 0, porque surgen de **contar**.
	- *Ejemplos:* nº de integrantes de una familia, nº de habitaciones de una vivienda, nº de imperfecciones de un rollo de alambre.
- **Continuas** → sus valores se asocian a los números **reales** y generalmente surgen de una **medición**.
	- *Ejemplos:* ingreso familiar, peso de un componente, diámetro de tubos, nivel de colesterol en sangre.

> [!tip] Regla mnemotécnica
> **Cuento → discreta. Mido → continua.**

## Mapa de la clasificación

![[Clasificacion de variables.png]]

## Variables y escalas

La clasificación cualitativa/cuantitativa (y discreta/continua) no es lo mismo que la [[escalas de medición|escala de medición]] (nominal, ordinal, intervalo, razón), aunque están asociadas: las cualitativas se miden típicamente en escala nominal u ordinal, y las cuantitativas en escala de intervalo o razón. Ambas clasificaciones **en conjunto** determinan qué gráficos y qué medidas de resumen tienen sentido para una variable dada — ver [[medidas de posición]] y [[distribución de frecuencias]].

## Puente con programación

En Python, los tipos primitivos se corresponden directo con estos tipos de variable: `int`/`float` → cuantitativas (discreta/continua), `str` → cualitativas, `bool` → binarias, `None` → datos faltantes. Ver [[tipos primitivos en Python]] (Algoritmos).

En un DataFrame de Pandas, `df.dtypes` muestra esta clasificación columna por columna (`int64`/`float64` → cuantitativa, `object`/`category` → cualitativa) — ver [[01 - Introduccion a Series y DataFrame]]. Y es exactamente lo que decide qué gráfico de Seaborn corresponde: cuantitativa → [[05 - Distribuciones (histplot, kdeplot, ecdfplot)]], cualitativa → [[06 - Variables categoricas (boxplot, violinplot, barplot)]].

## Relacionado
- [[01 - Como dar sentido a los datos]]
- [[escalas de medición]]
- [[medidas de posición]]
- [[distribución de frecuencias]]
- [[tipos primitivos en Python]]
- [[01 - Introduccion a Series y DataFrame]]
- [[05 - Distribuciones (histplot, kdeplot, ecdfplot)]]
- [[06 - Variables categoricas (boxplot, violinplot, barplot)]]
