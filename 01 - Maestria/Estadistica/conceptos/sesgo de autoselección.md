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

## Relación con validez externa

> [!important] Es la razón detrás del ejemplo de la clase
> Cuando [[01 - Como dar sentido a los datos|la clase]] pregunta *"¿qué pasa si analizo datos de personas que respondieron voluntariamente?"*, esto es exactamente lo que está en juego: el sesgo de autoselección es una causa concreta de pérdida de [[validez externa]] — la muestra observada no representa a la población que se quería estudiar, por más grande que sea.

## Relacionado
- [[01 - Como dar sentido a los datos]]
- [[validez externa]]
- [[población y muestra]]
- [[sesgo de supervivencia]]
- [[Practical Statistics for Data Scientists]]
