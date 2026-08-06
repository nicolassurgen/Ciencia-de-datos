---
titulo: Estratificación
materia: Estadística
tipo: concepto
tags:
  - estadistica
  - maestria
  - concepto
  - tema/variabilidad
fecha: 2026-08-03
---

# Estratificación

> [!definition] Estratificación
> Técnica de análisis que consiste en **separar** un conjunto de datos en subgrupos (estratos) según alguna variable relevante, para ver si el comportamiento **cambia entre subgrupos** — en lugar de analizar todos los datos "mezclados" como si vinieran de una sola fuente homogénea.

## Por qué hace falta

> [!tip] Los datos globales pueden ocultar comportamientos distintos
> Al mirar el conjunto completo, la variabilidad total puede parecer solo "ruido". Al **estratificar** (por ejemplo, separar los mismos pesos de un producto **por máquina** que lo fabricó), puede aparecer que cada estrato tiene su propio **centro** y **dispersión**. La estratificación es clave para pasar de "hay variabilidad" a "**esta** es la fuente de la variabilidad".

Un histograma **bimodal** (con dos picos) es una señal típica de que hay **dos grupos mezclados** que conviene estratificar por separado.

## Relación con el diagrama de Ishikawa

Las categorías de un [[diagrama de Ishikawa]] (máquina, turno, operario, lote de materia prima, etc.) son candidatas naturales para estratificar: si se sospecha que una de las "6 M" es fuente de variabilidad, estratificar por esa variable es la forma de confirmarlo con los datos.

## Relación con el diseño de experimentos

Estratificar en el análisis (después de recolectar los datos) es distinto de **bloquear** en el diseño (antes de recolectar): el bloqueo en un [[diseño de experimentos|experimento]] construye la separación por estratos **de antemano**, para evitar que una variable se confunda con el factor de interés (ver [[variable de confusión]]).

> [!note] En código
> `df.groupby('maquina')` en Pandas (ver [[06 - Agregacion y groupby]]) calcula un resumen por estrato; `hue=`/`col=`/`row=` en Seaborn (ver [[08 - Grids y comparaciones multiples]]) lo hace **visual**, mostrando los estratos lado a lado en vez de solo como números.

> [!info] A futuro: modelar los estratos en vez de separarlos a mano
> `groupby` estratifica **analizando cada grupo por separado**. Un modelo mixto (`smf.mixedlm(..., groups=df['maquina'])`, ver [[06 - Modelos multivariados y otros]] de statsmodels) hace algo más fino: modela la variabilidad **entre** estratos y **dentro** de cada estrato a la vez, en un solo ajuste.

## Relacionado
- [[02 - El estudio de la variabilidad]]
- [[diagrama de Ishikawa]]
- [[variable de confusión]]
- [[08 - Grids y comparaciones multiples]]
- [[06 - Modelos multivariados y otros]]
