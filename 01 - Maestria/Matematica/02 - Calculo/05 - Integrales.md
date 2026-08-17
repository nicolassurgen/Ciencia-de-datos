---
titulo: Integrales
materia: Matemática
tipo: apunte
fecha: 2026-08-16
tags:
  - matematica
  - maestria
  - calculo
  - ciencia-de-datos
  - mlops
  - tema/integrales
---

## ¿Qué problema resuelve la integral?

`SciPy/02 - Distribuciones de probabilidad.md` describe `pdf(x)` como "qué tan densa es la probabilidad en $x$" y `cdf(x)` como "qué proporción de la distribución queda por debajo de $x$", y da a entender que una se obtiene de la otra — pero nunca dice **cómo**. La respuesta es una integral, y sin entender qué es una integral, la relación entre densidad y probabilidad acumulada queda como un hecho a memorizar en vez de algo que se entiende.

El problema concreto que resuelve la integral: dada una curva, ¿cuál es el **área** que queda debajo de ella, entre dos puntos? Para una figura simple (un rectángulo, un triángulo) el área se calcula con una fórmula geométrica directa. Para una curva cualquiera —como la campana de una distribución normal— no hay una fórmula geométrica simple. Hace falta una herramienta general.

## De sumar rectángulos a la integral

La idea es la misma que ya se usó para llegar a la derivada en [[02 - Derivadas]]: partir de una aproximación simple y **refinarla hasta el límite**.

Para aproximar el área bajo una curva $f(x)$ entre $x=a$ y $x=b$, se puede dividir ese tramo en $n$ rectángulos angostos, cada uno de ancho $\Delta x = (b-a)/n$ y de altura $f(x_i)$ (el valor de la función en algún punto de ese rectángulo). Sumando las áreas de todos los rectángulos se obtiene una aproximación del área total:

$$\text{área aproximada} = \sum_{i=1}^{n} f(x_i) \, \Delta x$$

Esta aproximación mejora a medida que los rectángulos se hacen más angostos (más cantidad de rectángulos, cada uno más fino). Si se deja que $n \to \infty$ (y por lo tanto $\Delta x \to 0$), esa suma converge a un valor exacto: la **integral definida**.

> [!definition] Integral definida
> $$\int_a^b f(x)\,dx = \lim_{n \to \infty} \sum_{i=1}^{n} f(x_i)\,\Delta x$$
> Es el área (con signo: negativa donde $f(x) < 0$) bajo la curva de $f$, entre $x=a$ y $x=b$. El símbolo $\int$ es una "S" alargada (de *suma*), y $dx$ representa el ancho de cada rectángulo infinitesimal — literalmente, el límite de $\Delta x$ cuando tiende a cero.

Esta construcción (sumas de rectángulos cada vez más finos, llevadas al límite) se llama **suma de Riemann**, y es la definición estándar de integral que alcanza para todo lo que aparece en ciencia de datos.

## La integral indefinida y el Teorema Fundamental del Cálculo

Hay una segunda idea, aparentemente sin relación con la primera: dada una función $f$, encontrar una función $F$ tal que $F'(x) = f(x)$ — es decir, **deshacer** una derivada. A $F$ se la llama una **antiderivada** o **integral indefinida** de $f$, y se anota:

$$\int f(x)\,dx = F(x) + C$$

(la constante $C$ aparece porque la derivada de cualquier constante es cero, así que $F(x)$ y $F(x)+5$ tienen exactamente la misma derivada — sin más información, no se puede distinguir cuál era la función original).

> [!important] Teorema Fundamental del Cálculo
> Estas dos ideas —área bajo la curva, y deshacer una derivada— son, sorprendentemente, **la misma operación**. Si $F$ es una antiderivada de $f$ (es decir, $F'=f$), entonces:
> $$\int_a^b f(x)\,dx = F(b) - F(a)$$
> Esto es lo que permite calcular áreas **sin** sumar infinitos rectángulos a mano: alcanza con encontrar una antiderivada y evaluarla en los dos extremos. Es la razón por la que integrar y derivar se enseñan como operaciones inversas, del mismo modo que sumar y restar.

## Reglas básicas de integración

| Regla | Fórmula |
|---|---|
| Potencia | $\displaystyle\int x^n\,dx = \frac{x^{n+1}}{n+1} + C \quad (n \neq -1)$ |
| Constante multiplicativa | $\displaystyle\int k f(x)\,dx = k\int f(x)\,dx$ |
| Suma | $\displaystyle\int \big(f(x)+g(x)\big)\,dx = \int f(x)\,dx + \int g(x)\,dx$ |
| Exponencial | $\displaystyle\int e^x\,dx = e^x + C$ (ver [[04 - Funciones exponenciales y logaritmicas]]) |

La regla de la potencia es, literalmente, la regla de la potencia de la derivada ($\frac{d}{dx}x^n = nx^{n-1}$, ver [[02 - Derivadas]]) aplicada al revés: sumar 1 al exponente y dividir por el exponente nuevo, en vez de restar 1 y multiplicar por el viejo.

## Ejemplo trabajado: de una densidad a una probabilidad

Una variable aleatoria uniforme entre 2 y 6 tiene densidad constante:

$$f(x) = \begin{cases} \dfrac{1}{4} & \text{si } 2 \le x \le 6 \\ 0 & \text{en cualquier otro caso} \end{cases}$$

**¿Por qué $\frac14$?** El área total bajo cualquier densidad de probabilidad tiene que dar exactamente 1 (es una certeza que la variable cae en *algún* valor de su rango). El intervalo $[2,6]$ tiene ancho 4, así que la altura tiene que ser $1/4$ para que área $=$ ancho $\times$ altura $= 4 \times \frac14 = 1$.

**¿Cuál es la probabilidad de que la variable caiga entre 2 y 5?** Es el área bajo $f$ entre esos dos puntos:

$$P(2 \le X \le 5) = \int_2^5 \frac14\,dx = \frac14 (5-2) = \frac{3}{4}$$

Verificado numéricamente (integrando la densidad con `scipy.integrate.quad` entre 2 y 5): el resultado da exactamente $0{,}75$, coincidiendo con el cálculo a mano.

> [!important] La relación exacta entre PDF y CDF
> La función de distribución acumulada $F(x)$ (lo que en SciPy es `cdf(x)`) **es**, por definición, el área bajo la función de densidad $f$ (lo que en SciPy es `pdf(x)`) desde $-\infty$ hasta $x$:
> $$F(x) = \int_{-\infty}^{x} f(t)\,dt$$
> Para el ejemplo de arriba, $F(x) = \frac{x-2}{4}$ para $2 \le x \le 6$ — evaluando en $x=5$: $F(5) = \frac{5-2}{4} = 0{,}75$, el mismo resultado. Por el Teorema Fundamental del Cálculo, esto también significa que **la derivada de la CDF es la PDF**: $F'(x) = f(x)$ — la densidad mide qué tan rápido crece la probabilidad acumulada en cada punto.

## Por qué esto importa para Data Science y MLOps

- **`scipy.stats`**: `pdf()` y `cdf()` de cualquier distribución continua (normal, exponencial, uniforme...) están relacionadas exactamente por esta integral — ver [[02 - Distribuciones de probabilidad]] de SciPy.
- **Esperanza y momentos poblacionales**: la media teórica de una variable continua es $E[X] = \int x\, f(x)\,dx$, y la varianza teórica es $\text{Var}(X) = \int (x-\mu)^2 f(x)\,dx$ — la versión continua exacta de la analogía del "momento de inercia" que ya aparece, en su versión discreta (suma en vez de integral), en [[medidas de dispersión]].
- **Verosimilitud continua**: evaluar la densidad de una distribución continua en un dato observado (no su probabilidad puntual, que sería cero) es la base de la función de verosimilitud para datos continuos — ver [[06 - Verosimilitud y estimación por máxima verosimilitud]].
- **Área bajo la curva (AUC)**: métricas de evaluación de modelos de clasificación como el AUC-ROC son, literalmente, el cálculo de un área bajo una curva mediante integración numérica.

## Temas relacionados
- [[02 - Derivadas]] — la operación inversa; el Teorema Fundamental del Cálculo conecta ambas.
- [[04 - Funciones exponenciales y logaritmicas]] — la integral de $e^x$.
- [[06 - Verosimilitud y estimación por máxima verosimilitud]] — usa densidades (evaluadas, no integradas) para datos continuos.
- [[medidas de dispersión]] — la varianza como "momento de inercia": versión discreta (suma) de lo que acá es una integral.

---
