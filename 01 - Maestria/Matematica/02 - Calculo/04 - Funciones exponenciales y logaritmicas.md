---
titulo: Funciones exponenciales y logarítmicas
materia: Matemática
tipo: apunte
fecha: 2026-08-16
tags:
  - matematica
  - maestria
  - calculo
  - ciencia-de-datos
  - mlops
  - tema/logaritmos
---

## ¿Qué problema resuelve el logaritmo?

En Algoritmos aparece constantemente la expresión $\log_2 n$ — en la notación Big O ($O(\log n)$), en la fórmula del *doubling ratio* de Sedgewick ($b = \log_2(T(2n)/T(n))$), en la altura de un árbol balanceado ($\approx \log_2 N$) — pero nunca se explica desde cero qué **es** un logaritmo. Sin esa base, esas fórmulas hay que memorizarlas en vez de entenderlas.

La pregunta que resuelve el logaritmo es la inversa de una pregunta mucho más familiar. Elevar a una potencia responde: *"2 elevado a la 10, ¿cuánto da?"* → 1024. El logaritmo responde la pregunta al revés: *"¿a qué potencia hay que elevar 2 para llegar a 1024?"* → 10.

> [!definition] Logaritmo
> El logaritmo en base $b$ de un número $x$ es el exponente al que hay que elevar $b$ para obtener $x$:
> $$\log_b(x) = y \quad \Longleftrightarrow \quad b^y = x$$
> con $b > 0$, $b \neq 1$, y $x > 0$.

$\log_2(1024) = 10$ porque $2^{10} = 1024$. $\log_2(8) = 3$ porque $2^3 = 8$. El logaritmo "deshace" la potencia, de la misma forma que la resta deshace la suma y la división deshace la multiplicación — es la **operación inversa** de exponenciar.

## Por qué la base 2 aparece tanto en Algoritmos

> [!tip] La respuesta directa a "¿por qué log₂?"
> $\log_2(n)$ responde literalmente la pregunta *"¿cuántas veces puedo dividir $n$ a la mitad antes de llegar a 1?"* — que es exactamente lo que hace la búsqueda binaria (descartar la mitad de los datos restantes en cada paso) o lo que mide la altura de un árbol binario balanceado (cada nivel duplica la cantidad de nodos posibles respecto del nivel anterior). Con $n=1024$, hacen falta 10 divisiones a la mitad ($1024 \to 512 \to 256 \to \dots \to 1$) — el mismo 10 que da $\log_2(1024)$.

Esto conecta directo con la fórmula del *doubling ratio* de [[notación Big O y familias de complejidad]]: si al duplicar $n$ el tiempo se multiplica por una razón $r$, el exponente de la familia de complejidad es $b = \log_2(r)$ — la misma pregunta ("¿a qué potencia de 2 hay que elevar para obtener $r$?"), aplicada a tiempos de ejecución en vez de a tamaños de árbol.

## Tres bases distintas, tres contextos distintos

| Base | Notación | Dónde aparece |
|---|---|---|
| **2** | $\log_2$ | Ciencias de la computación: Big O, estructuras de datos que dividen a la mitad, teoría de la información (bits) |
| **10** | $\log_{10}$ o $\log$ | Escalas (decibeles, escala Richter, escalas logarítmicas en gráficos para comparar órdenes de magnitud muy distintos) |
| **$e$** (número de Euler, $\approx 2{,}71828$) | $\ln$ (logaritmo **natural**) | Cálculo y estadística: es la base que hace que la derivada de $e^x$ sea ella misma (ver más abajo), por eso aparece en la función sigmoide, en la log-verosimilitud y en casi cualquier desarrollo matemático continuo |

> [!important] Todos los logaritmos son proporcionales entre sí
> No hace falta memorizar tablas de conversión: $\log_b(x) = \dfrac{\ln(x)}{\ln(b)}$ para cualquier base $b$. Cambiar de base es multiplicar por una constante — por eso, en notación Big O, la base del logaritmo **no importa** y ni siquiera se especifica ($O(\log n)$ alcanza): $\log_2(n)$ y $\ln(n)$ difieren solo en un factor constante ($\ln(n) = \log_2(n) \times \ln(2)$), y las constantes se descartan en Big O (ver [[notación Big O y familias de complejidad]]).

## Propiedades algebraicas

Estas tres propiedades son la razón por la que el logaritmo es una herramienta tan usada, no una curiosidad matemática:

| Propiedad | Fórmula | En criollo |
|---|---|---|
| Logaritmo de un producto | $\log_b(xy) = \log_b(x) + \log_b(y)$ | Multiplicar adentro del log es sumar afuera |
| Logaritmo de una potencia | $\log_b(x^k) = k\log_b(x)$ | Un exponente adentro del log sale multiplicando afuera |
| Logaritmo de un cociente | $\log_b(x/y) = \log_b(x) - \log_b(y)$ | Dividir adentro del log es restar afuera |

> [!tip] Por qué esto importa: convierte productos en sumas
> Multiplicar muchos números chicos entre sí (como se hace al calcular la probabilidad conjunta de varios datos independientes) produce números extremadamente pequeños, que una computadora puede llegar a redondear a cero (*underflow*). Tomar logaritmo convierte ese producto en una suma — mucho más estable numéricamente y mucho más fácil de derivar. Esta propiedad es la razón exacta por la que se trabaja con **log-verosimilitud** en vez de verosimilitud directamente — ver [[06 - Verosimilitud y estimación por máxima verosimilitud]].

## La función exponencial y su inversa

$f(x) = b^x$ (con $b>0$, $b \neq 1$) es la **función exponencial**: crece (si $b>1$) multiplicándose por $b$ cada vez que $x$ aumenta en 1, en vez de sumar una cantidad fija como hace una función lineal. La función logarítmica $g(x) = \log_b(x)$ es su **función inversa**: si $f(a) = c$, entonces $g(c) = a$. Graficadas juntas, son reflejos una de la otra respecto de la recta $y=x$.

```
f(x) = 2^x            g(x) = log₂(x)
x=0 -> f=1             x=1   -> g=0
x=1 -> f=2             x=2   -> g=1
x=3 -> f=8             x=8   -> g=3
x=10 -> f=1024         x=1024 -> g=10
```

> [!note] Dominio y crecimiento
> La función exponencial $b^x$ ($b>1$) está definida para **todo** $x$ real, siempre da un resultado **positivo**, y crece cada vez más rápido (crecimiento *exponencial*, en el sentido literal de la palabra). Su inversa, $\log_b(x)$, solo está definida para $x > 0$ (no existe el logaritmo de un número negativo o de cero, en los reales) — consecuencia directa de que $b^y$ nunca da negativo ni cero.

## Derivadas de $e^x$ y $\ln(x)$

Conectando con [[02 - Derivadas]]: la base $e$ es especial precisamente porque es la única base para la cual la función exponencial es su propia derivada:

$$\frac{d}{dx} e^x = e^x \qquad\qquad \frac{d}{dx}\ln(x) = \frac{1}{x}$$

La primera fórmula dice que la tasa de crecimiento de $e^x$ en cualquier punto es exactamente igual al valor de la función en ese punto — la razón matemática de fondo por la que $e$ aparece en cualquier proceso donde "la velocidad de crecimiento es proporcional a la cantidad actual" (crecimiento poblacional, interés compuesto continuo, decaimiento radioactivo). La segunda regla ($\ln(x)$ deriva a $1/x$) es exactamente la que se usa para derivar la log-verosimilitud en [[06 - Verosimilitud y estimación por máxima verosimilitud]].

## Por qué esto importa para Data Science y MLOps

- **Notación Big O**: $O(\log n)$ describe algoritmos que dividen el problema a la mitad en cada paso (búsqueda binaria, árboles balanceados) — ver [[notación Big O y familias de complejidad]] y [[árboles]].
- **Función sigmoide**: $\sigma(x) = \frac{1}{1+e^{-x}}$ usa la exponencial de base $e$ — ver [[01 - Funciones]].
- **Log-verosimilitud**: convertir un producto de probabilidades en una suma de logaritmos es lo que hace viable, en la práctica, ajustar modelos estadísticos por máxima verosimilitud — ver [[06 - Verosimilitud y estimación por máxima verosimilitud]].
- **Escalas logarítmicas en gráficos**: cuando los datos abarcan varios órdenes de magnitud (por ejemplo, tiempos de ejecución de O(n) contra O(n²) para distintos $n$), graficar en escala logarítmica comprime esas diferencias y permite comparar formas de crecimiento — como ya se usó en los gráficos de verificación empírica de [[03 - Estructuras no lineales y complejidad algoritmica]].
- **Entropía y teoría de la información**: la entropía de Shannon usa $\log_2$ para medir "cantidad de información" en bits — tema de clases futuras de minería de datos.

## Temas relacionados
- [[01 - Funciones]] — la función sigmoide y softmax ya usan $e^x$ sin desarrollar por qué.
- [[02 - Derivadas]] — las reglas de derivación de $e^x$ y $\ln(x)$.
- [[06 - Verosimilitud y estimación por máxima verosimilitud]] — por qué se usa log-verosimilitud en vez de verosimilitud.
- [[notación Big O y familias de complejidad]] — el $\log_2$ de la fórmula del *doubling ratio*.
- [[árboles]] — la altura de un árbol balanceado es $O(\log N)$.

---
