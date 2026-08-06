---
titulo: Funciones
materia: Matemática
tipo: apunte
fecha: 2026-08-01
tags:
  - matematica
  - maestria
  - calculo
  - ciencia-de-datos
  - mlops
  - tema/funciones
---

## ¿Qué es una función?

Una **función** es un mapeo que a cada elemento de un conjunto de entrada (el **dominio**) le asigna **exactamente un** elemento de un conjunto de salida (el **codominio**):

$$f: A \rightarrow B$$

El subconjunto del codominio que efectivamente se alcanza (los valores que la función realmente produce) es la **imagen** o **rango** de $f$.

> [!tip] Por qué importa en ciencia de datos
> Un modelo de Machine Learning **es**, en esencia, una función: toma una entrada (features) y produce una salida (predicción). Entrenar un modelo es buscar, dentro de una familia de funciones posibles, la que mejor se ajusta a los datos.

## Funciones escalares vs. funciones vectoriales

En ML conviene distinguir según qué tipo de salida (y de entrada) tiene la función:

| Tipo | Notación | Ejemplo |
|---|---|---|
| Escalar de una variable | $f: \mathbb{R} \rightarrow \mathbb{R}$ | $f(x) = x^2$ |
| Escalar de varias variables | $f: \mathbb{R}^n \rightarrow \mathbb{R}$ | Una función de costo $J(\mathbf{w})$ que toma un vector de pesos y devuelve un número |
| Vectorial (varias salidas) | $f: \mathbb{R}^n \rightarrow \mathbb{R}^m$ | Una capa de red neuronal: toma un [[01 - Vectores\|vector]] de entrada y devuelve un vector de salida |

> [!info] Conexión clave
> Cuando una función mapea un vector a otro vector (no a un escalar), su comportamiento local — cómo cambia la salida ante pequeños cambios en cada componente de la entrada — se describe con una **matriz Jacobiana**: la generalización del concepto de derivada a funciones vectoriales. Ver [[02 - Derivadas]] para el caso escalar (la base) antes de llegar ahí.

## Composición de funciones

Si $f: A \rightarrow B$ y $g: B \rightarrow C$, la **composición** $g \circ f: A \rightarrow C$ aplica primero $f$ y después $g$:

$$(g \circ f)(x) = g(f(x))$$

> [!tip] Por qué importa en ciencia de datos
> Una red neuronal de varias capas **es literalmente una composición de funciones**. Si cada capa $i$ aplica una [[03 - Transformaciones lineales|transformación lineal]] $L_i$ seguida de una función de activación $\sigma_i$, la red completa es:
> $$\text{red}(x) = \sigma_L(L_L(\dots \sigma_1(L_1(x))\dots))$$
> Entender la regla de la cadena para derivar composiciones es la base matemática del **backpropagation** (ver [[02 - Derivadas]]).

## Funciones habituales en Machine Learning

### Función lineal

$$f(x) = wx + b$$

La base de la regresión lineal y de cada "neurona" antes de aplicar la activación (ver [[03 - Transformaciones lineales]] para la versión vectorial/matricial: $f(\mathbf{x}) = W\mathbf{x} + \mathbf{b}$).

### Función sigmoide (logística)

$$\sigma(x) = \frac{1}{1 + e^{-x}}$$

Comprime cualquier número real al intervalo $(0, 1)$. Se usa para convertir una salida en una **probabilidad** (regresión logística, capa de salida en clasificación binaria) y como función de activación clásica.

### ReLU (*Rectified Linear Unit*)

$$\text{ReLU}(x) = \max(0, x)$$

La función de activación más usada en redes profundas hoy: es simple, barata de calcular y evita algunos problemas de entrenamiento (*vanishing gradient*) que tenía la sigmoide en redes muy profundas.

### Softmax

$$\text{softmax}(\mathbf{x})_i = \frac{e^{x_i}}{\sum_{j} e^{x_j}}$$

Toma un vector de números reales y lo convierte en una **distribución de probabilidad** (valores en $(0,1)$ que suman 1). Es la función de activación estándar en la capa de salida de un clasificador multiclase.

> [!note] Nota
> Todas estas son **funciones de activación**: se aplican después de una transformación lineal para introducir **no linealidad**. Sin ellas, componer muchas capas lineales seguiría siendo, en el fondo, una única transformación lineal — la no linealidad es lo que le da a una red neuronal su poder expresivo.

## Por qué esto importa para Data Science y MLOps

- **Un modelo es una función**: entrenar = ajustar los parámetros de una función (o composición de funciones) para que se aproxime a los datos observados.
- **Funciones de activación**: introducen la no linealidad que permite a las redes neuronales aproximar relaciones complejas, no solo lineales.
- **Funciones de costo/pérdida**: funciones escalares ($f: \mathbb{R}^n \rightarrow \mathbb{R}$) que miden qué tan mal predice el modelo; el proceso de [[03 - Optimizacion|optimización]] busca minimizarlas.
- **Backpropagation**: aplica la regla de la cadena sobre la composición de funciones de una red para calcular cómo ajustar cada parámetro.

## Temas relacionados

- [[01 - Vectores]] — el tipo de entrada/salida de una función vectorial.
- [[02 - Derivadas]] — cómo cambia una función; base del gradiente y la Jacobiana.
- [[03 - Transformaciones lineales]] — el caso particular de las funciones lineales, representables con matrices.
- [[03 - Optimizacion]] — cómo se usa el comportamiento de una función (su gradiente) para minimizarla.

---
