---
titulo: Sesgo de supervivencia
materia: Estadística
tipo: concepto
tags:
  - estadistica
  - maestria
  - concepto
  - tema/introduccion
fecha: 2026-08-03
---

# Sesgo de supervivencia

> [!definition] Sesgo de supervivencia (survivorship bias)
> Error de razonamiento que ocurre al analizar **solo las unidades que "sobrevivieron"** un proceso de selección, ignorando las que no llegaron a ser observadas — precisamente porque no sobrevivieron. Las conclusiones basadas solo en los sobrevivientes pueden ser **engañosas o directamente opuestas** a la realidad.

## El caso clásico: Abraham Wald

Segunda Guerra Mundial. Los aviones volvían de combate con impactos de bala concentrados en ciertas zonas (alas, cola). La intuición decía: **blindar donde hay más impactos**.

Wald razonó al revés: esos son los aviones que **sobrevivieron** y volvieron a la base. Había que blindar donde **no** hay impactos en los aviones que volvieron, porque los aviones alcanzados **ahí** probablemente no volvieron — no están en los datos.

```
Datos observados = aviones que SOBREVIVIERON
Datos faltantes  = aviones derribados (justamente los más informativos)
```

## La lección general

> [!important] Importa qué unidades NO están en los datos
> El sesgo de supervivencia es un caso particular de un problema más amplio de [[validez externa]]: si el mecanismo que decide qué unidades llegan a observarse está relacionado con la variable de interés, la muestra observada **no representa** a la población completa, aunque parezca grande o "completa" a simple vista.

## Otros ejemplos típicos

- Estudiar solo las **empresas que siguen existiendo** hoy para sacar conclusiones sobre "qué hace exitosa a una empresa" (las que quebraron no entran en el análisis).
- Analizar solo los **fondos de inversión activos** para medir el rendimiento promedio del mercado (los fondos que cerraron por bajo rendimiento no aparecen).

## Relacionado
- [[01 - Como dar sentido a los datos]]
- [[validez externa]]
