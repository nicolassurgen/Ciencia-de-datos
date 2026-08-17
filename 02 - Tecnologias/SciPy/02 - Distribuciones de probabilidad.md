---
titulo: "SciPy.stats - Distribuciones de probabilidad"
materia: SciPy
tipo: apunte
tags:
  - scipy
  - tecnologias
  - python
  - tema/distribuciones
fuente: "SciPy Reference Guide — scipy.stats (docs.scipy.org/doc/scipy/reference/stats.html)"
---

# Distribuciones de probabilidad

> [!definition] Variable aleatoria
> `scipy.stats` modela cada distribución de probabilidad como un objeto: `rv_continuous` para variables continuas (normal, exponencial, uniforme…) y `rv_discrete` para discretas (binomial, Poisson…). Cada distribución conocida (`norm`, `binom`, `poisson`, etc.) es una instancia lista para usar de una de estas dos clases base.

## De la distribución empírica a la teórica

Un [[histograma]] o una [[distribución de frecuencias]] describen la forma de los datos **que efectivamente tenés**. Una distribución de `scipy.stats` es un **modelo teórico**: una curva matemática que, si se ajusta bien, permite calcular probabilidades para valores que no están en tu muestra, no solo describir los que sí están.

## Crear y usar una distribución

```python
from scipy import stats

normal = stats.norm(loc=170, scale=10)   # loc = media, scale = desvío estándar
```

Una vez creada ("congelada", con sus parámetros fijos), la distribución responde a cuatro preguntas básicas:

```python
normal.pdf(170)      # densidad de probabilidad en x=170 (el "alto" de la curva ahí)
normal.cdf(180)       # P(X <= 180) -> probabilidad acumulada hasta 180
normal.ppf(0.975)     # el x tal que P(X <= x) = 0.975 -> percentil 97.5 (la inversa de cdf)
normal.rvs(size=100, random_state=42)   # 100 valores simulados con esa distribución
```

> [!important] Las cuatro funciones, en una tabla
> | Método | Pregunta que responde |
> |---|---|
> | `pdf(x)` | ¿Qué tan densa es la probabilidad en `x`? (curva de densidad) |
> | `cdf(x)` | ¿Qué proporción de la distribución queda **por debajo** de `x`? |
> | `ppf(q)` | ¿Qué valor `x` acumula la proporción `q`? (la inversa de `cdf`) |
> | `rvs(size)` | Generame `size` valores simulados con esta distribución |
>
> `cdf` **es**, por definición, el área bajo la curva de `pdf` desde $-\infty$ hasta `x` — una integral. El desarrollo completo de esa relación (y por qué el área total bajo cualquier `pdf` siempre da 1) está en [[05 - Integrales]] de Matemática.

> [!tip] `ppf` es exactamente un percentil teórico
> `normal.ppf(0.75)` responde la misma pregunta que un [[medidas de posición|percentil]] de Estadística ($q_3$: el valor que acumula el 75 % de los datos) — la diferencia es que acá el 75 % se calcula sobre la **curva teórica**, no contando datos de una muestra.

## Ejemplo completo: una pregunta de punta a punta

Si la altura de un grupo se modela como $N(170, 10)$ (media 170 cm, desvío 10 cm), **¿qué proporción mide más de 180 cm?**

```python
altura = stats.norm(loc=170, scale=10)

p_hasta_180 = altura.cdf(180)        # 0.8413 -> 84.13% mide 180 cm o menos
p_mas_de_180 = 1 - p_hasta_180        # 0.1587 -> ~16% mide más de 180 cm
```

Y la pregunta inversa: **¿a partir de qué altura está el 10 % más alto del grupo?**

```python
altura.ppf(0.90)   # 182.8 -> el 10% más alto mide más de 182.8 cm
```

Ninguno de estos dos números viene de contar datos reales — salen enteros de la curva teórica, una vez que se fijan `loc` y `scale`.

## Distribuciones más usadas

```python
stats.norm(loc=0, scale=1)        # normal estándar
stats.uniform(loc=0, scale=1)     # uniforme continua en [0, 1)
stats.binom(n=10, p=0.5)          # binomial: n ensayos, probabilidad p de éxito
stats.poisson(mu=3)               # Poisson: cantidad de eventos por intervalo
```

> [!note] Discreta vs. continua, la misma distinción de Estadística
> `binom` y `poisson` no tienen `.pdf()` (una probabilidad puntual no tiene sentido en variables continuas de densidad); usan `.pmf()` (*probability mass function*) en su lugar. Es el mismo criterio de [[el ciclo estadístico (PPDAC)|cualitativa/cuantitativa discreta/continua]] visto en la [[01 - Como dar sentido a los datos|clase 1 de Estadística]], aplicado a modelos en vez de a datos observados.

## Ajustar una distribución a datos reales

```python
datos = [39.1, 39.5, 40.3, 36.7, 39.3, 38.9, 39.2]
media, desvio = stats.norm.fit(datos)   # estima los parámetros por máxima verosimilitud
```

`fit()` busca los parámetros que hacen más probable haber observado justo estos datos — es el puente entre una distribución teórica y un conjunto de datos concreto, resolviendo por dentro un problema de **máxima verosimilitud** (ver [[06 - Verosimilitud y estimación por máxima verosimilitud]] de Matemática para el mecanismo completo). Se profundiza en [[09 - Estimacion de densidad y ajuste de distribuciones]].

## Relacionado
- [[01 - Introduccion a SciPy.stats]]
- [[histograma]]
- [[distribución de frecuencias]]
- [[09 - Estimacion de densidad y ajuste de distribuciones]]
