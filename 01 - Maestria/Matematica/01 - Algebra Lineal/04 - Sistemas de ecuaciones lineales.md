---
titulo: Sistemas de ecuaciones lineales
materia: Matemática
tipo: apunte
fecha: 2026-08-16
tags:
  - matematica
  - maestria
  - algebra-lineal
  - ciencia-de-datos
  - mlops
  - tema/sistemas-de-ecuaciones
---

## ¿Qué problema resuelve?

La fórmula $\hat\beta = (X^TX)^{-1}X^Ty$ aparece citada en [[02 - Matrices]] y en [[03 - Optimizacion]] como "la solución de la regresión lineal por mínimos cuadrados", sin nunca explicar de dónde sale. La respuesta empieza acá: esa fórmula es la solución de un **sistema de ecuaciones lineales** — la misma idea que resolver "2 ecuaciones con 2 incógnitas" del colegio, generalizada a cientos o miles de ecuaciones e incógnitas usando matrices.

## El problema, sin matrices todavía

Un sistema de ecuaciones lineales es un conjunto de ecuaciones que comparten las mismas incógnitas, todas elevadas a la primera potencia (sin cuadrados, sin productos entre incógnitas). Por ejemplo:

$$\begin{cases} 2x + y = 5 \\ x - y = 1 \end{cases}$$

Geométricamente, cada ecuación es una **recta** en el plano $(x,y)$. Resolver el sistema es encontrar el punto (o los puntos) donde **todas** las rectas se cruzan a la vez. Con dos rectas en el plano hay exactamente tres posibilidades:

- **Se cruzan en un único punto** → el sistema tiene **una solución** (el caso más común: dos rectas con distinta pendiente).
- **Son paralelas y distintas** → el sistema **no tiene solución** (nunca se cruzan).
- **Son la misma recta** → el sistema tiene **infinitas soluciones** (se cruzan en todos sus puntos).

Para el ejemplo de arriba, despejando: $x=2$, $y=1$ es la única solución (verificado: $2(2)+1=5$ ✓, $2-1=1$ ✓).

## Forma matricial: $A\mathbf{x} = \mathbf{b}$

Escribir un sistema ecuación por ecuación se vuelve inmanejable apenas hay más de 3 o 4 incógnitas. La forma compacta agrupa los coeficientes en una [[02 - Matrices|matriz]] $A$, las incógnitas en un [[01 - Vectores|vector]] $\mathbf{x}$, y los resultados en un vector $\mathbf{b}$:

$$\underbrace{\begin{bmatrix} 2 & 1 \\ 1 & -1 \end{bmatrix}}_{A} \underbrace{\begin{bmatrix} x \\ y \end{bmatrix}}_{\mathbf{x}} = \underbrace{\begin{bmatrix} 5 \\ 1 \end{bmatrix}}_{\mathbf{b}}$$

Multiplicar $A$ por $\mathbf{x}$ (con la regla de multiplicación de matrices de [[02 - Matrices]]) reproduce exactamente las dos ecuaciones originales — es solo una forma más compacta de escribir lo mismo, no una idea distinta.

> [!definition] Sistema de ecuaciones lineales
> Un sistema $A\mathbf{x}=\mathbf{b}$, donde $A$ es una matriz de coeficientes conocidos ($m$ ecuaciones × $n$ incógnitas), $\mathbf{b}$ es un vector de resultados conocidos, y $\mathbf{x}$ es el vector de incógnitas a encontrar. *Fuente: [[mml-book]], cap. 2.1.*

## Resolver el sistema: eliminación gaussiana, la idea

El método sistemático para resolver un sistema (a mano, para pocas ecuaciones) es la **eliminación gaussiana**: usar una ecuación para "cancelar" una incógnita de las demás, repitiendo hasta que quede una sola ecuación con una sola incógnita, y después ir sustituyendo hacia atrás.

Sobre el ejemplo: sumando las dos ecuaciones originales ($2x+y=5$ y $x-y=1$), el término $y$ se cancela: $3x = 6 \Rightarrow x=2$. Sustituyendo en la segunda ecuación: $2-y=1 \Rightarrow y=1$.

> [!note] Esto no es lo que hace una computadora
> A mano, la eliminación gaussiana alcanza perfectamente. En la práctica, NumPy (`np.linalg.solve(A, b)`) no elimina variables ecuación por ecuación como se haría a mano — usa una **factorización de la matriz** (descomposición LU) internamente, más estable numéricamente para sistemas grandes. La idea de fondo (reducir el sistema a una forma más simple de resolver) es la misma; el método exacto es distinto. Este vault no desarrolla esas factorizaciones todavía — no hay ningún punto del código del vault que las necesite hoy.

## Cuando no hay solución exacta: el caso que realmente importa en Data Science

Todo lo anterior asume que existe una solución exacta. Pero en ciencia de datos el caso típico es **al revés**: muchas más ecuaciones que incógnitas. Por ejemplo, "ajustar una recta a 300 puntos" es, formalmente, plantear 300 ecuaciones (una por punto: "la recta debería pasar por este punto") con solo 2 incógnitas (pendiente y ordenada al origen). Casi con certeza, **no existe** ninguna recta que pase exactamente por los 300 puntos — el sistema $X\beta = y$ no tiene solución exacta.

> [!important] La salida: no resolver el sistema, aproximarlo
> Cuando $A\mathbf{x}=\mathbf{b}$ no tiene solución exacta, la pregunta razonable deja de ser "¿qué $\mathbf{x}$ resuelve el sistema?" y pasa a ser "¿qué $\mathbf{x}$ hace que $A\mathbf{x}$ quede **lo más cerca posible** de $\mathbf{b}$?" — minimizando el error total. Esa pregunta tiene una respuesta cerrada:
> $$\hat{\mathbf{x}} = (A^TA)^{-1}A^T\mathbf{b}$$
> *Fuente: [[mml-book]], cap. 2.3.*
>
> Aplicada al caso de ajustar una recta ($A=X$, la matriz de diseño; $\mathbf{b}=y$, los valores observados), esta es exactamente la fórmula de mínimos cuadrados $\hat\beta=(X^TX)^{-1}X^Ty$ que ya citan [[02 - Matrices]] y [[03 - Optimizacion]] — no es una fórmula nueva ni mágica, es la solución "más cercana posible" de un sistema de ecuaciones que, tomado literalmente, no tiene solución. El desarrollo geométrico completo de *por qué* esta fórmula da la mejor aproximación (proyectar $\mathbf b$ sobre el subespacio que sí es alcanzable) está en [[05 - Proyecciones ortogonales]], y el desarrollo por cálculo (derivar e igualar a cero) está en [[03 - Optimizacion]].

## Ejemplo verificado

Sobre el sistema $2x+y=5$, $x-y=1$:

```python
import numpy as np

A = np.array([[2, 1], [1, -1]])
b = np.array([5, 1])
solucion = np.linalg.solve(A, b)
print(solucion)   # [2. 1.]
```

Coincide con la solución a mano ($x=2$, $y=1$).

## Por qué esto importa para Data Science y MLOps

- **Regresión lineal**: ajustar un modelo a datos observados es, de fondo, intentar resolver un sistema sobredeterminado (más observaciones que parámetros) y quedarse con la mejor aproximación — ver [[02 - Regresion lineal (OLS y WLS)]] de Statsmodels.
- **Redes neuronales**: cada capa resuelve, en el fondo, una transformación lineal $A\mathbf{x}$ — entender cuándo esa transformación es invertible (determinante distinto de cero, ver [[02 - Matrices]]) es entender cuándo esa capa "pierde información".
- **Multicolinealidad**: cuando dos predictoras de un modelo están muy correlacionadas, el sistema $X^TX\beta = X^Ty$ queda cerca de no tener solución única — la causa algebraica exacta detrás del VIF alto que reporta [[04 - Diagnostico de modelos]] de Statsmodels.

## Temas relacionados
- [[02 - Matrices]] — la matriz de coeficientes y la matriz de diseño.
- [[05 - Proyecciones ortogonales]] — por qué $(A^TA)^{-1}A^T\mathbf{b}$ es la mejor aproximación cuando no hay solución exacta.
- [[03 - Optimizacion]] — la misma fórmula, derivada minimizando una suma de errores al cuadrado.
- [[02 - Regresion lineal (OLS y WLS)]] — la aplicación práctica en Statsmodels.

---
