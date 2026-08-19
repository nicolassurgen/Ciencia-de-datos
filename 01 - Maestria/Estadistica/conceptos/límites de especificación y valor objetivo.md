---
titulo: Límites de especificación y valor objetivo
materia: Estadística
tipo: concepto
tags:
  - estadistica
  - maestria
  - concepto
  - tema/variabilidad
fecha: 2026-08-19
---

# Límites de especificación y valor objetivo

Un histograma solo, sin nada más, describe una distribución — pero no dice si esa distribución es "buena" o "mala". Para eso hace falta compararla contra algo externo: lo que se **pretende** que el proceso produzca. Esa comparación es lo que agregan los límites de especificación.

> [!definition] Límites de especificación
> "Si respecto de alguna variable de interés, existen límites de especificación que las unidades de la población deben cumplir, el histograma y la información brindada por las medidas de localización y de dispersión resultan de mucha utilidad para analizar si el proceso es capaz de cumplir con las especificaciones fijadas." *Fuente: [[Estadística para la resolución de problemas en Ingeniería]], cap. 2.*

> [!definition] Valor objetivo (target) y tolerancia
> "Las especificaciones que debe cumplir alguna variable de interés en la población, se definen de la forma $T \pm h$, donde **T es el valor nominal o valor objetivo** y $h$ es la tolerancia que se admite. Sería ideal que la media del proceso, $\mu$, coincida con T y que el desvío estándar del proceso, $\sigma$, sea claramente menor que $h$." *Fuente: [[Estadística para la resolución de problemas en Ingeniería]], cap. 2.*

## Las cuatro combinaciones posibles

Cumplir con la especificación no depende de una sola cosa — depende, a la vez, de dónde está centrado el proceso (¿$\mu$ coincide con $T$?) y de cuánto varía (¿$\sigma$ es chico frente a $h$?). Cruzando esas dos preguntas aparecen cuatro escenarios distintos:

| | Variabilidad aceptable ($\sigma \ll h$) | Variabilidad excesiva ($\sigma$ grande) |
|---|---|---|
| **Bien centrado** ($\mu \approx T$) | Cumple | No cumple — hay que **reducir la dispersión** |
| **Descentrado** ($\mu \neq T$) | No cumple — hay que **corregir el centro** | No cumple, por las dos razones a la vez |

> [!important] Por qué distinguir el caso importa
> Cada una de las tres celdas de incumplimiento requiere una intervención **distinta**: correr el proceso a un centrado (recalibrar, ajustar un parámetro de la máquina) es una acción; reducir la variabilidad (identificar y eliminar una causa especial, ver [[causas comunes y causas especiales]]) es otra completamente diferente. Diagnosticar mal cuál de las dos falla —o si fallan las dos— lleva a intervenir donde no corresponde y no resolver el problema real.

## El requisito silencioso: que el proceso sea estable

> [!warning] Esto presupone estabilidad
> "El análisis de la capacidad de un proceso para cumplir con ciertas especificaciones presupone que este se comporta de manera **estable**, lo cual se evalúa mediante gráficos de control, que no se desarrollan en el presente texto." *Fuente: [[Estadística para la resolución de problemas en Ingeniería]], cap. 2.* Hablar de "la media del proceso" y "el desvío del proceso" como si fueran valores fijos solo tiene sentido si el proceso no está cambiando de régimen — ver [[estabilidad de un proceso]]. Comparar contra límites de especificación un proceso que en realidad mezcla dos regímenes distintos ([[02.1 - Casos aplicados]], Caso 1) lleva a conclusiones tan engañosas como las que produce mirar solo el promedio.

## Una forma descriptiva de estimar cuánta variabilidad hay

Sin llegar todavía a la capacidad de proceso formal, se puede usar la regla empírica ya vista en la materia para tener una primera idea de cuánto "ocupa" la variabilidad del proceso frente a la tolerancia permitida:

> [!tip] Los intervalos $\bar y \pm ks$
> Construir $\bar y \pm s$, $\bar y \pm 2s$ y $\bar y \pm 3s$ y ver qué proporción de los datos cae dentro de cada uno da una idea rápida de qué tan "ancho" es el proceso en relación a $h$. Desarrollo completo, con los porcentajes esperados en datos razonablemente simétricos, en [[medidas de dispersión]].

## A dónde lleva esto más adelante

> [!info] A futuro: capacidad de proceso ($C_p$ / $C_{pk}$)
> El paso siguiente, no desarrollado en este curso, es resumir la relación entre tolerancia y variabilidad en un único índice numérico de **capacidad de proceso** — $C_p$ compara únicamente el ancho de la tolerancia con la dispersión del proceso (ignora el centrado); $C_{pk}$ sí penaliza el descentrado. Son la formalización cuantitativa de las cuatro combinaciones descriptas arriba.

## Relacionado
- [[estabilidad de un proceso]]
- [[causas comunes y causas especiales]]
- [[medidas de dispersión]]
- [[medidas de posición]]
- [[histograma]]
- [[02 - El estudio de la variabilidad]]
