---
titulo: Tratamiento primario de los datos
materia: Estadística
tipo: concepto
tags:
  - estadistica
  - maestria
  - concepto
  - tema/variabilidad
fecha: 2026-08-03
---

# Tratamiento primario de los datos

> [!definition] Tratamiento primario
> Etapa del **Análisis de los Datos** (dentro del [[el ciclo estadístico (PPDAC)|ciclo PPDAC]]) en la que se evalúa la **calidad** de los datos recién recolectados, antes de cualquier análisis descriptivo o inferencial.

## Qué incluye

- **Corregir datos erróneos** → valores que se sabe que están mal (errores de tipeo, de carga, de unidades).
- **Transformar datos** si es necesario (cambiar de escala, unificar formatos, recodificar categorías).
- **Detectar y decidir qué hacer con [[valores atípicos|outliers]]** → no siempre se eliminan; primero hay que entender si son un error o un valor real pero extremo.
- **Completar o tratar datos faltantes**.
- **Verificar la consistencia** entre respuestas.

> [!tip] Consistencia de los datos
> Si hay incoherencia entre respuestas es probable que haya datos falsos o que la pregunta no se haya comprendido. Por eso, al diseñar cuestionarios, a veces se **repite intencionalmente** la misma cuestión redactada de dos formas distintas y mezclada, como forma de **validación**.

> [!warning] Faltantes disfrazados de datos válidos (códigos centinela)
> Un tipo de error particularmente peligroso: encuestas y bases de datos suelen codificar los faltantes con **números que parecen mediciones reales** — por ejemplo, `97 = No corresponde`, `98 = Se negó a responder`, `99 = No sabe/No contesta`, en una variable donde los valores válidos son de un solo o dos dígitos. Si esos códigos no se identifican y convierten a faltante (`None`/`NaN`) **antes** de calcular cualquier medida de resumen, contaminan el resultado de forma silenciosa: un peso registrado como `99` (código de "no sabe") se sumaría como si el objeto pesara 99 kilos. La forma de blindarse es **siempre revisar el diccionario de variables (codebook)** de la fuente de datos antes de asumir que un valor numérico es una medición real. *Fuente: [[Think Stats – Exploratory Data Analysis in Python]], cap. 1.*

> [!tip] Dato crudo (raw) vs. dato derivado (recode)
> Vale la pena distinguir explícitamente el **dato crudo** (`raw data`, tal como se recolectó, sin ninguna transformación) del **dato derivado** (`recode`, una variable nueva calculada a partir de una o más variables crudas mediante alguna regla — por ejemplo, calcular la duración de un evento a partir de dos fechas, o combinar dos preguntas de un cuestionario en un solo indicador). El tratamiento primario y la transformación de datos son, en el fondo, el proceso de construir *recodes* confiables a partir de datos crudos — y toda decisión tomada en ese proceso (qué fórmula se usó, qué se hizo con los faltantes del dato crudo) debería quedar documentada para que el análisis sea reproducible.

> [!tip] Validar contra una fuente de referencia
> Además de revisar consistencia interna entre respuestas, una técnica de validación eficaz es comparar los conteos por categoría de una variable (`value_counts()`) contra una tabla ya publicada sobre la misma población (un informe oficial, el codebook de la encuesta, un censo) — si los conteos no coinciden razonablemente, es una señal de que algo se cargó o codificó mal en el propio dataset, y ayuda a encontrar valores imposibles (por ejemplo, un peso registrado que ningún objeto real podría tener).

> [!note] Preferencia de dígito (*digit preference* / *heaping*)
> Un patrón de mala calidad de datos distinto de un faltante o un atípico: cuando una medición se redondea o se estima "a ojo" en vez de medirse con precisión, ciertos valores (típicamente los que terminan en 0 o en 5) aparecen con una frecuencia mucho mayor de la que deberían tener si la variable fuera realmente continua. Es una señal de que el dato no se midió con el instrumento o la precisión que se supone, y conviene tenerlo en cuenta antes de tratar la variable como estrictamente continua.

## Por qué va antes del análisis descriptivo

Cualquier medida de resumen (media, desvío estándar, etc.) o gráfico que se construya **hereda** los problemas de calidad de los datos de entrada. Un solo dato mal cargado puede distorsionar fuertemente una medida **no robusta** como la media (ver [[robustez estadística]]). El tratamiento primario busca evitar que ese ruido contamine las conclusiones.

> [!tip] Por qué a veces conviene tratar una muestra y no todo el volumen de datos
> Revisar manualmente outliers y faltantes —leer casos sospechosos, decidir caso por caso qué hacer— es viable sobre una muestra de algunos miles de registros. Sobre millones de registros, ese mismo proceso manual se vuelve directamente inviable. Es un argumento práctico (no solo estadístico) a favor de trabajar el tratamiento primario sobre una [[población y muestra|muestra]] manejable antes de escalar cualquier limpieza automatizada al dataset completo. *Fuente: [[Practical Statistics for Data Scientists]] (Bruce & Bruce), cap. 2.*

> [!note] En código
> `df.isnull().sum()`, `df.dropna()`, `df.fillna()` en Pandas (ver [[04 - Datos faltantes]]) son las herramientas para la parte de datos faltantes; para atípicos, ver la nota de código en [[valores atípicos]].

## Relacionado
- [[02 - El estudio de la variabilidad]]
- [[el ciclo estadístico (PPDAC)]]
- [[valores atípicos]]
- [[robustez estadística]]
- [[04 - Datos faltantes]]
