---
titulo: Estabilidad de un proceso
materia: Estadística
tipo: concepto
tags:
  - estadistica
  - maestria
  - concepto
  - tema/variabilidad
fecha: 2026-08-19
---

# Estabilidad de un proceso

Antes de construir un histograma o calcular un promedio, hay una pregunta que tiene que responderse primero, si se cuenta con el orden en que se obtuvieron los datos: ¿el proceso que los generó se comportó siempre igual, o cambió en algún momento? La respuesta decide si tiene sentido "aplastar" los datos en una única distribución, o si hay que mirarlos en el tiempo.

> [!definition] Proceso estable
> "El proceso se comporta de manera **estable** a través del tiempo si actúan siempre las mismas causas y lo hacen de manera similar. La variabilidad en la o las características en estudio se denomina **variabilidad natural**." *Fuente: [[Estadística para la resolución de problemas en Ingeniería]], cap. 1.*

> [!definition] Proceso no estable
> "El proceso no se comporta de manera estable si algunos factores actúan ocasional y fortuitamente en el proceso. La variabilidad se denomina **variabilidad asignable**. En este caso, el modelo se va modificando, por lo que esta variabilidad debe ser identificada y preferentemente eliminada." *Fuente: [[Estadística para la resolución de problemas en Ingeniería]], cap. 1.*

Esta distinción es, en el fondo, la misma que separa las causas comunes de las causas especiales — ver [[causas comunes y causas especiales]] para el desarrollo completo del marco de Shewhart/Deming detrás de esta idea.

## El chequeo obligatorio: graficar contra el tiempo, antes que nada

> [!important] Por qué va primero, no después
> "Si para un conjunto de datos se cuenta con información del orden en el que las unidades fueron seleccionadas o en el que fueron medidas, antes de construir la distribución de frecuencias o realizar cualquier otro análisis con esos datos, es importante evaluar si el comportamiento de la variable es estable, analizando el gráfico de series cronológicas. Si dicho comportamiento no es estable (se presentan tendencias, cambios de nivel, ciclos, etc.) **carece de sentido construir la tabla de distribución de frecuencias** u obtener medidas de resumen para la totalidad de los datos recolectados." *Fuente: [[Estadística para la resolución de problemas en Ingeniería]], cap. 2.*

Es un orden de trabajo concreto, no solo una recomendación general: si hay información de orden temporal disponible, el gráfico de [[series de tiempo]] se mira **antes** que la [[distribución de frecuencias]], no como una verificación posterior. [[02.1 - Casos aplicados]] (Caso 1) desarrolla en detalle qué sale mal cuando se invierte ese orden — un promedio global de 48 cP que no describe ningún día real, calculado sin haber revisado primero si el proceso era estable.

## Patrones de inestabilidad

No todo apartamiento de la estabilidad se ve igual — el libro de cátedra distingue varios patrones típicos en un gráfico de serie cronológica:

- **Tendencia** — el nivel general sube o baja de forma sostenida.
- **Comportamiento cíclico** — el proceso oscila siguiendo un patrón que se repite (estacional, por turno, etc.).
- **Cambio de nivel** — el proceso salta de un régimen a otro en un momento puntual (como el quiebre del día 25 en el Caso 1 de [[02.1 - Casos aplicados]]).
- **Cambio en la variabilidad** — el nivel promedio se mantiene, pero la dispersión alrededor de él aumenta o disminuye.

Solo un gráfico sin ninguno de estos patrones —sin tendencia, sin ciclos, sin saltos, con dispersión pareja— corresponde a un proceso estable.

## Un chequeo adicional: verificar el supuesto de aleatoriedad de la muestra

> [!tip] La serie de tiempo también sirve para auditar el muestreo
> Si la muestra fue obtenida mediante un [[muestreo y diseño muestral|muestreo aleatorio simple]], el gráfico de los datos contra el orden en que fueron seleccionados **no debería mostrar ningún patrón**. Ver un patrón ahí (una tendencia, un ciclo) es evidencia de que el mecanismo de selección no fue tan aleatorio como se suponía — el mismo gráfico que se usa para chequear estabilidad del proceso sirve, con otra lectura, para chequear la calidad del propio muestreo. *Fuente: [[Estadística para la resolución de problemas en Ingeniería]], cap. 2.*

## A dónde conecta esto más adelante

> [!info] A futuro: control estadístico de procesos
> La estabilidad de un proceso es el requisito de entrada para poder aplicar **gráficos de control** y evaluar la **capacidad de un proceso** para cumplir especificaciones — herramientas de control estadístico de procesos que el libro de cátedra menciona explícitamente como no desarrolladas en el texto actual. Quedan señaladas acá porque [[límites de especificación y valor objetivo]] ya depende de este mismo supuesto de estabilidad. *Fuente: [[Estadística para la resolución de problemas en Ingeniería]], cap. 2.*

## Relacionado
- [[causas comunes y causas especiales]]
- [[series de tiempo]]
- [[distribución de frecuencias]]
- [[límites de especificación y valor objetivo]]
- [[muestreo y diseño muestral]]
- [[02.1 - Casos aplicados]]
- [[02 - El estudio de la variabilidad]]
