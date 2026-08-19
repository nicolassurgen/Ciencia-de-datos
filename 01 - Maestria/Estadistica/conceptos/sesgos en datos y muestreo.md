---
titulo: Sesgos en datos y muestreo
materia: Estadística
tipo: concepto
tags:
  - estadistica
  - maestria
  - concepto
  - tema/introduccion
fecha: 2026-08-19
---

# Sesgos en datos y muestreo

[[sesgo de autoselección]] y [[sesgo de supervivencia]] ya tienen nota propia en este vault, cada uno con su ejemplo clásico. Lo que faltaba era el concepto que los engloba: **qué es un sesgo**, en general, más allá de sus casos particulares — y por qué siguen apareciendo casos nuevos que no encajan en ninguno de los dos ya vistos.

> [!definition] Sesgo (bias)
> "Systematic error." Un error que **no** se cancela promediando más datos, porque empuja sistemáticamente los resultados en la misma dirección — a diferencia del error puramente aleatorio, que sí tiende a compensarse con más observaciones. *Fuente: [[Practical Statistics for Data Scientists]] (Bruce & Bruce), cap. 2.*

> [!important] Por qué "más datos" no alcanza contra el sesgo
> Es la idea que distingue al sesgo del [[error muestral y error no muestral|error muestral]]: el error muestral se reduce agrandando la muestra; el sesgo, no — una muestra sesgada de un millón de casos sigue sesgada. El criterio operativo para detectarlo: hay sesgo cuando la **probabilidad de que una unidad entre a la muestra está relacionada con la variable que se quiere medir**.

## El criterio, con un ejemplo aplicado

> [!example] Las láminas de madera apiladas
> Para medir imperfecciones en láminas de madera apiladas, tomar por comodidad las láminas de **arriba** de la pila produce sesgo **si** la variable de interés (imperfecciones) está relacionada con la posición en la pila (por ejemplo, si las de abajo, más comprimidas, tienen más defectos). Si en cambio se midiera la longitud de las láminas —una variable que no depende de la posición—, tomar solo las de arriba no introduciría ningún sesgo. *Fuente: [[Estadística para la resolución de problemas en Ingeniería]], cap. 7.* El mismo mecanismo de selección puede ser inofensivo para una variable y sesgado para otra — depende de si esa variable está relacionada con el criterio (implícito) de selección.

## Una taxonomía: varios sesgos, con mecanismos distintos

No hay una única forma en que aparece el sesgo — vale la pena tener mapeados los mecanismos más comunes, cada uno con su propia causa:

- **Sesgo de selección** (concepto general) — la muestra no representa a la población porque el mecanismo de selección está relacionado con la variable de interés.
- **[[sesgo de autoselección|Autoselección]]** — quien entra a la muestra lo decide voluntariamente (responder una encuesta, dejar una reseña), y esa decisión está correlacionada con lo que se mide.
- **[[sesgo de supervivencia|Supervivencia]]** — solo se observan las unidades que "sobrevivieron" un proceso de selección; las que no llegaron a observarse son, precisamente, las más informativas.
- **Sesgo del observador / paradoja del tamaño de clase** — cuando la probabilidad de que una unidad aparezca en la muestra es proporcional a su propio tamaño (ver más abajo).
- **Sesgo de confirmación** — no es un problema de quién entra a la muestra, sino de **qué casos se eligen contar**: quien ya cree una afirmación tiende a notar y compartir los que la confirman.
- **Vast search effect** (efecto de búsqueda extensa) — no es un problema del mecanismo de muestreo, sino del análisis: revisar muchas relaciones posibles hasta encontrar una "interesante" (ver más abajo).

> [!quote] La propia bibliografía ya organiza esta taxonomía
> El índice de [[Think Stats – Exploratory Data Analysis in Python]] agrupa, bajo la entrada "bias", exactamente cinco subtipos: *confirmation, observer, oversampling, selection, sampling* — la misma estructura de esta nota, tomada directamente de cómo el propio libro organiza el tema.

## Un mecanismo menos intuitivo: el sesgo del observador

> [!example] La paradoja del tamaño de clase
> Si se les pregunta a estudiantes "¿cuántos alumnos tiene tu clase?" y se promedian las respuestas, el resultado **sobreestima** el tamaño real promedio de las clases — porque cada estudiante de una clase grande "aporta" más respuestas (hay más alumnos ahí para responder) que cada estudiante de una clase chica. En un ejemplo real del libro, el tamaño medio real de las clases era de 23.7 alumnos, pero el tamaño medio *percibido* por los propios estudiantes (por este efecto) daba 29.1 — casi un 25 % más alto, sin que hubiera ningún error de medición ni nadie se hubiera autoseleccionado: el sesgo está en que la probabilidad de que una unidad (un alumno) "aparezca" en el cálculo es proporcional al tamaño del grupo al que pertenece. *Fuente: [[Think Stats – Exploratory Data Analysis in Python]], cap. 3.*

## Un mecanismo del análisis, no de la muestra: el vast search effect

> [!warning] Buscar hasta encontrar algo "interesante"
> "**Vast search effect**: Bias or nonreproducibility resulting from repeated data modeling, or modeling data with large numbers of predictor variables." Y, citando el origen de la idea: *"If you don't know what you're looking for, look hard enough and you'll find it."* *Fuente: [[Practical Statistics for Data Scientists]] (Bruce & Bruce), cap. 2.* A diferencia de los sesgos anteriores (que están en cómo se armó la muestra), este está en cómo se **analizaron** los datos: revisar muchas relaciones posibles entre variables y reportar solo la que "dio algo" produce hallazgos que parecen reales pero son artefactos del propio proceso de búsqueda. Conecta directamente con por qué [[análisis exploratorio vs confirmatorio|explorar y confirmar con el mismo dataset]] es un riesgo, y con el "*data snooping*" que señala [[tratamiento primario]].

## Relacionado
- [[sesgo de autoselección]] · [[sesgo de supervivencia]]
- [[muestreo y diseño muestral]]
- [[error muestral y error no muestral]]
- [[validez externa]]
- [[análisis exploratorio vs confirmatorio]]
- [[01 - Como dar sentido a los datos]]
