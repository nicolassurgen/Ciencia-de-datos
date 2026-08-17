---
titulo: Derivadas
materia: Matemática
tipo: apunte
fecha: 2026-08-01
tags:
  - matematica
  - maestria
  - calculo
  - ciencia-de-datos
  - mlops
  - tema/derivadas
---

## ¿Qué problema resuelve?

Saber que una función "crece" no alcanza para entrenar un modelo: hace falta saber **cuánto** crece, y en qué dirección moverse para hacer que decrezca lo más rápido posible (la idea detrás de ajustar los parámetros de un modelo para reducir su error). Para eso hace falta una noción precisa de **qué tan rápido** cambia una función en un punto exacto.

### De la tasa de cambio promedio a la instantánea

La forma más simple de medir "qué tan rápido cambia" $f$ entre dos puntos $x$ y $x+h$ es la pendiente de la recta que los une (la **recta secante**):

$$\text{tasa de cambio promedio} = \frac{f(x+h) - f(x)}{h}$$

donde:
- $f(x+h) - f(x)$ es cuánto cambió la salida;
- $h$ es cuánto cambió la entrada;
- el cociente es "cuánto cambia la salida por cada unidad que cambia la entrada", en promedio, en ese tramo.

El problema es que esto describe el cambio **en un tramo**, no en un punto. Para obtener la tasa de cambio **en el punto** $x$, la idea es achicar $h$ cada vez más: si $h$ tiende a 0, el tramo $[x, x+h]$ colapsa sobre el punto $x$, y la recta secante se convierte en la recta **tangente** a la curva en ese punto exacto. Esa tasa de cambio instantánea es la **derivada**:

$$f'(x) = \lim_{h \to 0} \frac{f(x+h) - f(x)}{h}$$

## ¿Qué es una derivada?

La **derivada** de una función en un punto mide su **tasa de cambio instantánea**: cuánto varía la salida ante un cambio infinitesimal en la entrada — el límite construido arriba.

> [!tip] Interpretación geométrica
> $f'(x)$ es la **pendiente de la recta tangente** a la curva de $f$ en el punto $x$ (el límite de la pendiente de la secante, a medida que el segundo punto se acerca al primero). Si $f'(x) > 0$, la función crece ahí; si $f'(x) < 0$, decrece; si $f'(x) = 0$, el punto es "plano" (posible mínimo, máximo o punto de inflexión).

## Reglas básicas

| Regla | Fórmula |
|---|---|
| Potencia | $\dfrac{d}{dx} x^n = n x^{n-1}$ |
| Suma | $(f+g)' = f' + g'$ |
| Producto | $(fg)' = f'g + fg'$ |
| **Regla de la cadena** | $\dfrac{d}{dx} f(g(x)) = f'(g(x)) \cdot g'(x)$ |

> [!tip] La regla de la cadena es la más importante para ML
> Permite derivar una [[01 - Funciones|composición de funciones]]. Una red neuronal es una composición de capas, y el algoritmo de **backpropagation** no es más que aplicar la regla de la cadena repetidamente, de la última capa hacia la primera, para saber cuánto contribuye cada parámetro al error final.

## Derivadas parciales

Cuando una función depende de **varias variables** ($f: \mathbb{R}^n \rightarrow \mathbb{R}$), se puede derivar respecto de **una sola variable a la vez**, tratando a las demás como constantes. Eso es una **derivada parcial**:

$$\frac{\partial f}{\partial x_i}$$

**Ejemplo** — con $f(x, y) = x^2 y + 3y$:

$$\frac{\partial f}{\partial x} = 2xy \qquad \frac{\partial f}{\partial y} = x^2 + 3$$

## El gradiente

> [!definition] Gradiente
> El **gradiente** de una función escalar de varias variables es el **vector** que agrupa todas sus derivadas parciales:
> $$\nabla f = \left( \frac{\partial f}{\partial x_1}, \frac{\partial f}{\partial x_2}, \dots, \frac{\partial f}{\partial x_n} \right)$$
> *Fuente: [[mml-book]], cap. 5.2 (Diferenciación parcial y gradientes).*

> [!tip] Propiedad clave
> El gradiente **apunta en la dirección de máximo crecimiento** de la función. Su opuesto, $-\nabla f$, apunta en la dirección de **máximo decrecimiento** — la dirección exacta que conviene seguir para minimizar una función. Esa es la idea completa detrás del **descenso por gradiente** (ver [[03 - Optimizacion]]).

Como el gradiente es un [[01 - Vectores|vector]], hereda todas sus operaciones: norma (¿qué tan "empinada" es la función en ese punto?), producto escalar, etc.

## La Jacobiana: cuando la salida también es un vector

El gradiente sirve para $f:\mathbb R^n\to\mathbb R$ (varias entradas, **una** salida). [[01 - Funciones]] ya menciona que cuando la salida **también** es un vector ($f:\mathbb R^n\to\mathbb R^m$ — el caso de una capa de red neuronal, o de cualquier transformación que produce varios números a la vez), el comportamiento local se describe con una **matriz Jacobiana** en vez de un vector gradiente. Esta sección cumple esa promesa.

> [!definition] Matriz Jacobiana
> Para $f:\mathbb R^n\to\mathbb R^m$, con $f(\mathbf x)=(f_1(\mathbf x),\dots,f_m(\mathbf x))$, la Jacobiana es la matriz $m\times n$ que junta **todas** las derivadas parciales de **todas** las salidas respecto de **todas** las entradas:
> $$J = \frac{\partial f}{\partial \mathbf x} = \begin{bmatrix} \dfrac{\partial f_1}{\partial x_1} & \cdots & \dfrac{\partial f_1}{\partial x_n} \\ \vdots & \ddots & \vdots \\ \dfrac{\partial f_m}{\partial x_1} & \cdots & \dfrac{\partial f_m}{\partial x_n} \end{bmatrix}$$
> Cada **fila** $i$ es el gradiente de $f_i$ (la salida $i$-ésima) respecto de todas las entradas — la Jacobiana es, literalmente, "un gradiente por cada salida, apilados". *Fuente: [[mml-book]], cap. 5.3.*

**El caso más importante en la práctica**, y el que conecta directo con [[02 - Matrices|transformaciones lineales]]: si $f(\mathbf x) = A\mathbf x$ (una transformación lineal, matriz $A$ fija), entonces:

$$\frac{\partial (A\mathbf x)}{\partial \mathbf x} = A$$

Es decir, **la Jacobiana de una transformación lineal es la matriz que la define** — no hay nada que "derivar" en el sentido usual, la matriz ya describe exactamente cómo cambia cada salida ante cada entrada, en cualquier punto. Verificado numéricamente (Jacobiana calculada por diferencias finitas vs. la matriz $A$ original de una transformación $\mathbb R^2\to\mathbb R^3$): coinciden exactamente. Esta es la regla que se usa constantemente al derivar $W\mathbf x+\mathbf b$ en una capa de red neuronal — es la razón por la que "la derivada de una capa lineal es la matriz de pesos" no es una casualidad de notación, es este resultado.

> [!tip] Otra lectura útil: el determinante de la Jacobiana como factor de escala
> Cuando $f:\mathbb R^n\to\mathbb R^n$ (misma cantidad de entradas que salidas), el [[02 - Matrices|determinante]] de la Jacobiana en un punto mide **en qué factor se expande o contrae** un volumen infinitesimal alrededor de ese punto al aplicar $f$. Es la pieza que falta para entender, más adelante, cómo cambia una densidad de probabilidad al transformar una variable aleatoria (cambio de variable).

## El Hessiano (segundas derivadas)

Así como el gradiente junta las **primeras** derivadas parciales en un vector, el **Hessiano** junta las **segundas** derivadas parciales en una [[02 - Matrices|matriz]]:

$$H_{i,j} = \frac{\partial^2 f}{\partial x_i \, \partial x_j}$$

El Hessiano describe la **curvatura** de la función: si es una matriz definida positiva en un punto donde el gradiente es cero, ese punto es un **mínimo local**. Se usa en métodos de optimización de segundo orden (ver [[03 - Optimizacion]]).

> [!note] El Hessiano siempre es simétrico
> $H_{i,j}=H_{j,i}$: derivar primero respecto de $x_i$ y después de $x_j$ da lo mismo que en el orden inverso (teorema de Schwarz/Clairaut, válido para cualquier función con segundas derivadas continuas — el caso normal en la práctica). Es la misma propiedad de simetría que ya aparece en la [[02 - Matrices|matriz de covarianza]], y no es casualidad: ambas son matrices que agrupan una relación "de a pares" sin un orden privilegiado entre los dos índices.

## Serie de Taylor y aproximación lineal local

Todo lo anterior —"el gradiente apunta a la dirección de máximo crecimiento", "el Hessiano describe la curvatura"— son afirmaciones sobre el comportamiento de $f$ **cerca** de un punto, no en toda la función. La herramienta que formaliza "cerca" es la serie de Taylor: aproximar una función complicada por un polinomio simple, construido a partir de sus derivadas en un único punto.

> [!definition] Aproximación lineal (primer orden)
> Cerca de un punto $\mathbf x_0$, cualquier función derivable se puede aproximar por su plano tangente:
> $$f(\mathbf x) \approx f(\mathbf x_0) + \nabla f(\mathbf x_0)^T(\mathbf x-\mathbf x_0)$$
> Es la generalización a varias variables de "cerca de un punto, una curva se parece a su recta tangente". *Fuente: [[mml-book]], cap. 5.8.*

Esta aproximación es la que justifica formalmente que el gradiente da la dirección de máximo crecimiento **localmente** — la fórmula de arriba dice que, para un paso chico $\Delta\mathbf x = \mathbf x - \mathbf x_0$, el cambio en $f$ es aproximadamente $\nabla f(\mathbf x_0)^T\Delta\mathbf x$, y ese producto se maximiza (para un paso de tamaño fijo) cuando $\Delta\mathbf x$ apunta en la misma dirección que $\nabla f(\mathbf x_0)$ — consecuencia directa de la fórmula del ángulo entre vectores (ver [[01 - Vectores]]).

Agregando el término cuadrático (con el Hessiano) se obtiene la **aproximación de segundo orden**:

$$f(\mathbf x) \approx f(\mathbf x_0) + \nabla f(\mathbf x_0)^T(\mathbf x-\mathbf x_0) + \tfrac12(\mathbf x-\mathbf x_0)^TH(\mathbf x_0)(\mathbf x-\mathbf x_0)$$

Esta es, exactamente, la aproximación que usa el **método de Newton** de [[03 - Optimizacion]]: en vez de dar un paso en la dirección del gradiente (como hace el descenso por gradiente), Newton minimiza directamente esta aproximación cuadrática — que, al ser una parábola, tiene un mínimo exacto y calculable, dando pasos más precisos a costa de tener que calcular y invertir el Hessiano en cada paso.

## Backpropagation: la regla de la cadena como algoritmo

La sección de "Reglas básicas" ya adelantó que backpropagation es "aplicar la regla de la cadena repetidamente". Vale la pena ver **cómo**, concretamente, sin quedarse solo en la analogía.

Una red neuronal calcula su salida como una cadena de operaciones intermedias — por ejemplo, para una expresión como $e = (a+b)\times c$, se puede descomponer en pasos:

```
a, b, c  -> entradas
d = a + b
e = d × c   -> salida
```

Este esquema (variables intermedias, cada una función de las anteriores) es un **grafo de cómputo**. Calcular $\frac{\partial e}{\partial a}$ requiere la regla de la cadena atravesando el grafo: $\frac{\partial e}{\partial a} = \frac{\partial e}{\partial d}\cdot\frac{\partial d}{\partial a}$. La pregunta de diseño es: ¿en qué **orden** conviene calcular estas derivadas parciales cuando hay muchísimas variables intermedias (como en una red con millones de parámetros)?

> [!important] Forward mode vs. reverse mode
> - **Modo hacia adelante** (*forward mode*): calcular las derivadas en el mismo orden que se calculó la función (de las entradas hacia la salida). Conviene cuando hay **pocas entradas** y muchas salidas.
> - **Modo hacia atrás** (*reverse mode*) — esto es **backpropagation**: calcular primero $\frac{\partial e}{\partial e}=1$, y propagar hacia atrás, reutilizando en cada paso lo ya calculado para la capa siguiente (más cercana a la salida). Conviene cuando hay **muchas entradas** (los millones de parámetros de una red) y **pocas salidas** (típicamente una: el valor de la función de costo) — que es exactamente la situación de entrenar un modelo. *Fuente: [[mml-book]], cap. 5.6.*
>
> La ventaja de reverse mode no es solo conceptual: evita recalcular la misma derivada parcial una y otra vez para cada parámetro por separado (el mismo problema de **trabajo redundante** que ya apareció en [[recursion y memoizacion]] de Algoritmos, resuelto ahí con memoización y acá con una estrategia de orden de cómputo). Por eso backpropagation es viable para entrenar redes con millones de parámetros, mientras que derivar "a mano, parámetro por parámetro" no lo sería.

## Por qué esto importa para Data Science y MLOps

- **Entrenamiento de modelos**: ajustar los parámetros de un modelo para minimizar una función de costo requiere saber en qué dirección moverse — eso es el gradiente.
- **Backpropagation**: aplica la regla de la cadena sobre la composición de funciones de una red neuronal para calcular el gradiente respecto de **cada** parámetro, capa por capa.
- **Convergencia**: la forma del Hessiano (su curvatura) ayuda a entender por qué algunos problemas de optimización son más difíciles o lentos de resolver que otros.

## Temas relacionados

- [[01 - Funciones]] — qué se está derivando; la composición de funciones detrás de backpropagation.
- [[01 - Vectores]] — el gradiente es un vector de derivadas parciales.
- [[02 - Matrices]] — el Hessiano es una matriz de segundas derivadas; la Jacobiana de una transformación lineal es la matriz que la define.
- [[03 - Optimizacion]] — cómo se usa el gradiente (y el Hessiano) para minimizar funciones; la aproximación de Taylor detrás del método de Newton.
- [[recursion y memoizacion]] de Algoritmos — el mismo problema de trabajo redundante que resuelve backpropagation con reverse mode.

---
