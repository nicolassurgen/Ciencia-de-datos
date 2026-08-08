---
titulo: Diagrama de tallo y hoja
materia: Estadística
tipo: concepto
tags:
  - estadistica
  - maestria
  - concepto
  - tema/variabilidad
fecha: 2026-08-03
---

# Diagrama de tallo y hoja

> [!definition] Diagrama de tallo y hoja (stem-and-leaf)
> Gráfico para variables **cuantitativas** que muestra la forma de la distribución **sin perder los datos originales**. Cada dato se separa en dos partes: el **tallo** (dígitos mayores, a la izquierda de un "|") y la **hoja** (el último dígito, a la derecha).

## Cómo leerlo

```
 9 | 1 3 4
10 | 0 2 2 5 7 8
11 | 1 3
```

Cada fila es un "tallo" (por ejemplo, la decena) y cada dígito a la derecha es una "hoja" (una observación individual). Girado 90°, el diagrama tiene la misma silueta que un [[histograma]] — es esencialmente un histograma "acostado".

## Ventaja frente al histograma

A diferencia del histograma, que **agrupa y pierde el valor exacto** de cada dato dentro de su intervalo, el tallo y hoja conserva los **valores originales**: se puede reconstruir el conjunto de datos completo a partir del gráfico. Es especialmente útil para conjuntos de datos pequeños o medianos, donde perder el detalle no compensa.

> [!tip] No hay una única forma de elegir tallo y hoja
> La división en tallo/hoja del ejemplo (decenas | unidades) es solo una posibilidad. También puede tomarse la parte entera como tallo y el primer decimal como hoja, o centena/decena como tallo y unidad como hoja — la elección depende de la escala de los datos y de cuántos tallos distintos conviene mostrar. Si un mismo tallo termina concentrando demasiadas hojas (una fila muy larga que no deja ver la forma), se lo puede **partir en dos líneas** (por ejemplo, separando las hojas 0-4 de las 5-9 dentro del mismo tallo) para recuperar la resolución visual del gráfico.

## Relacionado
- [[02 - El estudio de la variabilidad]]
- [[histograma]]
- [[diagrama de puntos (dot plot)]]
- [[distribución de frecuencias]]
