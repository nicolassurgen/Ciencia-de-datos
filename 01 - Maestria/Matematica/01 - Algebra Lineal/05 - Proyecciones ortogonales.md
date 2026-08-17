---
titulo: Proyecciones ortogonales
materia: Matemática
tipo: apunte
fecha: 2026-08-16
tags:
  - matematica
  - maestria
  - algebra-lineal
  - ciencia-de-datos
  - mlops
  - tema/proyecciones
---

## ¿Qué problema resuelve?

[[04 - Sistemas de ecuaciones lineales]] terminó con una pregunta sin cerrar: cuando un sistema $A\mathbf{x}=\mathbf{b}$ no tiene solución exacta, ¿por qué $\hat{\mathbf{x}}=(A^TA)^{-1}A^T\mathbf{b}$ es la "mejor aproximación posible"? Esta nota responde esa pregunta desde la geometría — la misma pregunta que responde [[03 - Optimizacion]] desde el cálculo (derivando e igualando a cero). Son dos caminos distintos al mismo resultado, y verlos ambos es lo que hace que la fórmula deje de sentirse arbitraria.

También responde algo que `Statsmodels/04 - Diagnostico de modelos.md` da por sentado sin explicar: por qué, después de ajustar una regresión, los residuos "deberían no decir nada" — no tener ningún patrón, no estar correlacionados con las predictoras.

## La idea, con una sombra

Pensá en un objeto flotando sobre una mesa, y el sol pegando derecho desde arriba. La **sombra** del objeto sobre la mesa es su **proyección**: el punto de la mesa que queda más cerca del objeto, siguiendo un rayo perpendicular a la mesa. Si el objeto ya está apoyado en la mesa, su sombra es él mismo. Si está flotando a un metro de altura, la sombra "pierde" esa dimensión de altura — se queda solo con la parte del objeto que sí vive en el plano de la mesa.

Proyectar un vector sobre una recta o un subespacio es exactamente esa idea, en el lenguaje de vectores: encontrar el punto de la recta (o el subespacio) que queda **más cerca** del vector original, y esa distancia mínima queda, geométricamente, formando un **ángulo recto** con la recta o subespacio.

## Proyección sobre una recta

Dado un vector $\mathbf{x}$ y una recta que pasa por el origen en la dirección de un vector $\mathbf{b}$, la proyección de $\mathbf{x}$ sobre esa recta es el punto de la recta más cercano a $\mathbf{x}$:

> [!definition] Proyección de un vector sobre una recta
> $$\text{proy}_{\mathbf b}(\mathbf x) = \frac{\mathbf{x}\cdot\mathbf{b}}{\mathbf{b}\cdot\mathbf{b}}\,\mathbf{b}$$
> donde $\mathbf x \cdot \mathbf b$ es el [[01 - Vectores|producto escalar]]. *Fuente: [[mml-book]], cap. 3.8.1.*

**De dónde sale**: la proyección es un múltiplo de $\mathbf b$ (vive sobre la recta), digamos $\lambda\mathbf b$. Para que sea la *más cercana* a $\mathbf x$, el vector "error" ($\mathbf x - \lambda\mathbf b$, la distancia entre el original y su sombra) tiene que ser **perpendicular** a la recta — es decir, ortogonal a $\mathbf b$:

$$(\mathbf{x}-\lambda\mathbf{b})\cdot\mathbf{b} = 0 \;\Longrightarrow\; \mathbf{x}\cdot\mathbf{b} - \lambda(\mathbf{b}\cdot\mathbf{b}) = 0 \;\Longrightarrow\; \lambda = \frac{\mathbf{x}\cdot\mathbf{b}}{\mathbf{b}\cdot\mathbf{b}}$$

**Ejemplo verificado**: proyectar $\mathbf{x}=(3,4)$ sobre la recta $y=x$ (dirección $\mathbf{b}=(1,1)$):

```python
import numpy as np
x = np.array([3, 4])
b = np.array([1, 1])
proyeccion = ((x @ b) / (b @ b)) * b
print(proyeccion)   # [3.5, 3.5]

residuo = x - proyeccion
print(residuo @ b)   # 0.0 -> el residuo es ortogonal a b
```

> [!important] La propiedad que se generaliza a todo el resto de la nota
> El residuo ($\mathbf{x}$ menos su proyección) es siempre **ortogonal** a aquello sobre lo que se proyectó. No es una coincidencia del ejemplo — es la condición que *define* qué significa "más cercano".

## Proyección sobre un subespacio: la ecuación normal

La misma idea se generaliza cuando, en vez de una recta, se proyecta sobre un **subespacio** generado por varios vectores (las columnas de una matriz $B$, en vez de un solo vector $\mathbf b$). La condición sigue siendo la misma —el residuo tiene que ser ortogonal a **todas** las columnas de $B$ a la vez— y lleva a la **ecuación normal**:

$$B^T(\mathbf{x}-B\boldsymbol\lambda) = \mathbf{0} \;\Longrightarrow\; B^TB\boldsymbol\lambda = B^T\mathbf{x} \;\Longrightarrow\; \boldsymbol\lambda = (B^TB)^{-1}B^T\mathbf{x}$$

*Fuente: [[mml-book]], cap. 3.8.2.* Y la proyección misma (el punto del subespacio, no solo las coordenadas $\boldsymbol\lambda$) es:

$$\text{proy}(\mathbf{x}) = B\boldsymbol\lambda = \underbrace{B(B^TB)^{-1}B^T}_{\text{matriz de proyección}}\,\mathbf{x}$$

## La conexión con mínimos cuadrados: por qué OLS es una proyección

Reemplazando $B$ por la matriz de diseño $X$ (una columna por predictora) y $\mathbf x$ por el vector de valores observados $y$, la ecuación normal es **literalmente** $X^TX\hat\beta = X^Ty$ — la misma ecuación que resuelve $\hat\beta = (X^TX)^{-1}X^Ty$.

> [!important] Qué significa esto en criollo
> Cuando `smf.ols(...)` ajusta una regresión, lo que hace geométricamente es tomar el vector de valores observados $y$ (que en general **no** puede escribirse como ninguna combinación lineal exacta de las predictoras) y encontrar su **sombra**: el punto $\hat y = X\hat\beta$ que sí vive en el subespacio generado por las columnas de $X$, y que queda más cerca posible de $y$. Los **residuos** ($y - \hat y$, lo que `Statsmodels/04 - Diagnostico de modelos.md` grafica para diagnosticar el modelo) son, por construcción, ortogonales a cada columna de $X$ — $X^T(y-X\hat\beta) = \mathbf 0$. Esa es la razón matemática exacta de por qué se espera que los residuos "no digan nada": si tuvieran algún patrón relacionado con una predictora, esa correlación no sería cero, y el ajuste no habría sido óptimo todavía.

**Verificado con un ejemplo mínimo** (3 puntos, recta con intercepto):

```python
import numpy as np
X = np.array([[1, 1], [1, 2], [1, 3]])   # columna de 1s (intercepto) + x
y = np.array([2, 3, 5])

beta_hat = np.linalg.inv(X.T @ X) @ X.T @ y
print(beta_hat)          # [0.333..., 1.5]  -> intercepto y pendiente

residuos = y - X @ beta_hat
print(X.T @ residuos)    # [~0, ~0] -> los residuos son ortogonales a las columnas de X
```

## Por qué esto importa para Data Science y MLOps

- **Regresión lineal**: la interpretación geométrica de por qué OLS es "óptimo" — ver [[02 - Regresion lineal (OLS y WLS)]].
- **Diagnóstico de residuos**: la ortogonalidad $X^Te=0$ es la razón formal por la que se espera que los residuos no tengan patrón — ver [[04 - Diagnostico de modelos]] de Statsmodels.
- **Similitud coseno y recomendación**: proyectar un vector sobre otro es, en esencia, la misma operación que mide cuánto se "parecen" dos vectores en la dirección que comparten (ver la fórmula del ángulo en [[01 - Vectores]]).

## Temas relacionados
- [[04 - Sistemas de ecuaciones lineales]] — el problema que esta nota resuelve geométricamente.
- [[01 - Vectores]] — producto escalar, la operación base de toda proyección.
- [[02 - Matrices]] — la matriz de diseño y la matriz inversa que aparecen en la fórmula.
- [[03 - Optimizacion]] — la misma fórmula, derivada por cálculo en vez de por geometría.

---
