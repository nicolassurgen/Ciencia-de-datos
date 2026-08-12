---
titulo: Exactitud y precisión
materia: Estadística
tipo: concepto
tags:
  - estadistica
  - maestria
  - concepto
  - tema/variabilidad
fecha: 2026-08-11
---

# Exactitud y precisión

Decir que "en promedio, dos instrumentos miden igual" no alcanza para decir que **miden igual**. Dos instrumentos pueden coincidir perfectamente en el promedio de sus errores y, aun así, ser radicalmente distintos en qué tan confiable es *cada medición individual* que producen. Separar esas dos preguntas —¿el instrumento acierta en promedio? y ¿cuánto varía de una medición a otra?— es exactamente lo que distinguen la exactitud y la precisión.

> [!definition] Exactitud (accuracy)
> Qué tan cerca está, **en promedio**, el valor medido del valor real. Se evalúa mirando el **centro** de la distribución de los errores de medición (error = valor obtenido − valor real): si el error promedio es cercano a cero, el instrumento es exacto — no tiene un **sesgo** sistemático hacia arriba o hacia abajo.

> [!definition] Precisión (precision)
> Qué tan **repetible** es una medición: si se mide el mismo objeto varias veces, ¿los resultados quedan agrupados o dispersos? Se evalúa mirando la **dispersión** de los errores (desvío estándar, RIQ) — no el promedio. Un instrumento preciso da resultados parecidos entre sí, esté o no centrado en el valor correcto.

## Por qué son dos preguntas distintas

Exactitud es una pregunta sobre el **centro** (media, mediana); precisión es una pregunta sobre la **dispersión** (desvío estándar, RIQ). Son dos ejes independientes — un instrumento puede tener cualquier combinación de las dos:

| | Exacto (bajo sesgo) | Inexacto (con sesgo) |
|---|---|---|
| **Preciso** (baja dispersión) | Mediciones agrupadas alrededor del valor real | Mediciones agrupadas, pero lejos del valor real |
| **Impreciso** (alta dispersión) | Mediciones centradas en el valor real, pero muy dispersas | Mediciones dispersas y además lejos del valor real |

> [!example] Caso real: dos laboratorios que "miden igual" en promedio
> Dos laboratorios miden 20 veces una misma muestra patrón (cantidad conocida) y se registra el error de cada medición. El error promedio da casi idéntico en ambos ($\approx -0{,}006$) — a simple vista, "miden igual". Pero el desvío estándar del error es $0{,}110$ en el Laboratorio A y $0{,}037$ en el Laboratorio B: el A varía casi **3 veces más** que el B de una medición a la siguiente. Ambos laboratorios son igual de **exactos** (sin sesgo sistemático), pero el B es mucho más **preciso**. Desarrollo completo del caso en [[02.1 - Casos aplicados]].

> [!important] Por qué no alcanza con el promedio
> Reportar solo el error promedio (la exactitud) y concluir que "miden igual" ignora por completo la precisión. En la práctica, un instrumento menos preciso es menos confiable **aunque no tenga sesgo**: cualquier medición individual que devuelva puede estar bastante lejos del valor real, aun cuando el promedio de muchas mediciones no lo esté. La combinación correcta para evaluar un instrumento es siempre **centro + dispersión** — el mismo principio general que en [[medidas de dispersión]].

## Relacionado
- [[medidas de posición]]
- [[medidas de dispersión]]
- [[robustez estadística]]
- [[02.1 - Casos aplicados]]
- [[02 - El estudio de la variabilidad]]
