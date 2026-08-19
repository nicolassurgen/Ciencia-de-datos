---
titulo: Sesgo de autoselección
materia: Estadística
tipo: concepto
tags:
  - estadistica
  - maestria
  - concepto
  - tema/introduccion
fecha: 2026-08-06
---

# Sesgo de autoselección

> [!definition] Sesgo de autoselección (self-selection bias)
> Ocurre cuando quienes terminan formando parte de la muestra lo hacen por una **decisión propia** (responder una encuesta, anotarse a algo, escribir una reseña), y esa decisión está relacionada con lo que se quiere medir. La muestra deja de representar a la población, porque el mecanismo que decide "quién entra" no es azaroso.

## El caso clásico: la encuesta de *Literary Digest* (1936)

*Literary Digest*, una revista líder de la época, encuestó a más de **10 millones** de personas (sus propios suscriptores, más listas de gente con teléfono y auto) y predijo una victoria arrasadora de Landon sobre Roosevelt. George Gallup, con apenas **2.000** encuestados pero bien seleccionados, predijo correctamente la victoria de Roosevelt.

```
Muestra de Literary Digest = gente de nivel socioeconómico alto (sesgada)
Muestra de Gallup          = 2.000 personas, pero representativas
```

> [!important] Más muestra no compensa una muestra sesgada
> 10 millones de respuestas mal seleccionadas perdieron contra 2.000 bien seleccionadas. El tamaño de la muestra no arregla un mecanismo de selección sesgado — ver [[población y muestra]].

## Otro ejemplo típico: reseñas online

Las reseñas de restaurantes, hoteles o productos en sitios como Yelp o Google están sujetas a sesgo de autoselección: quien escribe una reseña **decidió** hacerlo, y esa decisión suele estar asociada a haber tenido una experiencia particularmente **buena o mala** — no es una muestra al azar de todos los clientes.

> [!tip] Un matiz: sirve para comparar, no para medir el promedio real
> El promedio de estrellas de un solo lugar puede estar sesgado (solo opina quien tuvo una experiencia extrema). Pero si el **mismo sesgo** afecta a dos lugares comparables, comparar sus promedios entre sí puede seguir siendo razonablemente confiable — el sesgo "se cancela" en la comparación, aunque no en el valor absoluto.

## Sesgos relacionados, pero distintos

> [!note] Autoselección es un caso particular de un problema más general: el sesgo de muestreo
> El **sesgo de muestreo** (*sampling bias*) es la categoría general: cualquier mecanismo por el cual la forma de seleccionar la muestra la hace no representativa de la población. La autoselección es **una causa concreta** de sesgo de muestreo (la decide el propio individuo), pero no la única — un método de reclutamiento que sistemáticamente excluye a cierto grupo (p. ej. encuestar solo por teléfono fijo, que excluye a quien no tiene) es sesgo de muestreo sin que nadie se haya "autoseleccionado".

> [!note] Sesgo de confirmación: un problema distinto, sobre qué se cuenta, no sobre quién participa
> El **sesgo de confirmación** (*confirmation bias*) es un sesgo hermano pero conceptualmente distinto: quien ya cree una afirmación tiende a recordar y compartir los casos que la confirman, y a pasar por alto los que la contradicen. La diferencia con la autoselección es dónde ocurre el sesgo — en autoselección, el sesgo está en **quién termina en la muestra**; en confirmación, está en **qué anécdotas o casos se eligen contar**, incluso a partir de la misma población de eventos. *Fuente: [[Think Stats – Exploratory Data Analysis in Python]], cap. 1.*

> [!info] A futuro: un mecanismo de sesgo con causa distinta (length-biased sampling)
> Existe otro sesgo emparentado pero con un mecanismo propio: cuando la probabilidad de que una unidad **aparezca** en la muestra es proporcional a su propio tamaño (por ejemplo, preguntarles a estudiantes "¿cuántos alumnos tiene tu clase?" sobrerrepresenta a las clases grandes, porque hay más alumnos ahí para responder), el promedio observado sobreestima sistemáticamente el promedio real — sin que nadie haya decidido "autoseleccionarse" ni haya un error de medición de por medio. No se desarrolla en detalle acá por ser un mecanismo distinto; queda señalado como referencia si la materia lo trata más adelante.

## Relación con validez externa

> [!important] Es la razón detrás del ejemplo de la clase
> Cuando [[01 - Como dar sentido a los datos|la clase]] pregunta *"¿qué pasa si analizo datos de personas que respondieron voluntariamente?"*, esto es exactamente lo que está en juego: el sesgo de autoselección es una causa concreta de pérdida de [[validez externa]] — la muestra observada no representa a la población que se quería estudiar, por más grande que sea.

## Relacionado
- [[01 - Como dar sentido a los datos]]
- [[validez externa]]
- [[población y muestra]]
- [[sesgo de supervivencia]]
- [[sesgos en datos y muestreo]]
- [[Practical Statistics for Data Scientists]]
