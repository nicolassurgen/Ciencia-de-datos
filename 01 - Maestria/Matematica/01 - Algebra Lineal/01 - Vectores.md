---
titulo: Vectores
materia: Matemática
tipo: apunte
fecha: 2026-08-01
tags:
  - matematica
  - maestria
  - algebra-lineal
  - ciencia-de-datos
  - mlops
  - tema/vectores
---

## ¿Qué es un vector?

El concepto de **vector** tiene dos lecturas complementarias que conviene tener claras desde el principio, porque en ciencia de datos se mezclan todo el tiempo:

- **Vector matemático**: un segmento de recta orientado, definido respecto a un sistema de coordenadas, sobre el que se pueden realizar operaciones (suma, producto escalar, normas, etc.).
- **Vector computacional**: un arreglo unidimensional, es decir, una colección finita y ordenada de datos del mismo tipo (lo que en Python sería un `array` de NumPy o una fila/columna de un `DataFrame`).

Estrictamente hablando, no son lo mismo. Pero en la práctica, un vector computacional se comporta como un vector matemático lo suficiente como para que valga la pena importar toda la intuición geométrica y las operaciones del álgebra lineal hacia las estructuras de datos que usamos en ML.

> [!tip] Por qué importa en ciencia de datos
> Cada observación de un dataset (una fila de tu `DataFrame`), cada embedding de texto o imagen, cada conjunto de pesos de una red neuronal, son vectores. Pensar en términos vectoriales es la base de todo: desde la regresión lineal hasta los transformers.

## Definición matemática

Un vector representa magnitudes que tienen **dirección e intensidad**, a diferencia de las magnitudes escalares (que solo tienen magnitud, como la temperatura o el precio). Ejemplos físicos: fuerza, velocidad, desplazamiento.

### Características geométricas de un vector

| Propiedad               | Descripción                                                                      |
| ----------------------- | -------------------------------------------------------------------------------- |
| **Dirección**           | La recta sobre la que está situado el vector (o cualquier recta paralela a ella) |
| **Sentido**             | La orientación del vector, indicada por su flecha                                |
| **Módulo**              | La longitud del vector; corresponde a su valor numérico                          |
| **Punto de aplicación** | El origen del vector                                                             |

### Representación numérica

Además de representarse gráficamente como flechas, los vectores se representan numéricamente mediante sus **componentes (o coordenadas)**.

**Convenciones importantes:**

- Los vectores suelen escribirse como **columnas**.
- Se nombran con minúsculas y en **negrita** (𝐮, 𝐯) para diferenciarlos de las [[02 - Matrices|matrices]] (que suelen ser mayúsculas) y de los escalares simples.

**Ejemplo — velocidad de un cohete** (vector tridimensional):

Si un cohete asciende con una velocidad vertical de 5000 m/s, una componente este de 10 m/s y una componente norte de 50 m/s, su vector velocidad es:

```
velocidad = [10, 50, 5000]
```

La magnitud de este vector es la rapidez del cohete, y su dirección es hacia dónde apunta esa flecha en el espacio 3D.

## Definición en computación

En computación, un vector es un **arreglo unidimensional**: una colección finita y ordenada de elementos del mismo tipo.

### Uso en Machine Learning

Los vectores computacionales se usan masivamente para representar tanto **observaciones** (inputs) como **predicciones**(outputs) de un modelo.

**Ejemplo — clasificación de videos** (bueno / spam / clickbait):

Cada video se representa como un vector de _features_:

```
video = [10.5, 5.2, 3.25, 7.0]
```

Donde cada componente tiene un significado distinto:

- `10.5` → duración en minutos
- `5.2` → % de espectadores que ven más de 1 minuto
- `3.25` → promedio de vistas por día
- `7.0` → veces marcado como spam

A partir de este vector de entrada, un modelo predice un vector de salida (probabilidades):

```
probabilidades_de_clase = [0.80, 0.18, 0.02]ᵀ
```

→ 80% spam, 18% clickbait, 2% buen video.

> [!tip] Conexión con redes neuronales
> Esta lógica de "vector de entrada → [[01 - Funciones|función]] → vector de salida" es exactamente lo que hace una capa de una red neuronal, y se generaliza con [[03 - Transformaciones lineales|transformaciones lineales]] cuando trabajamos con varias salidas a la vez (de ahí la conexión directa con [[02 - Matrices|matrices]]).

## Norma de un vector

La **norma** de un vector 𝐮, anotada ‖𝐮‖, mide su longitud o magnitud. La más usada es la **norma euclidiana** (también llamada norma L2):

$$||u|| = \sqrt{\sum_i u_i^2}$$

Es decir, la raíz cuadrada de la suma de los cuadrados de sus componentes (generalización del teorema de Pitágoras a n dimensiones). *Fuente: [[mml-book]], cap. 3.1 (Normas) y cap. 3.2 (Producto interno).*

> [!note] Otras normas usadas en la práctica
> Existen otras normas muy usadas en la práctica que conviene tener mapeadas aunque no se hayan visto formalmente todavía:
>
> - **Norma L1** (Manhattan): `Σᵢ |uᵢ|` → usada en regularización Lasso.
> - **Norma L2** (Euclidiana): la de arriba → usada en regularización Ridge y en casi todo cálculo de distancias.
> - **Norma L∞**: el máximo valor absoluto de las componentes. Estas normas son centrales en problemas de [[03 - Optimizacion|optimizacion]] (funciones de costo regularizadas) y en medir distancias entre embeddings.

## Operaciones con vectores

### Adición

Solo se pueden sumar vectores del **mismo tamaño** (misma dimensión). La suma se hace **elemento a elemento**:


$$u + v = [u_1 + v_1, u_2 + v_2, ..., u_n +v_n]$$

Geométricamente, equivale a poner un vector a continuación del otro ("regla del paralelogramo" o "punta con cola").

### Multiplicación por un escalar

Al multiplicar un vector por un número (escalar), **todos sus elementos se multiplican** por ese número:

```
k · u = [k·u₁, k·u₂, ..., k·uₙ]
```

Geométricamente, esto **escala** el vector (lo alarga, lo achica o invierte su sentido si `k` es negativo), pero no cambia su dirección.

> [!note] Combinación lineal
> Estas dos operaciones (suma y producto por escalar) son las que definen lo que en álgebra lineal se llama una **combinación lineal**, concepto que después se conecta directamente con [[03 - Transformaciones lineales|transformaciones lineales]].

## Tipos especiales de vectores

- **Vector nulo**: vector lleno de ceros. `‖0‖ = 0`.
- **Vector unitario**: vector cuya norma es igual a 1.
- **Vector normalizado**: dado un vector no nulo 𝐮, su versión normalizada 𝐮̂ es el vector unitario que apunta en la misma dirección que 𝐮:

```
û = u / ‖u‖
```

> [!tip] Aplicación práctica
> Normalizar vectores es habitual antes de calcular similitud coseno entre embeddings, o como paso de preprocesamiento de features en muchos pipelines de ML.

## Producto escalar (producto punto)

El **producto escalar** (o producto punto) de dos vectores 𝐮 y 𝐯 se anota 𝐮·𝐯 (o ⟨𝐮|𝐯⟩) y tiene dos formas equivalentes de calcularse:

**Forma geométrica:**

```
u · v = ‖u‖ × ‖v‖ × cos(θ)
```

donde `θ` es el ángulo entre ambos vectores.

**Forma algebraica (componente a componente):**

```
u · v = Σᵢ uᵢ × vᵢ
```

### Lecturas clave del producto escalar

- Si `u · v = 0` → los vectores son **ortogonales** (perpendiculares).
- El signo del producto escalar indica si el ángulo entre vectores es agudo (positivo), obtuso (negativo) o recto (cero).
- Es la operación base detrás de la **similitud coseno**, ampliamente usada para comparar embeddings de texto, usuarios o productos.

> [!important] La fórmula que conecta ambas lecturas: el ángulo entre dos vectores
> Despejando $\cos\theta$ de la forma geométrica del producto escalar ($u\cdot v = \|u\|\,\|v\|\cos\theta$):
> $$\cos\theta = \frac{u\cdot v}{\|u\|\,\|v\|}$$
> Esta es, literalmente, la **similitud coseno**: el coseno del ángulo entre dos vectores, sin importar su longitud (por eso dos embeddings "apuntan en la misma dirección" — se parecen — aunque uno tenga norma mucho más grande que el otro). Verificado con $u=(1,0)$, $v=(1,1)$: $\cos\theta = \frac{1}{\sqrt2}\approx0{,}71$, que corresponde a $\theta=45°$ — el ángulo real entre ambos vectores. Cuando $\theta=90°$ (vectores ortogonales), $\cos\theta=0$, consistente con "$u\cdot v=0$ ⟺ ortogonales" de arriba: son la misma propiedad, mirada desde dos ángulos distintos. *Fuente: [[mml-book]], cap. 3.4.*

> [!tip] Conexión clave con MLOps/ML
> El producto escalar es el "ladrillo" con el que se construye la multiplicación de [[02 - Matrices|matrices]]. Cuando una red neuronal calcula `W·x + b`, en el fondo está haciendo un producto escalar entre cada fila de la matriz de pesos `W` y el vector de entrada `x`. Esto es, en esencia, una [[03 - Transformaciones lineales|transformación lineal]] aplicada al vector de entrada.

## Por qué esto importa para Data Science y MLOps

- **Representación de datos**: cada fila de un dataset es un vector en un espacio de _n_ dimensiones (una por feature).
- **Embeddings**: en NLP y sistemas de recomendación, palabras, oraciones, usuarios e ítems se representan como vectores densos; la similitud entre ellos se mide con norma y producto escalar.
- **Modelos lineales**: regresión lineal/logística son, en esencia, productos escalares entre un vector de pesos y un vector de features.
- **Redes neuronales**: cada capa aplica una [[03 - Transformaciones lineales|transformaciones lineales]] (multiplicación por una matriz de pesos) seguida de una [[01 - Funciones|función]] de activación no lineal.
- **Optimización**: el entrenamiento de modelos ajusta vectores de parámetros minimizando una función de costo, usando el [[02 - Derivadas|gradiente]] (un vector de derivadas parciales) dentro de un proceso de [[03 - Optimizacion|optimizacion]].

## Temas relacionados

- [[02 - Matrices|Matrices]] — generalización de vectores a colecciones de vectores; producto matricial.
- [[03 - Transformaciones lineales|Transformaciones lineales]] — cómo las matrices transforman vectores (rotación, escalado, proyección).
- [[01 - Funciones|Funciones]] — mapeos entre espacios vectoriales (incluye funciones de activación).
- [[02 - Derivadas|Derivadas]] — base para entender el gradiente como vector de máximo crecimiento.
- [[03 - Optimizacion|Optimizacion]] — cómo se usan vectores de parámetros y gradientes para entrenar modelos.

---