---
titulo: Análisis exploratorio vs. confirmatorio
materia: Estadística
tipo: concepto
tags:
  - estadistica
  - maestria
  - concepto
  - tema/introduccion
fecha: 2026-08-19
---

# Análisis exploratorio vs. confirmatorio

Todavía no siempre hay una pregunta clara antes de mirar los datos — a veces el punto de partida es exactamente al revés: "tengo estos datos, ¿qué hay ahí?". Esa situación (mirar sin una hipótesis previa) y la situación opuesta (ya tener una hipótesis y salir a ponerla a prueba) requieren una actitud distinta frente a los mismos datos, y confundirlas tiene un costo estadístico concreto.

> [!definition] Análisis exploratorio
> Se lleva a cabo **sin ideas previas**, para conocer qué puede estar pasando con un fenómeno. Permite familiarizarse con el problema, identificar variables relevantes y **formular hipótesis** — preguntas para responder más adelante, no todavía respuestas. *Fuente: [[Estadística para la resolución de problemas en Ingeniería]], cap. 4; [[01 - Como dar sentido a los datos]].*

> [!definition] Análisis confirmatorio
> Parte de una **hipótesis ya formulada** de antemano (antes de mirar estos datos en particular) y la **pone a prueba** con un diseño pensado específicamente para eso.

![[Exploratorio a confirmatorio.png]]

## El riesgo de mezclar ambos: por qué el orden importa

No es solo una cuestión de nombres — usar el mismo dataset para explorar y para confirmar tiene una consecuencia estadística real:

> [!quote] Explorar y testear con el mismo dataset infla los falsos positivos
> "I used the same dataset for exploration and testing. If you explore a large dataset, find a surprising effect, and then test whether it is significant, you have a good chance of generating a false positive." *Fuente: [[Think Stats – Exploratory Data Analysis in Python]], cap. 9.*

Si se revisan muchas relaciones posibles entre variables (sin haber planteado de antemano cuál interesaba) y luego se elige mostrar la que "dio un resultado interesante", es casi seguro encontrar **algo**, aunque sea puro azar — cuantos más patrones se prueben, más probable es toparse con uno que parezca significativo sin serlo realmente.

> [!important] Cómo se distingue en la práctica: la replicación
> "Typically the first paper to report a new result is considered **exploratory**. Subsequent papers that replicate the result with new data are considered **confirmatory**." *Fuente: [[Think Stats – Exploratory Data Analysis in Python]], cap. 9.* La forma de saber si un hallazgo exploratorio es real (y no un patrón fortuito de ese dataset en particular) es intentar **reproducirlo con datos nuevos**, distintos de los que lo sugirieron en primer lugar. Think Stats lo hace explícitamente: replica un resultado obtenido con un ciclo de la encuesta NSFG usando datos de un **ciclo posterior** — ver [[estudios transversales y longitudinales]] para el detalle de qué es un "ciclo" en un estudio transversal repetido.

## Cómo conecta con el resto de la materia

Esta distinción no es un detalle de vocabulario aislado — es la antesala conceptual de dos temas que la materia va a desarrollar más adelante:

- **Pruebas de hipótesis** (inferencia): son, por definición, análisis **confirmatorio** — solo tienen la garantía formal que prometen (nivel de significancia, riesgo controlado de error) si la hipótesis se planteó **antes** de ver los datos que la van a poner a prueba.
- **Train/test split** en Machine Learning: la misma lógica de "no confirmar con los mismos datos que exploraste" reaparece, ya en otro contexto, en la práctica de separar los datos en un conjunto para explorar/ajustar un modelo y otro, no visto durante ese proceso, para evaluarlo — una idea que retoma exactamente el mismo problema del *data snooping*.

> [!info] A futuro: sesgo de confirmación, un riesgo emparentado pero distinto
> Existe un sesgo cognitivo con nombre parecido pero de naturaleza distinta: el **sesgo de confirmación** (quien ya cree una afirmación tiende a notar y recordar los casos que la confirman, e ignorar los que la contradicen) — ver la nota al pie en [[sesgo de autoselección]]. No es lo mismo que "análisis confirmatorio": ese es un **diseño de estudio** válido y necesario; el sesgo de confirmación es un error de razonamiento que puede colarse incluso dentro de un análisis bien diseñado.

## Relacionado
- [[01 - Como dar sentido a los datos]]
- [[estudios transversales y longitudinales]]
- [[estadística descriptiva vs inferencial]]
- [[sesgos en datos y muestreo]]
- [[el ciclo estadístico (PPDAC)]]
