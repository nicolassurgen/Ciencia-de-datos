---
titulo: Trazabilidad de datos
materia: Estadística
tipo: concepto
tags:
  - estadistica
  - maestria
  - concepto
  - tema/introduccion
fecha: 2026-08-19
---

# Trazabilidad de datos

Un dato atípico o directamente imposible aparece en la [[matriz de datos]]. La pregunta inmediata es: ¿fue un error de carga, un instrumento descalibrado, o un valor real pero extremo? Responderla depende de algo que hay que haber previsto **antes**, en la etapa de recolección: poder volver de ese dato hacia la unidad, el momento y el instrumento que lo generaron.

> [!definition] Trazabilidad
> "La posibilidad de identificar, rastrear y recuperar las unidades de las cuales se extrajeron los datos, a través de códigos especialmente elaborados. También permite identificar características de interés en dichas unidades (en qué horario fue producida, con qué máquina o lote de materia prima, con qué equipo se realizó la medición, etc.)." *Fuente: [[Estadística para la resolución de problemas en Ingeniería]], cap. 1.*

## Para qué sirve en la práctica

> [!important] El caso de uso más concreto: los datos dudosos
> "Garantizar la trazabilidad de los datos es de gran utilidad, especialmente cuando aparecen datos erróneos, dudosos o atípicos, ya que permite recuperar las unidades elementales de las cuales se extrajeron y eventualmente repetir las mediciones. Los códigos que identifiquen a las unidades deben registrarse en la planilla." *Fuente: [[Estadística para la resolución de problemas en Ingeniería]], cap. 1.*

Es, en esencia, un seguro tomado por adelantado: si no se registró de dónde vino cada dato, un valor sospechoso detectado durante el [[tratamiento primario|tratamiento primario de los datos]] queda sin posibilidad de investigación real — solo se puede corregir a ciegas (o descartar a ciegas), en vez de volver a la fuente y confirmar qué pasó.

> [!tip] Sin trazabilidad, la corrección de errores queda a ciegas
> Si la trazabilidad está garantizada, un dato erróneo detectado durante el tratamiento primario se puede **recuperar y corregir con la unidad real** — volver a medir, revisar el registro original. Sin trazabilidad, la única opción frente a un dato sospechoso es descartarlo o corregirlo con una estimación, sin poder confirmar qué pasó realmente.

## Qué información hace falta registrar

La cita original ya da el listado concreto: horario de producción, máquina, lote de materia prima, equipo de medición. Es, en la práctica, la misma lista de factores que agrupa el [[diagrama de Ishikawa]] (las "6 M") — no es casualidad: si una de esas categorías termina siendo la fuente real de un problema de calidad, solo se puede confirmar y [[estratificación|estratificar]] por ella si quedó registrada desde el principio.

## Dónde se garantiza: en el diseño del instrumento de recolección

> [!note] Planilla de registro, no solo planilla de volcado
> La trazabilidad se decide en el diseño del instrumento de recolección — incluir un código identificador de la unidad en la **planilla de registro** (donde se anota el dato en el momento) — no es algo que se pueda agregar después, una vez que los datos ya están consolidados en la [[matriz de datos|planilla de volcado]] final sin ese código. Es una decisión de diseño temprana, parte de la etapa de "Recolección" del [[el ciclo estadístico (PPDAC)|ciclo PPDAC]], no una corrección posterior.

## Relacionado
- [[01 - Como dar sentido a los datos]]
- [[matriz de datos]]
- [[tratamiento primario]]
- [[diagrama de Ishikawa]]
- [[el ciclo estadístico (PPDAC)]]
- [[valores atípicos]]
