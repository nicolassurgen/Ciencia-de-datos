---
titulo: Causas comunes y causas especiales
materia: Estadística
tipo: concepto
tags:
  - estadistica
  - maestria
  - concepto
  - tema/variabilidad
fecha: 2026-08-03
---

# Causas comunes y causas especiales

> [!tip] Marco conceptual de Shewhart / Deming
> La variabilidad de un proceso se separa en dos tipos de causas, una distinción central en control de calidad.

> [!definition] Causas comunes
> Variabilidad **"natural"**, inherente al proceso cuando funciona de forma estable. Está siempre presente, viene de la suma de muchas pequeñas fuentes (ver [[diagrama de Ishikawa]]: las 6 M) y produce un patrón **predecible**.

> [!definition] Causas especiales (o asignables)
> Algo **puntual y ajeno** al funcionamiento normal del proceso (una máquina desajustada, un lote de materia prima defectuoso, un operario nuevo sin entrenar). **Rompen la estabilidad** del proceso y producen un comportamiento que ya no es el habitual.

## Por qué importa la distinción

Esta separación explica por qué más adelante importa si los datos muestran o no un **comportamiento estable en el tiempo**:

- Si solo hay **causas comunes**, el proceso es estable y una [[distribución de frecuencias]] resume bien su comportamiento — el pasado es representativo del futuro cercano.
- Si hay **causas especiales** actuando, el proceso no es estable: conviene analizarlo como [[series de tiempo|serie de tiempo]], porque una distribución "aplastaría" justamente la señal de que algo cambió.

## Relación con el diseño de experimentos

En un [[diseño de experimentos|experimento]], la **replicación** permite estimar la variabilidad por causas comunes (el "ruido" de fondo), de modo que un efecto atribuible a un factor manipulado (una causa especial introducida deliberadamente) pueda distinguirse de esa variabilidad natural.

## Relacionado
- [[estabilidad de un proceso]]
- [[02 - El estudio de la variabilidad]]
- [[diagrama de Ishikawa]]
- [[series de tiempo]]
- [[diseño de experimentos]]
