---
titulo: Parámetro vs estadístico
materia: Estadística
tipo: concepto
tags:
  - estadistica
  - maestria
  - concepto
  - tema/introduccion
fecha: 2026-08-03
---

# Parámetro vs estadístico

Esta distinción es el corazón de la **inferencia estadística**: casi todo lo que se hace al pasar de una muestra a conclusiones sobre la población gira en torno a esta diferencia.

> [!definition] Parámetro
> Una medida que **resume información de todas las unidades de la [[población y muestra|población]]**. Es un valor **fijo** (aunque generalmente **desconocido**). Se simboliza con **letras griegas**.
> - Proporción poblacional → $\pi$
> - Media poblacional → $\mu$
> - Varianza poblacional → $\sigma^2$

> [!definition] Estadístico
> Una medida calculada a partir de los datos de una **muestra**, que se usa para **estimar** el parámetro correspondiente. Es una **variable aleatoria** (cambia de muestra a muestra). Se simboliza con **letras latinas**.
> - Proporción muestral → $p$ o $\hat{p}$
> - Media muestral → $\bar{x}$ o $\bar{y}$
> - Varianza muestral → $s^2$

## Tabla comparativa

| | Parámetro | Estadístico |
|---|---|---|
| Se calcula sobre | Población (todas las unidades) | Muestra (una parte) |
| Valor | Fijo, generalmente desconocido | Varía de muestra a muestra |
| Notación | Griega ($\mu$, $\sigma$, $\pi$) | Latina ($\bar{x}$, $s$, $p$) |
| Rol | Lo que queremos conocer | Lo que usamos para estimarlo |

> [!important] Por qué importa
> Cuando trabajamos con una muestra en lugar de un censo, no conocemos el parámetro: solo tenemos el estadístico. La inferencia estadística (intervalos de confianza, pruebas de hipótesis) se ocupa precisamente de **cuantificar qué tan bien** el estadístico estima al parámetro, y con qué margen de error.

> [!note] En código
> `np.mean(muestra)`, `np.std(muestra, ddof=1)` (ver [[04 - Agregaciones y estadistica descriptiva]]) calculan el **estadístico**. El **parámetro** poblacional casi nunca se calcula — es lo que se busca estimar. Cuando llegue la inferencia formal (intervalos de confianza, pruebas de hipótesis), la skill `statistical-analysis` instalada en este proyecto cubre justamente eso, igual que [[06 - Tests de hipotesis - una y dos muestras]] y [[08 - Metodos de remuestreo]] de SciPy.

## Relacionado
- [[01 - Como dar sentido a los datos]]
- [[población y muestra]]
- [[grados de libertad]]
- [[04 - Agregaciones y estadistica descriptiva]]
- [[06 - Tests de hipotesis - una y dos muestras]]
