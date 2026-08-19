---
titulo: Error muestral y error no muestral
materia: Estadística
tipo: concepto
tags:
  - estadistica
  - maestria
  - concepto
  - tema/introduccion
fecha: 2026-08-19
---

# Error muestral y error no muestral

Una conclusión basada en una muestra casi nunca coincide exactamente con la realidad de la población. Pero no todas las causas de esa diferencia son iguales — y confundirlas lleva a un error de diagnóstico grave: aplicar una fórmula de inferencia (pensada para un tipo de error) a un problema que en realidad es del otro tipo, que ninguna fórmula puede arreglar.

> [!definition] Error muestral (propio del muestreo)
> "Errores propios del muestreo": el error que aparece simplemente porque se trabaja con una **parte** de la población y no con su totalidad. Es inevitable en cualquier estudio por muestreo, pero tiene una propiedad clave: sus **riesgos están controlados** — se puede cuantificar con las herramientas de la inferencia estadística. *Fuente: [[Estadística para la resolución de problemas en Ingeniería]], cap. 1.*

> [!definition] Error no muestral (ajeno al muestreo)
> "Errores ajenos al muestreo": errores que se presentan **tanto en estudios poblacionales como en muestrales** — un dato mal tomado, una variable mal medida o mal registrada, un cálculo mal hecho. A diferencia del error muestral, **no se pueden cuantificar sus riesgos** con una fórmula; se previenen trabajando con cuidado en todas las etapas del [[el ciclo estadístico (PPDAC)|ciclo PPDAC]]. *Fuente: [[Estadística para la resolución de problemas en Ingeniería]], cap. 1.*

> [!important] La distinción que importa: ¿lo arregla una fórmula o no?
> Es la pregunta que separa a los dos tipos de error, y por eso es un concepto que va a reaparecer constantemente en la materia: ante cualquier resultado sorprendente o cualquier margen de error reportado, conviene preguntarse primero si la fuente del error es **muestral** (en cuyo caso, más datos o un mejor diseño muestral lo reducen, y la inferencia lo cuantifica) o **no muestral** (en cuyo caso ninguna cantidad de datos adicionales ni ninguna fórmula estadística lo va a corregir — solo un mejor procedimiento de medición y registro).

## La misma distinción, con más detalle: tres fuentes de error

[[Think Stats – Exploratory Data Analysis in Python]] desarrolla esta misma idea con tres términos que conviene tener bien diferenciados:

> [!quote] Tres fuentes de error, resumidas
> "Sampling bias is caused by non-representative sampling, measurement error is caused by errors in collecting and recording data, and sampling error is the result of measuring a sample rather than the entire population." *Fuente: [[Think Stats – Exploratory Data Analysis in Python]], cap. 9.*

- **Sampling error (error muestral)** — la variación de una estimación causada únicamente por trabajar con una muestra en vez de con toda la población. Es el error que **sí** cuantifican los intervalos de confianza y el error estándar.
- **Sampling bias (sesgo de muestreo)** — el mecanismo de selección de la muestra no fue representativo (ver [[sesgos en datos y muestreo]] y [[muestreo y diseño muestral]]). No se arregla con más muestra: hay que rediseñar cómo se selecciona.
- **Measurement error (error de medición)** — el instrumento o el procedimiento de registro es inexacto (por ejemplo, la gente reporta mal su propio peso al ser encuestada por teléfono en lugar de ser pesada directamente). Tampoco lo arregla la inferencia: hay que mejorar cómo se mide.

Las dos últimas son, exactamente, las dos grandes familias de lo que el libro de cátedra llama en conjunto "error ajeno al muestreo" — el libro las agrupa, Think Stats las separa con nombre propio cada una.

> [!warning] Error estándar no es lo mismo que desvío estándar
> Una confusión frecuente que vale la pena aclarar acá: el **desvío estándar** describe la variabilidad **de los datos** (cuánto varían las mediciones individuales); el **error estándar** describe la variabilidad **de una estimación** (cuánto variaría el promedio muestral si se repitiera el muestreo muchas veces). Y ninguno de los dos, por sí solo, "ve" el sesgo de muestreo o el error de medición — ambos asumen implícitamente que esas otras dos fuentes de error no están presentes. *Fuente: [[Think Stats – Exploratory Data Analysis in Python]], cap. 8.*

## Un caso particular de error no muestral: el error en las mediciones

Al medir cualquier magnitud física, el error observado se descompone a su vez en dos partes:

> [!quote] Error sistemático y error aleatorio
> "En el resultado de cada medición pueden estar presentes el error sistemático (o sesgo) y el error aleatorio." *Fuente: [[Estadística para la resolución de problemas en Ingeniería]], cap. 3.*

El error sistemático de un instrumento es exactamente lo que mide la falta de [[exactitud y precisión|exactitud]]; su error aleatorio, la falta de precisión. Es un caso particular y muy concreto de error no muestral — nada tiene que ver con el tamaño de la muestra que se tome.

> [!note] En código
> El error estándar de una media (`np.std(x, ddof=1) / np.sqrt(n)`) y los intervalos de confianza (`scipy.stats`, ver [[06 - Tests de hipotesis - una y dos muestras]]) cuantifican **solo** el error muestral. Ningún cálculo de Python detecta por sí solo un error de medición o un sesgo de muestreo — eso requiere revisar el diseño del estudio y el [[tratamiento primario|tratamiento primario de los datos]], no solo correr una fórmula.

## Relacionado
- [[muestreo y diseño muestral]]
- [[sesgos en datos y muestreo]]
- [[exactitud y precisión]]
- [[población y muestra]]
- [[tratamiento primario]]
- [[01 - Como dar sentido a los datos]]
