---
titulo: Verosimilitud y estimación por máxima verosimilitud
materia: Matemática
tipo: apunte
fecha: 2026-08-16
tags:
  - matematica
  - maestria
  - calculo
  - ciencia-de-datos
  - mlops
  - tema/verosimilitud
---

## ¿Qué problema resuelve?

`scipy.stats` describe `fit()` como una función que "busca los parámetros que hacen más probable haber observado justo estos datos", y `statsmodels` ajusta un `GLM` o una regresión logística con `.fit()` sin nunca decir explícitamente **qué** está calculando por dentro. En ambos casos, la respuesta es el mismo procedimiento matemático: **estimación por máxima verosimilitud** (*Maximum Likelihood Estimation*, MLE).

El problema concreto: se tiene un dataset, y una familia de distribuciones de probabilidad con uno o más parámetros libres (por ejemplo, una Normal con media $\mu$ y desvío $\sigma$ sin especificar, o una Bernoulli con probabilidad de éxito $p$ sin especificar). ¿Qué valor de esos parámetros elegir, de entre todos los posibles, para que la distribución describa mejor los datos observados?

## Intuición: elegir el parámetro que hace más creíble lo que ya se vio

Imaginá una moneda de la que no se sabe si está cargada. Se la tira 10 veces y salen 7 caras. Si la moneda tuviera $p=0{,}1$ de probabilidad de cara, observar 7 caras en 10 tiradas sería un resultado rarísimo. Si tuviera $p=0{,}7$, sería el resultado más típico posible. Si tuviera $p=0{,}5$ (moneda justa), sería un resultado posible pero no el más esperable.

La idea de la máxima verosimilitud es exactamente esa comparación, llevada a su extremo: de **todos** los valores posibles de $p$ entre 0 y 1, elegir el que hace que el resultado observado (7 caras en 10 tiradas) sea el **más probable** de todos. No se trata de "¿cuál es la probabilidad de que $p$ valga tal cosa?" (esa es una pregunta distinta, de estadística bayesiana) sino de "¿para qué valor de $p$ es más creíble el dato que ya tengo?".

## Probabilidad y verosimilitud: la misma fórmula, dos preguntas distintas

> [!important] No es lo mismo "probabilidad" que "verosimilitud"
> Ambas se calculan con la misma función matemática — la densidad o función de masa de probabilidad $p(x \mid \theta)$ — pero mirándola desde ángulos opuestos:
> - **Probabilidad**: fijo el parámetro $\theta$, y pregunto qué tan probables son distintos datos $x$. ("Si la moneda tiene $p=0{,}5$, ¿qué tan probable es sacar 7 caras en 10 tiradas?")
> - **Verosimilitud**: fijo el dato $x$ observado (ya pasó, es un hecho), y pregunto qué tan verosímil es cada valor posible del parámetro $\theta$. ("Ya obtuve 7 caras en 10 tiradas — ¿qué tan verosímil es cada valor posible de $p$?")
>
> La **función de verosimilitud** $\mathcal{L}(\theta \mid x)$ es literalmente $p(x \mid \theta)$, la misma fórmula — pero tratada como función de $\theta$ con $x$ fijo, en vez de como función de $x$ con $\theta$ fijo.

## Definición formal

> [!definition] Función de verosimilitud
> Para un dato observado $x$ y una familia de distribuciones $p(x \mid \theta)$ parametrizada por $\theta$, la función de verosimilitud es:
> $$\mathcal{L}(\theta) = p(x \mid \theta)$$
> El **estimador de máxima verosimilitud** $\hat\theta_{\text{MLE}}$ es el valor de $\theta$ que maximiza esa función:
> $$\hat\theta_{\text{MLE}} = \arg\max_\theta \; \mathcal{L}(\theta)$$
> (la misma notación $\arg\max$/$\arg\min$ que ya se usa en [[03 - Optimizacion]] para "el valor de la variable que optimiza la función", no el valor óptimo en sí).

Cuando hay $n$ datos independientes $x_1, \dots, x_n$ (el supuesto de **independencia** hace que la probabilidad conjunta sea el **producto** de las probabilidades individuales), la verosimilitud del conjunto completo es:

$$\mathcal{L}(\theta) = \prod_{i=1}^{n} p(x_i \mid \theta)$$

## Por qué se usa el logaritmo: de un producto a una suma

Multiplicar $n$ probabilidades (cada una menor a 1) da un número que se achica extremadamente rápido a medida que $n$ crece — con cientos de datos, el producto puede ser tan chico que una computadora lo redondea a cero. Además, un producto de $n$ términos es incómodo de derivar. La solución es tomar logaritmo, usando la propiedad "logaritmo de un producto = suma de logaritmos" (ver [[04 - Funciones exponenciales y logaritmicas]]):

$$\ln \mathcal{L}(\theta) = \sum_{i=1}^{n} \ln p(x_i \mid \theta)$$

Como el logaritmo es una función **creciente** (si $a>b$ entonces $\ln a > \ln b$), maximizar $\mathcal{L}(\theta)$ y maximizar $\ln \mathcal{L}(\theta)$ dan **exactamente el mismo** $\hat\theta$ — el logaritmo no cambia *dónde* está el máximo, solo lo hace numéricamente manejable y algebraicamente más simple de derivar.

> [!note] Log-verosimilitud negativa: la misma idea, con el signo dado vuelta
> Gran parte de la literatura de Machine Learning trabaja con la **log-verosimilitud negativa** $\mathcal{L}_{\text{neg}}(\theta) = -\ln \mathcal{L}(\theta)$ y la **minimiza**, en vez de maximizar la log-verosimilitud directamente. Son la misma operación: minimizar $-f(\theta)$ da el mismo $\theta$ que maximizar $f(\theta)$. La razón de esta convención es, en palabras del propio libro de referencia, *"un artefacto histórico, debido a que se quiere maximizar la verosimilitud, pero la literatura de optimización numérica tiende a estudiar la minimización de funciones"* — la log-verosimilitud negativa encaja directo en el marco de "función de costo a minimizar" de [[03 - Optimizacion]]. *Fuente: [[mml-book]], cap. 8.3.1.*

## Ejemplo trabajado: la moneda (distribución de Bernoulli)

Sobre el ejemplo de la intuición: $n=10$ tiradas, $k=7$ caras. Cada tirada es una Bernoulli con probabilidad de éxito $p$ desconocida. La verosimilitud de observar exactamente $k$ caras en $n$ tiradas independientes es:

$$\mathcal{L}(p) = p^k (1-p)^{n-k}$$

Tomando logaritmo:

$$\ln \mathcal{L}(p) = k\ln p + (n-k)\ln(1-p)$$

Para maximizar, se deriva respecto de $p$ (ver [[02 - Derivadas]]) y se iguala a cero — exactamente el procedimiento de "punto crítico" de [[03 - Optimizacion]]:

$$\frac{d}{dp}\ln\mathcal{L}(p) = \frac{k}{p} - \frac{n-k}{1-p} = 0$$

Despejando $p$:

$$\frac{k}{p} = \frac{n-k}{1-p} \;\Longrightarrow\; k(1-p) = p(n-k) \;\Longrightarrow\; k = kp + p(n-k) = pn \;\Longrightarrow\; \hat{p}_{\text{MLE}} = \frac{k}{n}$$

Con $k=7$, $n=10$: $\hat p_{\text{MLE}} = 0{,}7$ — exactamente la proporción observada de caras. Verificado numéricamente (maximizando $\ln\mathcal{L}(p)$ por fuerza bruta con `scipy.optimize`, sin usar la fórmula cerrada): el óptimo numérico da $p \approx 0{,}7000003$, coincidiendo con la fórmula $k/n$.

> [!tip] Cuándo hay fórmula cerrada y cuándo no
> Para la Bernoulli (y para la Normal con varianza conocida, y para la regresión lineal por mínimos cuadrados) la ecuación $\frac{d}{d\theta}\ln\mathcal{L}(\theta)=0$ se puede despejar algebraicamente, dando una **fórmula cerrada** — como $\hat\beta=(X^TX)^{-1}X^Ty$ en OLS (ver [[02 - Matrices]]), que es, de hecho, el resultado de maximizar la log-verosimilitud de un modelo lineal con ruido gaussiano. *Fuente: [[mml-book]], cap. 9.2 y 9.4.* Para la mayoría de los modelos lineales generalizados (`GLM`, regresión logística/Poisson en `statsmodels`) esa ecuación **no** tiene solución algebraica — hay que resolverla numéricamente, con un método iterativo (`statsmodels` usa por defecto **IRLS**, *Iteratively Reweighted Least Squares*, una variante del método de Newton de [[03 - Optimizacion]]). Es exactamente lo que hace `.fit()` cuando no imprime ninguna fórmula: itera hasta converger a un óptimo numérico, en vez de calcular una fórmula cerrada de una sola vez.

## Por qué esto importa para Data Science y MLOps

- **`scipy.stats.<distribución>.fit()`**: ajusta los parámetros de cualquier distribución continua por máxima verosimilitud — ver [[02 - Distribuciones de probabilidad]] y [[09 - Estimacion de densidad y ajuste de distribuciones]] de SciPy.
- **`statsmodels` OLS**: la fórmula cerrada $\hat\beta=(X^TX)^{-1}X^Ty$ es, de fondo, el resultado de maximizar la log-verosimilitud gaussiana — ver [[02 - Regresion lineal (OLS y WLS)]].
- **`statsmodels` GLM**: sin fórmula cerrada, se resuelve por optimización numérica iterativa (IRLS) — ver [[03 - GLM y modelos discretos]].
- **Funciones de pérdida en Machine Learning**: la función de costo de la regresión logística, y la *cross-entropy loss* de las redes neuronales de clasificación, son ambas la log-verosimilitud negativa de un modelo probabilístico — el mismo objeto matemático de esta nota, con otro nombre.

## Temas relacionados
- [[03 - Optimizacion]] — $\arg\max$/$\arg\min$, puntos críticos, y por qué algunos problemas no tienen forma cerrada.
- [[02 - Derivadas]] — derivar la log-verosimilitud e igualar a cero.
- [[04 - Funciones exponenciales y logaritmicas]] — por qué el logaritmo convierte productos en sumas.
- [[02 - Matrices]] — la fórmula cerrada de mínimos cuadrados, $\hat\beta=(X^TX)^{-1}X^Ty$.
- [[02 - Distribuciones de probabilidad]] — dónde se usa MLE en la práctica, vía `fit()`.

---
