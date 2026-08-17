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

donde $\arg\min$ ("el argumento que minimiza") no es el valor mínimo de $J$, sino **el valor de $\mathbf{w}$** que produce ese mínimo — la pregunta no es "¿cuál es el costo más bajo posible?" sino "¿con qué parámetros se logra ese costo más bajo?". $\mathbf{w}^*$ es, entonces, el conjunto de parámetros óptimo que se busca al entrenar un modelo.

## Puntos críticos y tipos de mínimo

Un **punto crítico** es donde el [[02 - Derivadas|gradiente]] se anula: $\nabla J(\mathbf{w}) = 0$. Ahí la función no crece ni decrece en ninguna dirección — puede ser un mínimo, un máximo o un **punto de silla**.

- **Mínimo local** → el valor más bajo en un entorno cercano, pero no necesariamente en todo el dominio.
- **Mínimo global** → el valor más bajo posible en todo el dominio.
- **Función convexa** → tiene un único mínimo, que es automáticamente global. Es el caso "fácil": no hay mínimos locales que puedan engañar al algoritmo.
- **Función no convexa** → puede tener múltiples mínimos locales. La mayoría de las redes neuronales entrenan funciones de costo no convexas.

> [!warning]
> En la práctica de deep learning casi nunca se garantiza llegar al mínimo global; se busca un mínimo local **suficientemente bueno**.

> [!definition] Convexidad, formalmente
> Una función $f$ es **convexa** si, para cualquier par de puntos $x,y$ de su dominio y cualquier $\theta\in[0,1]$:
> $$f(\theta x + (1-\theta)y) \le \theta f(x) + (1-\theta)f(y)$$
> En criollo: el **segmento de recta** que une dos puntos cualquiera de la curva siempre queda **por encima o sobre** la curva misma — nunca por debajo. Una parábola $f(x)=x^2$ es el ejemplo clásico; una curva con una "joroba" en el medio no lo es. Si $f$ es dos veces derivable, hay un criterio equivalente y más fácil de chequear: $f$ es convexa si y solo si su [[02 - Derivadas|Hessiano]] es semidefinido positivo en todo el dominio — la misma condición que ya usa esta nota para reconocer un mínimo local, pero exigida en **todos** los puntos a la vez, no solo en el punto crítico. *Fuente: [[mml-book]], cap. 7.3.*

## Por qué no alcanza con resolver $\nabla J(\mathbf{w}) = 0$ directamente

La sección anterior dice que el mínimo está donde el gradiente se anula — en principio, entonces, "resolver la optimización" sería plantear esa ecuación y despejar $\mathbf{w}$ analíticamente, como se hace con una parábola en el colegio. Para algunos problemas eso funciona: la regresión lineal por mínimos cuadrados tiene una solución cerrada exacta ($\hat{\beta} = (X^TX)^{-1}X^Ty$, ver [[02 - Matrices]]) — y vale la pena verla derivada una vez, porque esa fórmula aparece citada en varias notas del vault sin que nunca se muestre de dónde sale.

> [!example] Derivación completa: por qué $\hat\beta=(X^TX)^{-1}X^Ty$ minimiza el error
> El problema es encontrar el vector de coeficientes $\beta$ que minimiza la suma de errores al cuadrado entre los valores observados $y$ y las predicciones $X\beta$ (con $X$ la matriz de diseño: una fila por observación, una columna por predictora — ver [[04 - Sistemas de ecuaciones lineales]]):
> $$J(\beta) = \|y-X\beta\|^2 = (y-X\beta)^T(y-X\beta)$$
>
> **Paso 1 — expandir el cuadrado.** Distribuyendo la transpuesta y el producto:
> $$J(\beta) = y^Ty - y^TX\beta - \beta^TX^Ty + \beta^TX^TX\beta$$
> Como $y^TX\beta$ es un escalar (un número de 1×1), es igual a su propia transpuesta: $y^TX\beta = \beta^TX^Ty$. Los dos términos del medio son entonces iguales, y se combinan:
> $$J(\beta) = y^Ty - 2\beta^TX^Ty + \beta^TX^TX\beta$$
>
> **Paso 2 — derivar respecto de $\beta$.** Hacen falta dos reglas de derivación vectorial (análogas a "la derivada de $kx$ es $k$" y "la derivada de $ax^2$ es $2ax$", pero para vectores):
> $$\frac{\partial}{\partial\beta}\big(\beta^Ta\big) = a \qquad\qquad \frac{\partial}{\partial\beta}\big(\beta^TA\beta\big) = 2A\beta \;\; \text{(si $A$ es simétrica)}$$
> Con $a=X^Ty$ y $A=X^TX$ (que es simétrica: $(X^TX)^T=X^TX^{TT}=X^TX$):
> $$\nabla_\beta J(\beta) = -2X^Ty + 2X^TX\beta$$
> *Fuente: [[mml-book]], cap. 9.2.1 y cap. 5.5 (reglas de derivación vectorial).*
>
> **Paso 3 — igualar a cero y despejar.** En el mínimo, el gradiente se anula:
> $$-2X^Ty + 2X^TX\beta = 0 \;\Longrightarrow\; X^TX\beta = X^Ty \;\Longrightarrow\; \hat\beta = (X^TX)^{-1}X^Ty$$
>
> Verificado numéricamente sobre un dataset mínimo ($X$ con intercepto y una predictora, 3 observaciones): el gradiente calculado con la fórmula de arriba coincide con el gradiente numérico (por diferencias finitas) en cualquier $\beta$, y vale exactamente cero en el $\hat\beta$ que da la fórmula cerrada — confirmando que la derivación es correcta, no solo plausible.
>
> Esta misma fórmula tiene, además, una segunda derivación completamente distinta y igual de válida: **geométrica**, viendo $X\hat\beta$ como la [[05 - Proyecciones ortogonales|proyección ortogonal]] de $y$ sobre el espacio que generan las columnas de $X$. Ver esa nota para el desarrollo completo — llegar a la misma fórmula por dos caminos independientes (cálculo acá, geometría ahí) es una buena señal de que no es una coincidencia algebraica.

Pero en la mayoría de los modelos de Machine Learning eso deja de ser viable por dos razones concretas:

1. **No hay forma cerrada.** $J(\mathbf{w})$ suele ser una composición de muchas funciones no lineales (capas de una red neuronal, funciones de activación, ver [[01 - Funciones]]) — al plantear $\nabla J(\mathbf{w}) = 0$ se obtiene un sistema de ecuaciones que, en general, no tiene una fórmula algebraica que lo despeje.
2. **La escala lo hace imposible aunque existiera.** Un modelo puede tener millones de parámetros; incluso si hubiera una forma cerrada, resolverla exigiría invertir matrices de un tamaño que ninguna computadora maneja en un tiempo razonable.

La alternativa es no intentar saltar directo al mínimo, sino **acercarse a él de a pasos**, usando el gradiente en el punto actual como guía de hacia dónde moverse. Eso es exactamente lo que hace el descenso por gradiente.

## Descenso por gradiente (*gradient descent*)

El algoritmo de optimización más usado en ML. La idea: moverse repetidamente en la dirección **opuesta al gradiente** (la de máximo decrecimiento, ver [[02 - Derivadas]]):

$$\mathbf{w}_{t+1} = \mathbf{w}_t - \eta \, \nabla J(\mathbf{w}_t)$$

donde $\eta$ (*eta*) es la **tasa de aprendizaje** (*learning rate*): qué tan grande es cada paso. *Fuente: [[mml-book]], cap. 7.1 (Optimización con descenso por gradiente).*

> [!tip] El learning rate importa muchísimo
> - Muy **chico** → converge, pero muy lentamente.
> - Muy **grande** → puede "saltar" por encima del mínimo y no converger, o directamente diverger.

### Variantes habituales

- **SGD (*Stochastic Gradient Descent*)**: cuando la función de costo es una suma sobre $n$ datos, $J(\mathbf w)=\sum_{i=1}^n J_i(\mathbf w)$, calcular el gradiente completo en cada paso exige recorrer los $n$ datos — caro si $n$ es grande. SGD aproxima el gradiente completo usando solo un subconjunto (*batch*) de datos en cada paso:
  $$\mathbf w_{t+1} = \mathbf w_t - \eta\sum_{i\in\text{batch}} \nabla J_i(\mathbf w_t)$$
  Funciona porque ese gradiente parcial es un **estimador insesgado** del gradiente completo: en promedio, sobre muchos batches distintos, apunta en la misma dirección — no es un atajo que sacrifica corrección, es una aproximación estadísticamente válida. *Fuente: [[mml-book]], cap. 7.1.3.*
- **Momentum**: acumula una "inercia" $\Delta\mathbf w$ de los pasos anteriores, para no frenar de golpe ante cada cambio de pendiente:
  $$\Delta\mathbf w_t = \alpha\,\Delta\mathbf w_{t-1} - \eta\,\nabla J(\mathbf w_t) \qquad\qquad \mathbf w_{t+1} = \mathbf w_t + \Delta\mathbf w_t$$
  con $\alpha\in[0,1)$ controlando cuánto "recuerda" del paso anterior — acelera la convergencia en valles largos y angostos, y suaviza oscilaciones. *Fuente: [[mml-book]], cap. 7.1.2.*
- **Adam**: combina momentum con una tasa de aprendizaje adaptativa por parámetro; es el optimizador por defecto en la mayoría de los frameworks de deep learning actuales. (No desarrollado en detalle acá — mml-book no lo cubre; queda para cuando el vault llegue a una nota dedicada de deep learning.)

## Métodos de segundo orden

El gradient descent solo usa la **primera derivada** (el gradiente). Los métodos de segundo orden (como el **método de Newton**) usan además el **Hessiano** (ver [[02 - Derivadas]] y [[02 - Matrices]]) para aprovechar información sobre la **curvatura** de la función y converger en menos pasos. Son más precisos pero mucho más costosos de calcular en modelos con millones de parámetros — por eso en deep learning se usan casi exclusivamente métodos de primer orden (SGD, Adam).

## Regularización: un problema de optimización con restricciones

Muchas funciones de costo se modifican agregando un término de penalización sobre los parámetros, para evitar el sobreajuste (*overfitting*):

$$J_{\text{reg}}(\mathbf{w}) = J(\mathbf{w}) + \lambda \, \|\mathbf{w}\|$$

Usando la [[01 - Vectores|norma]] L1 (Lasso) o L2 (Ridge) del vector de parámetros. Optimizar esta versión "regularizada" empuja a los parámetros hacia valores más chicos o más dispersos (más ceros), según la norma elegida.

> [!note] De dónde sale exactamente ese término $\lambda\|\mathbf w\|$
> El problema que en realidad se quiere resolver no es "minimizar $J(\mathbf w)+\lambda\|\mathbf w\|$" (eso ya es la solución) sino "minimizar $J(\mathbf w)$ **sujeto a** que $\|\mathbf w\|$ no supere cierto límite $t$" — mantener los parámetros acotados. Para pasar de una restricción a un término de penalización se usa un **multiplicador de Lagrange**: se arma una nueva función, el **Lagrangiano**, que combina el objetivo original con la restricción escrita como "$\le 0$":
> $$L(\mathbf w,\lambda) = J(\mathbf w) + \lambda\big(\|\mathbf w\| - t\big), \qquad \lambda \ge 0$$
> Para un $\lambda$ fijo, minimizar $L$ respecto de $\mathbf w$ es lo mismo que minimizar $J(\mathbf w)+\lambda\|\mathbf w\|$: el término $-\lambda t$ no depende de $\mathbf w$, así que no cambia dónde está el mínimo — y esa es, literalmente, la fórmula regularizada de arriba. $\lambda$ deja de ser "un número que se agrega porque sí" y pasa a ser el multiplicador que traduce la restricción "$\mathbf w$ no puede crecer demasiado" en un costo que se paga por cada unidad de norma. *Fuente: [[mml-book]], cap. 7.2.*

## Por qué esto importa para Data Science y MLOps

- **Entrenar cualquier modelo** (regresión, redes neuronales, boosting) es, en el fondo, resolver un problema de optimización.
- **Elegir el learning rate y el optimizador** es una de las decisiones prácticas más frecuentes al entrenar una red neuronal.
- **Diagnosticar un entrenamiento que no converge** (pérdida que oscila, que no baja, que diverge) requiere entender estos conceptos: tasa de aprendizaje, convexidad, mínimos locales.

## Temas relacionados

- [[02 - Derivadas]] — el gradiente y el Hessiano, la base matemática de todo método de optimización.
- [[01 - Vectores]] — normas, usadas en la regularización.
- [[02 - Matrices]] — el Hessiano como matriz; álgebra matricial detrás de los métodos de segundo orden.
- [[04 - Sistemas de ecuaciones lineales]] y [[05 - Proyecciones ortogonales]] — la misma fórmula de mínimos cuadrados, vista desde el álgebra lineal.
- [[01 - Funciones]] — qué función se está optimizando (la función de costo).

---
