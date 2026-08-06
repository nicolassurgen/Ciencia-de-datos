---
titulo: Valores atípicos
materia: Estadística
tipo: concepto
tags:
  - estadistica
  - maestria
  - concepto
  - tema/variabilidad
fecha: 2026-08-03
---

# Valores atípicos

> [!definition] Valor atípico (outlier)
> Observación que se **aparta notoriamente** del resto del conjunto de datos. Puede deberse a un **error** (de carga, medición o tipeo) o ser un valor **real pero extremo**. Distinguir entre ambos casos es tarea del [[tratamiento primario]] de los datos.

## Cómo se detectan

> [!important] Criterio del boxplot: 1.5 · RIQ
> Se considera atípico cualquier dato que caiga fuera de:
> $$[\,q_1 - 1{,}5 \cdot \text{RIQ}\ ,\ \ q_3 + 1{,}5 \cdot \text{RIQ}\,]$$
> Ver [[boxplot]] para el detalle visual y un ejemplo aplicado.

Otros criterios habituales (no vistos en la clase, pero de uso común): distancia en desvíos estándar respecto de la media (z-score), o métodos basados en la mediana y el RIQ que son más robustos que el z-score cuando ya hay atípicos presentes.

```python
from scipy import stats
z = stats.zscore(x)   # |z| > 3 suele marcarse como sospechoso
```

> [!warning] El z-score no es robusto
> Se calcula con media y desvío estándar — las mismas medidas **no robustas** de la sección siguiente. Si ya hay atípicos muy extremos, inflan la media y el desvío, lo que puede **esconder** atípicos menos extremos. El criterio 1.5·RIQ de arriba, basado en percentiles, no tiene ese problema. Ver [[05 - Transformaciones y deteccion de atipicos]] de SciPy.

## Por qué distorsionan tanto algunas medidas

Medidas como la **media** o la **varianza** usan **todos** los valores y los combinan con sumas (o sumas de cuadrados), por lo que un valor muy alejado tiene un peso desproporcionado. Medidas como la **mediana** o el **RIQ**, basadas en percentiles, ignoran directamente los extremos y por eso son [[robustez estadística|robustas]] frente a atípicos.

## Qué hacer con ellos

No hay una regla única: depende de si el atípico es un error (se corrige o elimina, ver [[tratamiento primario]]) o un valor legítimo (se conserva, y conviene además reportar medidas robustas junto con las clásicas para no dar una imagen distorsionada).

> [!note] En código
> `sns.boxplot()` en Seaborn (ver [[06 - Variables categoricas (boxplot, violinplot, barplot)]]) ya marca los atípicos con el criterio 1.5·RIQ automáticamente. Para un chequeo más formal (IQR y z-score, con recomendaciones), la skill `statistical-analysis` instalada en este proyecto trae `detect_outliers()`.

## Relacionado
- [[02 - El estudio de la variabilidad]]
- [[boxplot]]
- [[tratamiento primario]]
- [[robustez estadística]]
- [[06 - Variables categoricas (boxplot, violinplot, barplot)]]
- [[05 - Transformaciones y deteccion de atipicos]]
