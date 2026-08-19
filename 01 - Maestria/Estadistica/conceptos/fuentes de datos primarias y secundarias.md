---
titulo: Fuentes de datos primarias y secundarias
materia: Estadística
tipo: concepto
tags:
  - estadistica
  - maestria
  - concepto
  - tema/introduccion
fecha: 2026-08-19
---

# Fuentes de datos primarias y secundarias

No todos los datos que se analizan fueron recolectados por quien los analiza. Distinguir quién generó el dato originalmente cambia lo que se puede saber (o hay que asumir) sobre cómo se lo recolectó.

> [!definition] Fuente primaria
> Los datos se recolectan de **primera mano**, directamente para el estudio que se está haciendo — encuestando, midiendo o registrando personalmente. Quien analiza los datos controla (o al menos conoce de primera mano) el instrumento y el procedimiento de recolección.

> [!definition] Fuente secundaria
> Los datos **ya existían**, recolectados por otra persona u organismo con otro propósito, y se reutilizan para un análisis distinto del que motivó su recolección original. Quien analiza depende de la documentación que haya dejado quien los recolectó (el *codebook*) para entender cómo se obtuvieron.

## Un caso real: ser analista secundario de datos de otro

> [!example] La NSFG y la BRFSS en Think Stats
> [[Think Stats – Exploratory Data Analysis in Python]] es, de principio a fin, un ejemplo de análisis de **fuentes secundarias**: usa datos de la National Survey of Family Growth (NSFG) y del Behavioral Risk Factor Surveillance System (BRFSS), ambas relevadas por organismos de salud de EE.UU. con sus propios fines (vigilancia epidemiológica, estudio de fertilidad), no por el autor del libro. Para el autor —y para cualquier lector del libro que trabaje con esos datos— son fuentes secundarias; para el organismo que diseñó y llevó a cabo la encuesta, son datos de **fuente primaria**. Es el mismo dato, con dos calificaciones distintas según quién lo mira. *Fuente: [[Think Stats – Exploratory Data Analysis in Python]], prefacio.*

## Por qué importa la distinción

> [!important] El codebook es la memoria que reemplaza a "haber estado ahí"
> Al trabajar con una fuente secundaria, no se estuvo presente durante la recolección — no se puede preguntar directamente "¿qué significa este código 97?" Toda la información sobre cómo se definieron las variables, qué significan los valores especiales (ver el aviso sobre códigos centinela en [[tratamiento primario]]) y cómo se diseñó el muestreo (ver [[muestreo y diseño muestral]]) tiene que salir del *codebook* que acompaña a los datos. Trabajar con una fuente secundaria sin revisar su codebook es exponerse a interpretar mal una variable — el mismo riesgo que señala [[tratamiento primario]] sobre los faltantes disfrazados de datos válidos.

> [!tip] En la práctica de ciencia de datos, la mayoría de los proyectos empiezan con fuentes secundarias
> Es poco común que un proyecto de análisis empiece relevando datos propios desde cero — casi siempre se parte de datos ya recolectados por otro sistema (una base transaccional, una API pública, un dataset publicado). Eso hace que revisar críticamente la [[trazabilidad de datos|trazabilidad]] y el proceso de recolección original de una fuente secundaria sea, en la práctica, más la regla que la excepción.

## Relacionado
- [[01 - Como dar sentido a los datos]]
- [[trazabilidad de datos]]
- [[tratamiento primario]]
- [[muestreo y diseño muestral]]
- [[población y muestra]]
