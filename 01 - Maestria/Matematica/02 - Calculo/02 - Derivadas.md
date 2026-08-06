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

## ¿Qué es una derivada?

La **derivada** de una función en un punto mide su **tasa de cambio instantánea**: cuánto varía la salida ante un cambio infinitesimal en la entrada. Formalmente, es un límite:

$$f'(x) = \lim_{h \to 0} \frac{f(x+h) - f(x)}{h}$$

> [!tip] Interpretación geométrica
> $f'(x)$ es la **pendiente de la recta tangente** a la curva de $f$ en el punto $x$. Si $f'(x) > 0$, la función crece ahí; si $f'(x) < 0$, decrece; si $f'(x) = 0$, el punto es "plano" (posible mínimo, máximo o punto de inflexión).

## Reglas básicas

| Regla | Fórmula |
|---|---|
| Potencia | $\dfrac{d}{dx} x^n = n x^{n-1}$ |
| Suma | $(f+g)' = f' + g'$ |
| Producto | $(fg)' = f'g + fg'$ |
| **Regla de la cadena** | $\dfrac{d}{dx} f(g(x)) = f'(g(x)) \cdot g'(x)$ |

> [!info] La regla de la cadena es la más importante para ML
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

> [!tip] Propiedad clave
> El gradiente **apunta en la dirección de máximo crecimiento** de la función. Su opuesto, $-\nabla f$, apunta en la dirección de **máximo decrecimiento** — la dirección exacta que conviene seguir para minimizar una función. Esa es la idea completa detrás del **descenso por gradiente** (ver [[03 - Optimizacion]]).

Como el gradiente es un [[01 - Vectores|vector]], hereda todas sus operaciones: norma (¿qué tan "empinada" es la función en ese punto?), producto escalar, etc.

## El Hessiano (segundas derivadas)

Así como el gradiente junta las **primeras** derivadas parciales en un vector, el **Hessiano** junta las **segundas** derivadas parciales en una [[02 - Matrices|matriz]]:

$$H_{i,j} = \frac{\partial^2 f}{\partial x_i \, \partial x_j}$$

El Hessiano describe la **curvatura** de la función: si es una matriz definida positiva en un punto donde el gradiente es cero, ese punto es un **mínimo local**. Se usa en métodos de optimización de segundo orden (ver [[03 - Optimizacion]]).

## Por qué esto importa para Data Science y MLOps

- **Entrenamiento de modelos**: ajustar los parámetros de un modelo para minimizar una función de costo requiere saber en qué dirección moverse — eso es el gradiente.
- **Backpropagation**: aplica la regla de la cadena sobre la composición de funciones de una red neuronal para calcular el gradiente respecto de **cada** parámetro, capa por capa.
- **Convergencia**: la forma del Hessiano (su curvatura) ayuda a entender por qué algunos problemas de optimización son más difíciles o lentos de resolver que otros.

## Temas relacionados

- [[01 - Funciones]] — qué se está derivando; la composición de funciones detrás de backpropagation.
- [[01 - Vectores]] — el gradiente es un vector de derivadas parciales.
- [[02 - Matrices]] — el Hessiano es una matriz de segundas derivadas.
- [[03 - Optimizacion]] — cómo se usa el gradiente (y el Hessiano) para minimizar funciones.

---
