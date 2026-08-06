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

## Por qué va antes del análisis descriptivo

Cualquier medida de resumen (media, desvío estándar, etc.) o gráfico que se construya **hereda** los problemas de calidad de los datos de entrada. Un solo dato mal cargado puede distorsionar fuertemente una medida **no robusta** como la media (ver [[robustez estadística]]). El tratamiento primario busca evitar que ese ruido contamine las conclusiones.

> [!note] En código
> `df.isnull().sum()`, `df.dropna()`, `df.fillna()` en Pandas (ver [[04 - Datos faltantes]]) son las herramientas para la parte de datos faltantes; para atípicos, ver la nota de código en [[valores atípicos]].

## Relacionado
- [[02 - El estudio de la variabilidad]]
- [[el ciclo estadístico (PPDAC)]]
- [[valores atípicos]]
- [[robustez estadística]]
- [[04 - Datos faltantes]]
