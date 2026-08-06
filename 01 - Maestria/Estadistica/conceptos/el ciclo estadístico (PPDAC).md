---
titulo: El ciclo estadístico (PPDAC)
materia: Estadística
tipo: concepto
tags:
  - estadistica
  - maestria
  - concepto
  - tema/introduccion
fecha: 2026-08-03
---

# El ciclo estadístico (PPDAC)

> [!important] Un camino circular, no una línea recta
> El proceso no termina en una conclusión final: las conclusiones suelen abrir **nuevas preguntas** y reinician el ciclo.

## Las etapas, en orden

1. **P — Planteo del Problema** → definir qué queremos responder. Incluye delimitar la [[población y muestra|población]] y clasificar las variables de interés.
2. **P — Planificación del Estudio Estadístico** → diseñar cómo se van a obtener los datos: censo o muestreo, [[diseño de experimentos|experimento]] u observacional, transversal o longitudinal.
3. **D — Recolección de Datos** → conseguir los datos pertinentes, con instrumentos definidos y trazabilidad.
4. **A — Análisis de los Datos** → [[tratamiento primario]], análisis descriptivo y, si corresponde, inferencial.
5. **C — Obtención de Conclusiones** → interpretar los resultados **en el contexto del problema** planteado en la etapa 1, evaluando [[validez externa]] y [[validez interna]].

![[Ciclo PPDAC.png]]

> [!warning] Advertencia clave
> Aunque los "métodos estadísticos" se concentran en la **recolección** y el **análisis**, no pueden desvincularse del resto. Un buen cálculo sobre un mal diseño no salva nada.
>
> **Los métodos estadísticos NO SUPLEN las falencias de diseño.**

> [!note] En código, por etapa
> El **Análisis** (A) es donde vive el código de este vault: descriptivo con [[04 - Agregaciones y estadistica descriptiva|NumPy]]/[[01 - Introduccion a Series y DataFrame|Pandas]] y [[03 - Estadistica descriptiva|SciPy]]; inferencial —a futuro en la materia— con [[01 - Introduccion a SciPy.stats|scipy.stats]] y [[01 - Introduccion a statsmodels|statsmodels]]. Ninguna de esas herramientas ayuda si el **Planteo** o la **Planificación** (las dos primeras P) estuvieron mal hechos.

## Por qué "circular" importa

Pensar el proceso como un ciclo (y no como una receta lineal de 5 pasos que se hacen una sola vez) recuerda que:
- Una conclusión puede mostrar que la pregunta original estaba mal planteada, y hay que volver al paso 1.
- Un estudio puede ser **exploratorio** (para generar hipótesis) y dar lugar a un ciclo posterior **confirmatorio** (para ponerlas a prueba).

## Relacionado
- [[01 - Como dar sentido a los datos]]
- [[población y muestra]]
- [[tratamiento primario]]
- [[validez externa]] · [[validez interna]]
- [[01 - Introduccion a SciPy.stats]]
- [[01 - Introduccion a statsmodels]]
