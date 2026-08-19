---
titulo: Estudios transversales y longitudinales
materia: Estadística
tipo: concepto
tags:
  - estadistica
  - maestria
  - concepto
  - tema/introduccion
fecha: 2026-08-19
---

# Estudios transversales y longitudinales

¿La foto o la película? Es la pregunta de fondo detrás de esta distinción: un estudio puede registrar un fenómeno en **un solo momento** (una foto de la situación actual) o **seguirlo en el tiempo** (una película de cómo va cambiando). Elegir mal entre las dos deja abierta una pregunta que después no se puede responder con los datos que se tienen.

> [!definition] Estudio transversal (cross-sectional)
> "A study that captures a snapshot of a group at a point in time." Registra el estado de las unidades **una sola vez**. *Fuente: [[Think Stats – Exploratory Data Analysis in Python]], cap. 1.*

> [!definition] Estudio longitudinal
> "A study that follows a population over time, collecting data from the same group repeatedly." Observa a **las mismas unidades**, en más de un momento, para poder ver cómo cambian. *Fuente: [[Think Stats – Exploratory Data Analysis in Python]], cap. 1.*

## Un caso intermedio: el transversal repetido

Existe una tercera variante, que conviene no confundir con la longitudinal aunque también involucre varios momentos en el tiempo:

> [!important] Ciclo — no es lo mismo que longitudinal
> "In a repeated cross-sectional study, each repetition of the study is called a **cycle**." *Fuente: [[Think Stats – Exploratory Data Analysis in Python]], cap. 1.* Un estudio transversal **repetido** vuelve a tomar una foto cada cierto tiempo (un nuevo "ciclo"), pero cada foto es de una muestra **nueva** de la población, no de las mismas personas seguidas en el tiempo. La NSFG, por ejemplo, se realizó siete veces (siete ciclos) entre distintos años — cada ciclo es transversal en sí mismo, y comparar dos ciclos permite ver tendencias generales de la población, pero **no** permite decir "esta persona cambió de esta forma" — para eso hace falta un diseño longitudinal real, que siga a los mismos individuos.

## Por qué importa la diferencia

- Un estudio **transversal** puede decir "hoy, el 20 % de la población tiene la característica X" — pero no puede decir si ese 20 % está aumentando, disminuyendo o si son las mismas personas de hace un año.
- Un estudio **longitudinal** sí permite hablar de **cambio dentro de las mismas unidades** — pero es mucho más costoso de llevar adelante (hay que volver a encontrar y volver a medir a las mismas personas, con el riesgo de que algunas abandonen el estudio con el tiempo).

> [!tip] Representatividad, un objetivo típico del diseño transversal
> "In general, cross-sectional studies are meant to be representative, which means that every member of the target population has an equal chance of participating." *Fuente: [[Think Stats – Exploratory Data Analysis in Python]], cap. 1.* Ver [[muestreo y diseño muestral]] para el desarrollo completo de qué hace falta para que un estudio (transversal o longitudinal) sea efectivamente representativo.

## Relación con series de tiempo

No hay que confundir un estudio **longitudinal** (sigue a las mismas unidades, que pueden cada una tener su propia trayectoria) con una [[series de tiempo|serie de tiempo]] de un proceso (una sola magnitud medida repetidamente a lo largo del tiempo, como la viscosidad diaria de un producto). Ambos incorporan la dimensión temporal, pero responden preguntas distintas: uno sigue **individuos**, el otro sigue **un proceso**.

## Relacionado
- [[01 - Como dar sentido a los datos]]
- [[estudio observacional vs experimental]]
- [[muestreo y diseño muestral]]
- [[series de tiempo]]
- [[análisis exploratorio vs confirmatorio]]
