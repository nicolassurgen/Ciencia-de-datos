---
titulo: Optimización
materia: Matemática
tipo: apunte
fecha: 2026-08-01
tags:
  - matematica
  - maestria
  - calculo
  - ciencia-de-datos
  - mlops
  - tema/optimizacion
---

## ¿Qué es optimizar?

**Optimizar** es encontrar el punto que **minimiza** (o maximiza) una función. En Machine Learning, esa función casi siempre es una **función de costo o pérdida** $J(\mathbf{w})$: mide qué tan mal predice un modelo con un conjunto de parámetros $\mathbf{w}$, y **entrenar un modelo es, literalmente, resolver un problema de optimización**:

$$\mathbf{w}^{*} = \arg\min_{\mathbf{w}} J(\mathbf{w})$$

## Puntos críticos y tipos de mínimo

Un **punto crítico** es donde el [[02 - Derivadas|gradiente]] se anula: $\nabla J(\mathbf{w}) = 0$. Ahí la función no crece ni decrece en ninguna dirección — puede ser un mínimo, un máximo o un **punto de silla**.

- **Mínimo local** → el valor más bajo en un entorno cercano, pero no necesariamente en todo el dominio.
- **Mínimo global** → el valor más bajo posible en todo el dominio.
- **Función convexa** → tiene un único mínimo, que es automáticamente global. Es el caso "fácil": no hay mínimos locales que puedan engañar al algoritmo.
- **Función no convexa** → puede tener múltiples mínimos locales. La mayoría de las redes neuronales entrenan funciones de costo no convexas.

> [!warning]
> En la práctica de deep learning casi nunca se garantiza llegar al mínimo global; se busca un mínimo local **suficientemente bueno**.

## Descenso por gradiente (*gradient descent*)

El algoritmo de optimización más usado en ML. La idea: moverse repetidamente en la dirección **opuesta al gradiente** (la de máximo decrecimiento, ver [[02 - Derivadas]]):

$$\mathbf{w}_{t+1} = \mathbf{w}_t - \eta \, \nabla J(\mathbf{w}_t)$$

donde $\eta$ (*eta*) es la **tasa de aprendizaje** (*learning rate*): qué tan grande es cada paso.

> [!tip] El learning rate importa muchísimo
> - Muy **chico** → converge, pero muy lentamente.
> - Muy **grande** → puede "saltar" por encima del mínimo y no converger, o directamente diverger.

### Variantes habituales (para tener el mapa, sin entrar en detalle todavía)

- **SGD (*Stochastic Gradient Descent*)** → calcula el gradiente sobre un subconjunto (*batch*) de datos en vez de todo el dataset, mucho más eficiente en datasets grandes.
- **Momentum** → acumula una "inercia" de los gradientes anteriores para acelerar la convergencia y suavizar oscilaciones.
- **Adam** → combina momentum con una tasa de aprendizaje adaptativa por parámetro; es el optimizador por defecto en la mayoría de los frameworks de deep learning actuales.

## Métodos de segundo orden

El gradient descent solo usa la **primera derivada** (el gradiente). Los métodos de segundo orden (como el **método de Newton**) usan además el **Hessiano** (ver [[02 - Derivadas]] y [[02 - Matrices]]) para aprovechar información sobre la **curvatura** de la función y converger en menos pasos. Son más precisos pero mucho más costosos de calcular en modelos con millones de parámetros — por eso en deep learning se usan casi exclusivamente métodos de primer orden (SGD, Adam).

## Regularización: un problema de optimización con restricciones

Muchas funciones de costo se modifican agregando un término de penalización sobre los parámetros, para evitar el sobreajuste (*overfitting*):

$$J_{\text{reg}}(\mathbf{w}) = J(\mathbf{w}) + \lambda \, \|\mathbf{w}\|$$

Usando la [[01 - Vectores|norma]] L1 (Lasso) o L2 (Ridge) del vector de parámetros. Optimizar esta versión "regularizada" empuja a los parámetros hacia valores más chicos o más dispersos (más ceros), según la norma elegida.

## Por qué esto importa para Data Science y MLOps

- **Entrenar cualquier modelo** (regresión, redes neuronales, boosting) es, en el fondo, resolver un problema de optimización.
- **Elegir el learning rate y el optimizador** es una de las decisiones prácticas más frecuentes al entrenar una red neuronal.
- **Diagnosticar un entrenamiento que no converge** (pérdida que oscila, que no baja, que diverge) requiere entender estos conceptos: tasa de aprendizaje, convexidad, mínimos locales.

## Temas relacionados

- [[02 - Derivadas]] — el gradiente y el Hessiano, la base matemática de todo método de optimización.
- [[01 - Vectores]] — normas, usadas en la regularización.
- [[02 - Matrices]] — el Hessiano como matriz; álgebra matricial detrás de los métodos de segundo orden.
- [[01 - Funciones]] — qué función se está optimizando (la función de costo).

---
