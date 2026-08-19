---
titulo: Muestreo y diseño muestral
materia: Estadística
tipo: concepto
tags:
  - estadistica
  - maestria
  - concepto
  - tema/introduccion
fecha: 2026-08-19
---

# Muestreo y diseño muestral

[[población y muestra]] explica **qué** son una población y una muestra. Esta nota responde la pregunta siguiente, distinta: dado que se va a trabajar con una muestra y no con la población completa, **¿cómo se la obtiene** para que sea representativa?

> [!definition] Muestreo
> El **método** con el que se seleccionan las unidades que van a formar parte de la muestra. La elección del método no es un detalle técnico menor: de ella depende directamente si las conclusiones obtenidas sobre la muestra pueden extenderse a la población — ver [[validez externa]].

## Muestreo probabilístico vs. no probabilístico

> [!important] La diferencia que más importa
> En un muestreo **probabilístico**, cada unidad de la población tiene una probabilidad **conocida** (y mayor que cero) de ser seleccionada. En un muestreo **no probabilístico** (muestras "por conveniencia"), la selección depende de qué unidades son fáciles de conseguir, y esa facilidad puede estar relacionada con la variable de interés — lo que produce **sesgo de selección**. Ver [[sesgos en datos y muestreo]].

Solo el muestreo probabilístico permite, más adelante, cuantificar el margen de error de una estimación con las herramientas de la inferencia estadística.

## El muestreo aleatorio simple (M.A.S.)

Es el diseño de referencia, y el único que este curso desarrolla en profundidad:

> [!definition] Muestreo aleatorio simple
> "Un muestreo probabilístico es aquel que asigna a cada unidad elemental de la población una cierta probabilidad de ser seleccionada en la muestra [...] el muestreo aleatorio simple [...] refiere a que todas las muestras posibles de $n$ unidades tienen la misma probabilidad de ser seleccionadas." *Fuente: [[Estadística para la resolución de problemas en Ingeniería]], cap. 7.*

Formalmente, el M.A.S. se modela como un vector de variables aleatorias independientes e idénticamente distribuidas — cada unidad seleccionada es, en un sentido preciso, una "copia" con la misma distribución que la población de origen.

> [!tip] Chequeo práctico: mirar el gráfico contra el orden de selección
> Si la muestra es realmente aleatoria simple, el gráfico de los datos contra el orden en el que se seleccionaron no debería mostrar ningún patrón — cualquier tendencia, ciclo o agrupamiento visible en ese gráfico es una señal de que el mecanismo de selección no fue tan aleatorio como se suponía. Es la misma idea de [[series de tiempo|graficar contra el tiempo primero]], aplicada acá como control de calidad del propio muestreo. *Fuente: [[Estadística para la resolución de problemas en Ingeniería]], cap. 2.*

## Otros diseños muestrales

El libro de cátedra los nombra pero no los desarrolla en profundidad — quedan mencionados acá para tener el mapa completo, y se retoman con más detalle si la materia los formaliza más adelante:

- **Sistemático** — se elige una unidad al azar dentro de las primeras $k$, y luego cada $k$-ésima unidad siguiente (por ejemplo, cada 10º cliente que entra a un local).
- **Estratificado** — se divide la población en subgrupos homogéneos internamente ("estratos", según una variable relevante) y se muestrea dentro de cada uno por separado, para garantizar representación de todos. Es el mismo principio de [[estratificación]] aplicado **al diseño de la muestra** en vez de al análisis posterior de datos ya recolectados.
- **Por conglomerados** — se muestrean grupos completos preexistentes (por ejemplo, escuelas enteras en vez de alumnos individuales) en lugar de unidades sueltas — útil cuando no existe un listado completo de todas las unidades individuales, pero sí de los grupos.
- **Multietápico** — combina varios de los anteriores en etapas sucesivas (por ejemplo, sortear provincias, luego localidades dentro de cada provincia, luego hogares dentro de cada localidad).

> [!quote] Practical Statistics for Data Scientists
> "**Stratified sampling**: Dividing the population into strata and randomly sampling from each strata." *Fuente: [[Practical Statistics for Data Scientists]] (Bruce & Bruce), cap. 2.*

## Representatividad

> [!definition] Muestra representativa
> "In general, cross-sectional studies are meant to be representative, which means that every member of the target population has an equal chance of participating." *Fuente: [[Think Stats – Exploratory Data Analysis in Python]], cap. 1.*

Que una muestra sea grande **no** la hace representativa — el tamaño y la representatividad son dos propiedades independientes.

> [!important] Más muestra no arregla una muestra mal seleccionada
> El caso histórico de la encuesta de *Literary Digest* de 1936 (más de 10 millones de respuestas, mal seleccionadas, frente a las 2.000 bien seleccionadas de Gallup) es la demostración clásica de esto — desarrollado en detalle en [[sesgo de autoselección]]. Y en la era de "big data", la tentación de creer que un dataset enorme resuelve el problema de representatividad sigue vigente: *"Size versus Quality: When Does Size Matter?"*, sección dedicada exactamente a este punto en [[Practical Statistics for Data Scientists]] (Bruce & Bruce), cap. 2 — salvo en casos de datos muy dispersos (raros eventos sobre poblaciones enormes), el muestreo aleatorio bien hecho sigue siendo más valioso que el volumen bruto de datos.

## Muestreo no proporcional deliberado: oversampling

No toda desviación de "cada unidad con igual probabilidad" es un error — a veces es una decisión de diseño **a propósito**.

> [!example] La encuesta NSFG
> La NSFG (encuesta usada como caso de estudio en [[Think Stats – Exploratory Data Analysis in Python]]) sobremuestrea deliberadamente a tres grupos —hispanos, afroamericanos y adolescentes— con una probabilidad de selección **mayor** a su proporción real en la población, para asegurar que cada grupo tenga suficientes casos como para sacar conclusiones estadísticamente válidas *sobre ese grupo en particular*. El costo de esta decisión es que la muestra, tal cual, ya **no** es representativa de la población general — para usarla con ese fin hace falta **ponderar** cada respuesta según la probabilidad inversa con la que fue seleccionada, devolviéndole a cada grupo su peso real en la población.

## Relacionado
- [[población y muestra]]
- [[sesgos en datos y muestreo]] · [[sesgo de autoselección]]
- [[validez externa]]
- [[estratificación]]
- [[error muestral y error no muestral]]
- [[01 - Como dar sentido a los datos]]
