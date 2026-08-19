---
titulo: Estudio observacional vs. experimental
materia: Estadística
tipo: concepto
tags:
  - estadistica
  - maestria
  - concepto
  - tema/introduccion
fecha: 2026-08-19
---

# Estudio observacional vs. experimental

Antes de recolectar un solo dato hay que decidir algo que va a condicionar **qué se puede concluir después**: ¿el investigador se limita a registrar lo que pasa, tal como pasa? ¿O interviene, modificando algo, para ver qué efecto produce ese cambio? La diferencia entre observar e intervenir es una de las decisiones de diseño más importantes de todo el [[el ciclo estadístico (PPDAC)|ciclo PPDAC]], porque de ella depende directamente qué tan fuerte puede ser la conclusión sobre [[causalidad vs asociación|causalidad]].

> [!definition] Estudio observacional
> "Un estudio observacional es un estudio en el cual se registran los valores de algunas características de interés en las unidades, sin realizar modificaciones en la población o proceso, excepto las necesarias para obtener los datos requeridos. En este tipo de estudio no se intenta manipular ni modificar las unidades." *Fuente: [[Estadística para la resolución de problemas en Ingeniería]], cap. 1.*

> [!definition] Estudio experimental
> "Un estudio experimental o experimento propiamente dicho, es un estudio en el cual se hacen cambios en los niveles de algunas variables (factores) [...] con el objetivo de analizar si dichas modificaciones influyen/afectan a los valores de algunas características de interés (variables de respuesta) [...] Los experimentos constituyen la mejor manera de valorar el efecto de uno o más factores sobre alguna variable de interés." *Fuente: [[Estadística para la resolución de problemas en Ingeniería]], cap. 1.*

Incluso el vocabulario cambia entre uno y otro: se habla de **unidades observacionales** en el primer caso, y de **unidades experimentales** en el segundo.

## Por qué el experimento permite concluir más fuerte

En un experimento, quien investiga **controla** qué factores varían y cómo — típicamente asignando los tratamientos al azar entre las unidades. Eso es justamente lo que permite descartar que la diferencia observada se deba a otra cosa que no sea el factor manipulado. Es la misma lógica, vista desde el lado del diseño, que [[causalidad vs asociación]] plantea desde el lado del análisis: solo controlando (o aleatorizando) los demás factores se puede aislar el efecto de uno solo.

> [!example] Caso aplicado: el dispositivo neumático de siembra
> Una fábrica quiere comparar dos dispositivos de siembra en un cultivo. En vez de comparar dos lotes que ya existían de antemano (lo que dejaría abierta la duda de si la diferencia se debe al dispositivo o a algo distinto entre los lotes), se sortea **al azar** qué parcelas usan cada dispositivo dentro de un mismo campo, controlando el resto de los factores (tipo de semilla, riego, fecha de siembra). Desarrollo completo del ejemplo en [[diseño de experimentos]].

## La versión de ciencia de datos: el A/B test

En ámbitos digitales (sitios web, apps), el experimento controlado tiene un nombre específico:

> [!quote] A/B testing
> "An A/B test is an experiment with two groups to establish which of two treatments, products, procedures, or the like is superior. Often one of the two treatments is the standard existing treatment, or no treatment. If a standard (or no) treatment is used, it is called the **control**." *Fuente: [[Practical Statistics for Data Scientists]] (Bruce & Bruce), cap. 3.*

> [!important] Por qué hace falta un grupo de control
> "Without a control group, there is no assurance that 'other things are equal' and that any difference is really due to the treatment (or to chance)." *Fuente: [[Practical Statistics for Data Scientists]] (Bruce & Bruce), cap. 3.* Sin un grupo que **no** recibe el tratamiento (o recibe el tratamiento "de siempre"), no hay con qué comparar: cualquier cambio observado podría deberse a factores externos que también hubieran ocurrido sin la intervención (una tendencia estacional, un evento externo), no al tratamiento en sí.

## Cuando el experimento no es posible: el experimento natural

> [!quote] Natural experiment
> "Controlled trials are only possible in the laboratory sciences, medicine, and a few other disciplines. In the social sciences, controlled experiments are rare, usually because they are impossible or unethical. An alternative is to look for a natural experiment, where different 'treatments' are applied to groups that are otherwise similar. One danger of natural experiments is that the groups might differ in ways that are not apparent." *Fuente: [[Think Stats – Exploratory Data Analysis in Python]], cap. 7.*

Un experimento natural es, en la práctica, un estudio **observacional** que se parece a un experimento porque el azar (o alguna circunstancia externa, no controlada por quien investiga) ya separó a los grupos por sí solo — pero sigue siendo observacional en el sentido de que nadie asignó los tratamientos deliberadamente, y por lo tanto sigue expuesto a que los grupos difieran en algo más que en el "tratamiento" que se quiere estudiar.

## Tabla comparativa

| | Observacional | Experimental |
|---|---|---|
| ¿Quién decide los valores del factor? | Nadie — se observan tal como ocurren | Quien investiga, idealmente al azar |
| Riesgo principal | [[variable de confusión|Variables de confusión]] | Menor (controlado por el diseño) |
| Fuerza de la conclusión causal | Débil — solo asociación | Fuerte, si está bien diseñado |
| Ejemplo | Encuesta NSFG (registra, no interviene) | A/B test, ensayo clínico aleatorizado |

## Relacionado
- [[diseño de experimentos]]
- [[causalidad vs asociación]]
- [[variable de confusión]]
- [[validez interna]]
- [[estudios transversales y longitudinales]]
- [[01 - Como dar sentido a los datos]]
