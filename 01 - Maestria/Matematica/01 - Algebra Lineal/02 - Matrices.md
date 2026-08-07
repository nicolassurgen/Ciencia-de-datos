---
titulo: Matrices
materia: Matemática
tipo: apunte
fecha: 2026-08-01
tags:
  - matematica
  - maestria
  - algebra-lineal
  - ciencia-de-datos
  - mlops
  - tema/matrices
---

## ¿Qué es una matriz?

Una **matriz** es un arreglo rectangular de escalares (números enteros, reales o complejos) dispuestos en filas y columnas. Por ejemplo:

$$ A = \begin{bmatrix} 10 & 20 & 30 \ 40 & 50 & 60 \end{bmatrix} $$

También se puede pensar una matriz como una **lista de [[01 - Vectores|vectores]]**: la matriz $A$ de arriba puede leerse como 2 vectores 3D horizontales (sus filas) o como 3 vectores 2D verticales (sus columnas).

> [!tip] Por qué importa en ciencia de datos
> Las matrices son la estructura natural para representar un **dataset completo** (filas = observaciones, columnas = features), los **pesos de una red neuronal**, y son extremadamente eficientes para ejecutar operaciones sobre muchos vectores a la vez (vectorización). También permiten representar [[03 - Transformaciones lineales|transformaciones lineales]] como rotaciones, traslaciones y cambios de escala.

## Tamaño de una matriz

El tamaño de una matriz se define por su número de filas y columnas, y se anota:

$$ \text{filas} \times \text{columnas} $$

Por ejemplo, la matriz $A$ anterior es una matriz de $2 \times 3$ (2 filas, 3 columnas).

> [!warning] Cuidado
> Una matriz de $3 \times 2$ no es lo mismo que una de $2 \times 3$. El orden importa: primero filas, después columnas.

## Indexación de elementos

El elemento ubicado en la fila $i$ y la columna $j$ de una matriz $X$ se anota $X_{i,j}$ (no hay una notación 100% estándar, pero esta es la más común y coincide con la notación de NumPy). En general:

$$ X = \begin{bmatrix} x_{1,1} & x_{1,2} & x_{1,3} & \cdots & x_{1,n} \ x_{2,1} & x_{2,2} & x_{2,3} & \cdots & x_{2,n} \ x_{3,1} & x_{3,2} & x_{3,3} & \cdots & x_{3,n} \ \vdots & \vdots & \vdots & \ddots & \vdots \ x_{m,1} & x_{m,2} & x_{m,3} & \cdots & x_{m,n} \end{bmatrix} $$

> [!note] Nota importante
> En matemática los índices suelen empezar en 1, pero en programación (Python/NumPy) empiezan en 0. Para acceder a $A_{2,3}$ en NumPy:
>
> ```python
> A[1, 2]   # fila índice 1, columna índice 2 -> 60
> ```
> (usando la matriz $A$ del ejemplo del principio: fila 1 es `[40, 50, 60]`, y su elemento de índice 2 es `60`)

### Vectores fila y columna

- El vector de la fila $i$-ésima se anota $M_{i,}$. Por ejemplo, $A_{2, }$ es el vector de la segunda fila de $A$: `A[1, :]`.
- El vector de la columna $j$-ésima se anota $M_{_,j}$. Por ejemplo, $A_{_,3}$ es el vector de la tercera columna de $A$: `A[:, 2]`.

> [!tip] Slicing para conservar la forma 2D
> En NumPy, el resultado de `A[1, :]` o `A[:, 2]` es un array unidimensional (no existe un "vector fila" o "vector columna" 2D por defecto). Si necesitás conservar la forma 2D (por ejemplo, para multiplicar matrices después), hay que usar slicing en lugar de indexado directo: `A[1:2, :]` o `A[:, 2:3]`.

## Tipos especiales de matrices

- **Matriz cuadrada**: tiene el mismo número de filas y columnas ($n \times n$). Ejemplo $3\times3$:

$$ \begin{bmatrix} 4 & 9 & 2 \\ 3 & 5 & 7 \\ 8 & 1 & 6 \end{bmatrix} $$

- **Matriz triangular**: matriz cuadrada donde todos los elementos por encima (triangular inferior) o por debajo (triangular superior) de la diagonal principal son cero.
- **Matriz diagonal**: matriz cuadrada donde todos los elementos fuera de la diagonal principal son cero.
- **Matriz identidad** ($I$): matriz diagonal cuyos elementos en la diagonal son todos 1. Es el "elemento neutro" de la multiplicación de matrices: $AI = IA = A$.

> [!tip] Aplicación práctica
> La matriz identidad aparece constantemente en álgebra lineal aplicada a ML — por ejemplo, en la regularización Ridge ($\lambda I$ sumado a una matriz de covarianza) o como punto de partida para inicializar transformaciones que no deforman el espacio.

## 5. Suma de matrices

Si dos matrices $Q$ y $R$ tienen el mismo tamaño $m \times n$, se pueden sumar elemento a elemento. El resultado es una matriz $S$, también de $m \times n$:

$$ S_{i,j} = Q_{i,j} + R_{i,j} $$

$$ S = \begin{bmatrix} Q_{11}+R_{11} & Q_{12}+R_{12} & \cdots & Q_{1n}+R_{1n} \\Q_{21}+R_{21} & Q_{22}+R_{22} & \cdots  & Q_{2n}+R_{2n} \\ \vdots & \vdots & \ddots & \vdots \\ Q_{m1}+R_{m1} & Q_{m2}+R_{m2} & \cdots & Q_{mn}+R_{mn} \end{bmatrix} $$

## Multiplicación por un escalar

Una matriz $M$ se puede multiplicar por un escalar $\lambda$. El resultado $\lambda M$ tiene el mismo tamaño que $M$, con todos sus elementos multiplicados por $\lambda$:

$$ (\lambda M)_{i,j} = \lambda \cdot M_{i,j} $$

En NumPy esto se hace simplemente con el operador `*`:

```python
lambda_escalar * M
```

## Multiplicación de matrices

Esta es la operación más importante y la menos intuitiva al principio.

Una matriz $Q$ de tamaño $m \times n$ se puede multiplicar por una matriz $R$ de tamaño $n \times q$ (⚠️ **el número de columnas de $Q$ debe coincidir con el número de filas de $R$**). El resultado es una matriz $P$ de tamaño $m \times q$:

$$ P_{i,j} = \sum_{k=1}^{n} Q_{i,k} \times R_{k,j} $$

Es decir: el elemento $P_{i,j}$ es la suma de los productos entre los elementos de la fila $i$ de $Q$ y los elementos de la columna $j$ de $R$.

### Conexión con el producto escalar

Cada elemento $P_{i,j}$ es en realidad el **producto escalar** (producto punto) entre el vector fila $Q_{i,}$ y el vector columna $R_{_,j}$:

$$ P_{i,j} = Q_{i,} \cdot R_{_,j} $$

Por lo que podemos reescribir $P$ de forma más compacta como:

$$ P = \begin{bmatrix} Q_{1,}\cdot R_{_,1} & Q_{1,}\cdot R_{_,2} & \cdots & Q_{1,}\cdot R_{_,q} \\ Q_{2,}\cdot R_{_,1} & Q_{2,}\cdot R_{_,2} & \cdots & Q_{2,}\cdot R_{_,q} \\ \vdots & \vdots & \ddots & \vdots \\ Q_{m,}\cdot R_{_,1} & Q_{m,}\cdot R_{_,2} & \cdots & Q_{m,}\cdot R_{_,q} \end{bmatrix} $$

> [!warning] Propiedad clave que rompe la intuición
> La multiplicación de matrices **no es conmutativa** en general: $QR \neq RQ$. Esto contrasta con la suma o la multiplicación de escalares, y es algo a tener muy presente al implementar redes neuronales o pipelines de transformaciones.

> [!tip] Por qué importa en ML/MLOps
> Cada capa de una red neuronal calcula básicamente $W \cdot x + b$, una multiplicación de matrices (los pesos $W$) por un vector (la entrada $x$). Cuando se procesa un _batch_ completo de ejemplos a la vez, $x$ se convierte en una matriz, y toda la operación sigue siendo una multiplicación de matrices — la base de por qué las GPUs (optimizadas para álgebra matricial) son tan importantes en deep learning.

## Matriz transpuesta

La transpuesta de una matriz $M$, denominada $M^T$, es la matriz donde la fila $i$ de $M^T$ es igual a la columna $i$ de $M$:

$$ A^T = \begin{bmatrix} 10 & 20 & 30 \ 40 & 50 & 60 \end{bmatrix}^T = \begin{bmatrix} 10 & 40 \ 20 & 50 \ 30 & 60 \end{bmatrix} $$

En otras palabras:

$$ (A^T)_{i,j} = A_{j,i} $$

Si $M$ es una matriz $m \times n$, entonces $M^T$ es una matriz $n \times m$.

> [!note] Otras notaciones que pueden aparecer
> $M^t$, $M'$ o $^tM$.

> [!tip] Aplicación práctica
> La transposición aparece todo el tiempo al ajustar dimensiones para que una multiplicación de matrices sea posible (por ejemplo, en la fórmula de mínimos cuadrados $\hat{\beta} = (X^TX)^{-1}X^Ty$, muy usada en regresión lineal).

## Representación geométrica

Así como los [[01 - Vectores|vectores]] se representan como puntos o flechas en un espacio $N$-dimensional, una matriz puede verse como una **lista de vectores**: graficar una matriz equivale a graficar varios puntos o flechas a la vez (una por cada fila o columna, según cómo se la interprete).

### Aplicaciones geométricas de las operaciones matriciales

Recordando lo visto con [[01 - Vectores|vectores]]:

- La **suma de vectores** produce una traslación geométrica.
- La **multiplicación por un escalar** produce un reescalado (centrado en el origen).
- El **producto escalar** produce una proyección de un vector sobre otro.

De manera análoga, las operaciones matriciales tienen interpretaciones geométricas potentes: una matriz puede representar (y ejecutar) una [[03 - Transformaciones lineales|transformación lineal]] completa sobre un espacio vectorial: rotaciones, reflexiones, escalados, cizalladuras (_shear_) y proyecciones.

## Matriz inversa

Si una matriz $F$ representa una transformación lineal, una pregunta natural es: ¿existe una matriz que **revierta** ese efecto? Cuando existe, se llama **inversa** de $F$ y se anota $F^{-1}$, y cumple:

$$ F \cdot F^{-1} = F^{-1} \cdot F = I $$

No todas las matrices tienen inversa (solo las matrices cuadradas cuyo determinante es distinto de cero, ver más abajo). Cuando una matriz no tiene inversa se la llama **singular**.

Ejemplos de transformaciones que sí tienen inversa: la rotación, el mapeo de corte (_shear_) y el mapeo de compresión/escalado (siempre que no colapsen una dimensión a cero).

> [!tip] Aplicación práctica clave
> La inversa de una matriz aparece en la solución analítica de la regresión lineal por mínimos cuadrados, en el cálculo de la matriz de covarianza inversa (usada en Mahalanobis distance), y conceptualmente en la idea de "deshacer" una transformación de datos (por ejemplo, revertir una normalización lineal). En la práctica de ML rara vez se calcula la inversa explícitamente por costo computacional y estabilidad numérica; se prefieren métodos como la descomposición LU, QR o SVD.

## Determinante

El **determinante** de una matriz cuadrada $M$, anotado $\det(M)$ o $|M|$, es un valor escalar que resume ciertas propiedades de la matriz (como si la transformación que representa conserva o invierte la orientación del espacio, y en qué factor escala el volumen).

Uno de los métodos para calcularlo es la **expansión recursiva por la primera columna**:

$$ |M| = M_{1,1}\times|M^{(1,1)}| - M_{2,1}\times|M^{(2,1)}| + M_{3,1}\times|M^{(3,1)}| - \cdots \pm M_{n,1}\times|M^{(n,1)}| $$

donde $M^{(i,j)}$ es la matriz $M$ sin la fila $i$ ni la columna $j$ (este submatriz se llama **menor**).

### Ejemplo: determinante de una matriz $3\times3$

$$ M = \begin{bmatrix} 1 & 2 & 3 \ 4 & 5 & 6 \ 7 & 8 & 0 \end{bmatrix} $$

Aplicando la fórmula:

$$ |M| = 1\times\begin{vmatrix}5 & 6\\8 & 0\end{vmatrix} - 2\times\begin{vmatrix}4 & 6\\7 & 0\end{vmatrix} + 3\times\begin{vmatrix}4 & 5\\7 & 8\end{vmatrix} $$

Calculamos cada menor de $2\times2$:

$$ \begin{vmatrix}5 & 6\\8 & 0\end{vmatrix} = 5\times0 - 6\times8 = -48 $$

$$ \begin{vmatrix}4 & 6\\7 & 0\end{vmatrix} = 4\times0 - 6\times7 = -42 $$

$$ \begin{vmatrix}4 & 5\\7 & 8\end{vmatrix} = 4\times8 - 5\times7 = -3 $$

Resultado final:

$$ |M| = 1\times(-48) - 2\times(-42) + 3\times(-3) = -48 + 84 - 9 = 27 $$

Como $|M| = 27 \neq 0$, esta matriz **es invertible**: representa una transformación que no colapsa el espacio a una dimensión menor (por ejemplo, no aplasta el plano 3D sobre un plano o una recta), y $M^{-1}$ existe. El signo positivo además indica que la transformación conserva la orientación del espacio.

### Propiedades clave del determinante

- $\det(M) = 0$ ⟺ la matriz **no tiene inversa** (es singular) ⟺ las filas/columnas son linealmente dependientes.
- $\det(M) \neq 0$ ⟺ la transformación que representa $M$ **no colapsa** el espacio (no pierde dimensiones).
- El signo del determinante indica si la transformación **invierte la orientación** del espacio (determinante negativo) o no.

> [!tip] Aplicación práctica
> El determinante se usa para verificar si una matriz es invertible antes de intentar calcular $M^{-1}$, y aparece en el cálculo de la función de densidad de la distribución normal multivariada, muy usada en modelos probabilísticos.

## Por qué esto importa para Data Science y MLOps

- **Representación de datasets**: un dataset tabular es una matriz $m \times n$ (m observaciones, n features).
- **Pesos de modelos**: las capas de redes neuronales, los coeficientes de regresión y los kernels de modelos lineales son matrices.
- **Transformaciones lineales**: PCA, whitening, rotaciones de embeddings y proyecciones a espacios de menor dimensión se ejecutan multiplicando por matrices (ver [[03 - Transformaciones lineales]]).
- **Optimización**: el Hessiano (matriz de segundas derivadas) usado en métodos de optimización de segundo orden es una matriz; entender su estructura ayuda a comprender la convergencia de algoritmos de entrenamiento (ver [[02 - Derivadas]] y [[03 - Optimizacion]]).
- **Funciones vectoriales**: cuando una función mapea un vector a otro vector (no a un escalar), su comportamiento local se describe con una matriz Jacobiana (ver [[01 - Funciones]]).
- **Eficiencia computacional**: las operaciones matriciales son la base de la vectorización en NumPy/PyTorch/TensorFlow, y son las que se ejecutan en paralelo masivo sobre GPU/TPU.

## Temas relacionados

- [[01 - Vectores]] — la base sobre la que se construyen las matrices (filas y columnas son vectores).
- [[03 - Transformaciones lineales]] — cómo las matrices ejecutan rotaciones, escalados y proyecciones.
- [[01 - Funciones]] — generalización del concepto de matriz a mapeos no necesariamente lineales.
- [[02 - Derivadas]] — el gradiente y el Hessiano como vectores/matrices de derivadas.
- [[03 - Optimizacion]] — uso de matrices (Hessiano, matrices de covarianza) en algoritmos de entrenamiento.

---