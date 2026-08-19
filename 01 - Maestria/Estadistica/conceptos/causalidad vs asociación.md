---
titulo: Causalidad vs. asociación
materia: Estadística
tipo: concepto
tags:
  - estadistica
  - maestria
  - concepto
  - tema/introduccion
fecha: 2026-08-19
---

# Causalidad vs. asociación

Dos variables se mueven juntas: el uso de protector solar y las quemaduras de piel están asociados (a más protector, menos quemaduras) — pero también lo están las ventas de helado y los ahogamientos en piletas (ambos suben en verano). En el primer caso hay una causa directa; en el segundo, ninguna de las dos variables causa a la otra — ambas responden a una tercera, el calor. Distinguir estos dos casos, sin más información que "X e Y están asociadas", es imposible. Esta nota es sobre por qué, y qué hace falta para ir más allá.

> [!definition] Asociación (o correlación)
> Dos variables están asociadas cuando sus valores tienden a variar juntos de forma sistemática — cuando una cambia, la otra también tiende a cambiar, de forma predecible. Es un hecho puramente **descriptivo**: no dice nada sobre el mecanismo que produce esa relación.

> [!definition] Causalidad
> X causa Y cuando un cambio en X **produce** un cambio en Y — si se pudiera intervenir sobre X manteniendo todo lo demás constante, Y cambiaría en consecuencia. Es una afirmación sobre el **mecanismo**, no solo sobre el patrón de los datos.

## Por qué asociación no implica causalidad

> [!quote] Tres explicaciones posibles para una correlación
> "If variables A and B are correlated, there are three possible explanations: A causes B, or B causes A, or some other set of factors causes both A and B. Correlation alone does not distinguish between these explanations, so it does not tell you which ones are true. This rule is often summarized with the phrase 'Correlation does not imply causation.'" *Fuente: [[Think Stats – Exploratory Data Analysis in Python]], cap. 7.*

La tercera explicación —que un factor externo cause a ambas— es exactamente lo que en este vault se desarrolla como [[variable de confusión]]: el caso del ejemplo de las ventas de helado y los ahogamientos, donde el calor (variable de confusión, no medida ni controlada) genera una asociación entre dos variables que no tienen ninguna relación causal directa entre sí.

## Dos formas de acercarse a la causalidad

Ni el libro de cátedra ni la asociación por sí sola resuelven esto — pero hay dos criterios concretos que ayudan a inclinar la balanza:

> [!tip] Usar el orden temporal
> "Use time. If A comes before B, then A can cause B but not the other way around [...] The order of events can help us infer the direction of causation, but it does not preclude the possibility that something else causes both A and B." *Fuente: [[Think Stats – Exploratory Data Analysis in Python]], cap. 7.* Saber que A ocurrió antes que B descarta que B cause a A — pero no descarta una variable de confusión que cause a ambas.

> [!important] Usar el azar: por qué el experimento es la herramienta más fuerte
> "Use randomness. If you divide a large sample into two groups at random [...] you can eliminate spurious relationships." Es la base del [[estudio observacional vs experimental|experimento controlado aleatorizado]]: asignar el "tratamiento" al azar entre dos grupos garantiza que, en promedio, **todo lo demás** (conocido y desconocido) queda distribuido parejo entre ambos grupos — así, cualquier diferencia que persista solo puede deberse al tratamiento. *Fuente: [[Think Stats – Exploratory Data Analysis in Python]], cap. 7.*

## La versión de ciencia de datos: predicción vs. explicación

> [!quote] Practical Statistics for Data Scientists
> "A regression model that fits the data well is set up such that changes in X lead to changes in Y. However, by itself, the regression equation does not prove the direction of causation [...] It is our knowledge of the marketing process, not the regression equation, that leads us to the conclusion that clicks on the ad lead to sales, and not vice versa." *Fuente: [[Practical Statistics for Data Scientists]] (Bruce & Bruce), cap. 4.*

Es un punto que se va a volver crítico más adelante en la materia, cuando aparezca la regresión: un modelo que ajusta bien los datos y predice con precisión **no** demuestra por sí solo una relación causal. Un modelo puede ser excelente para predecir (usar X para anticipar Y) sin que eso implique que intervenir sobre X vaya a cambiar Y — la diferencia entre "predecir" y "explicar" depende de conocimiento externo al propio modelo, no de qué tan bien ajusten los datos.

## Cuándo sí se puede hablar de causalidad con más confianza

| Diseño | ¿Permite hablar de causalidad? |
|---|---|
| [[estudio observacional vs experimental\|Estudio observacional]] | Débilmente — siempre queda abierta la duda de una [[variable de confusión]] no medida |
| Experimento **no** aleatorizado | Algo mejor, pero sigue expuesto a confusión si los grupos ya diferían de antemano |
| Experimento **aleatorizado** ([[estudio observacional vs experimental\|A/B test]], ensayo clínico) | La forma más confiable de establecer causalidad |

> [!info] A futuro
> Existen técnicas para estimar efectos causales a partir de datos puramente observacionales (variables instrumentales, *propensity score matching*, diseños de regresión discontinua) que exceden el nivel actual del curso — quedan señaladas para cuando la materia (o la bibliografía de inferencia/regresión) las desarrolle.

## Relacionado
- [[variable de confusión]]
- [[estudio observacional vs experimental]]
- [[validez interna]]
- [[diseño de experimentos]]
- [[02 - Matrices]]
- [[03 - Optimizacion]]
