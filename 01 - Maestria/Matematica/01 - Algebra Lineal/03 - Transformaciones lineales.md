---
titulo: Transformaciones lineales
materia: Matemática
tipo: apunte
fecha: 2026-08-01
tags:
  - matematica
  - maestria
  - algebra-lineal
  - ciencia-de-datos
  - mlops
  - tema/transformaciones-lineales
---

## ¿Qué es una transformación lineal?

Una **transformación lineal** es una [[01 - Funciones|función]] $T: \mathbb{R}^n \rightarrow \mathbb{R}^m$ que **preserva** las dos operaciones básicas de los [[01 - Vectores|vectores]]:

$$T(\mathbf{u} + \mathbf{v}) = T(\mathbf{u}) + T(\mathbf{v}) \qquad \text{(preserva la suma)}$$
$$T(k\mathbf{u}) = k \, T(\mathbf{u}) \qquad \text{(preserva la multiplicación por escalar)}$$

En criollo: si transformás dos vectores y después los sumás, da lo mismo que sumarlos primero y transformar el resultado. La transformación "respeta" la estructura vectorial.

> [!tip] Consecuencia importante
> Toda transformación lineal manda el vector nulo al vector nulo ($T(\mathbf{0}) = \mathbf{0}$), y las rectas que pasan por el origen siguen siendo rectas que pasan por el origen después de transformarlas.

## Representación matricial

> [!important] El resultado central del álgebra lineal
> Toda transformación lineal entre espacios de dimensión finita se puede representar como la multiplicación por una **[[02 - Matrices|matriz]]**:
> $$T(\mathbf{x}) = A\mathbf{x}$$
> Aplicar la transformación $T$ a un vector es, ni más ni menos, multiplicar la matriz $A$ por ese vector. *Fuente: [[mml-book]], cap. 2.7 (Mapeos lineales).*

Esto significa que **estudiar transformaciones lineales es estudiar matrices**: cada columna de $A$ es la imagen de un vector de la base canónica bajo $T$.

## Ejemplos geométricos en 2D

| Transformación | Matriz (ejemplo) | Efecto |
|---|---|---|
| **Escalado** | $\begin{bmatrix} k & 0 \\ 0 & k \end{bmatrix}$ | Agranda ($k>1$) o achica ($k<1$) el vector, sin cambiar su dirección |
| **Rotación** (ángulo $\theta$) | $\begin{bmatrix} \cos\theta & -\sin\theta \\ \sin\theta & \cos\theta \end{bmatrix}$ | Gira el vector alrededor del origen |
| **Reflexión** (eje x) | $\begin{bmatrix} 1 & 0 \\ 0 & -1 \end{bmatrix}$ | Invierte el signo de una componente |
| **Cizalladura** (*shear*) | $\begin{bmatrix} 1 & k \\ 0 & 1 \end{bmatrix}$ | "Inclina" el espacio, como empujar la parte de arriba de un mazo de cartas |
| **Proyección** (sobre eje x) | $\begin{bmatrix} 1 & 0 \\ 0 & 0 \end{bmatrix}$ | Aplasta el vector sobre el eje x (colapsa una dimensión) |

## Composición de transformaciones = multiplicación de matrices

Si primero aplico la transformación $T_1$ (matriz $A$) y después $T_2$ (matriz $B$), el resultado combinado es otra transformación lineal, cuya matriz es el producto $BA$:

$$T_2(T_1(\mathbf{x})) = B(A\mathbf{x}) = (BA)\mathbf{x}$$

> [!warning]
> Como la multiplicación de matrices **no es conmutativa** (ver [[02 - Matrices]]), el **orden** en que se aplican las transformaciones importa: rotar y después escalar no es lo mismo que escalar y después rotar.

## La conexión con las redes neuronales

Cada capa de una red neuronal calcula:

$$\mathbf{y} = W\mathbf{x} + \mathbf{b}$$

El término $W\mathbf{x}$ es exactamente una **transformación lineal** aplicada al vector de entrada (la matriz de pesos $W$ rota, escala y proyecta el espacio de entrada). Sumar $\mathbf{b}$ agrega una **traslación** — la combinación de una transformación lineal más una traslación se llama **transformación afín**. Después se aplica una [[01 - Funciones|función de activación]] no lineal, que es justamente lo que le impide a la red entera "colapsar" en una única transformación lineal gigante (componer transformaciones lineales da como resultado *otra* transformación lineal).

## Por qué esto importa para Data Science y MLOps

- **Cada capa de una red neuronal** es (hasta la activación) una transformación lineal: entender rotación/escalado/proyección da intuición geométrica de qué le "hace" una capa a los datos.
- **PCA** (*Principal Component Analysis*) encuentra una transformación lineal (una rotación) que reordena los ejes según la dirección de mayor varianza de los datos.
- **Embeddings**: transformar datos crudos (texto, imágenes) a un espacio vectorial de menor dimensión suele implicar una cadena de transformaciones lineales y no lineales.

## Temas relacionados

- [[01 - Vectores]] — lo que las transformaciones lineales transforman.
- [[02 - Matrices]] — la herramienta que representa y ejecuta toda transformación lineal.
- [[01 - Funciones]] — las transformaciones lineales son un caso particular (y central) de función.
- [[03 - Optimizacion]] — cómo se ajustan las matrices de una transformación (los pesos) durante el entrenamiento.

---
