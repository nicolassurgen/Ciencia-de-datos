---
titulo: Diseño de experimentos
materia: Estadística
tipo: concepto
tags:
  - estadistica
  - maestria
  - concepto
  - tema/introduccion
fecha: 2026-08-03
---

# Diseño de experimentos

> [!definition] Experimento
> Estudio en el que se analiza el **efecto de uno o más factores** sobre una o más variables de respuesta, **introduciendo cambios deliberados** en esos factores y tratando de **controlar** los factores no controlables. Se diferencia de un estudio **observacional**, donde el investigador no interviene, solo observa.

## Elementos básicos

- **Factor** → variable que se manipula deliberadamente (p. ej. el proveedor de materia prima, la dosis de un medicamento).
- **Niveles / tratamientos** → los valores o combinaciones de valores que toma cada factor.
- **Variable de respuesta** → lo que se mide para evaluar el efecto (p. ej. calidad del producto, tiempo de remisión de síntomas).
- **Unidad experimental** → sobre qué se aplica el tratamiento.

## Principios clave

> [!important] Aleatorización
> Asignar los tratamientos **al azar** a las unidades experimentales. Es la herramienta principal contra las [[variable de confusión|variables de confusión]]: si algo no controlado influye, la aleatorización tiende a repartirlo parejo entre los grupos comparados, protegiendo la [[validez interna]].

> [!important] Replicación
> Aplicar cada tratamiento a **más de una** unidad experimental. Permite estimar la variabilidad **dentro** de cada tratamiento y así distinguir un efecto real de simple ruido (variabilidad natural, ver [[causas comunes y causas especiales]]).

> [!important] Bloqueo
> Agrupar unidades **similares** entre sí (bloques) antes de asignar tratamientos, y comparar **dentro** de cada bloque. Sirve para neutralizar una fuente de variabilidad conocida (p. ej. comparar proveedores dentro de cada planta) que de otro modo se confundiría con el factor de interés.

## Por qué un buen diseño es indispensable

> [!warning] Los métodos estadísticos NO suplen las falencias de diseño
> Un cálculo impecable sobre datos mal diseñados no salva la conclusión. El diseño experimental es la etapa de **Planificación** del [[el ciclo estadístico (PPDAC)|ciclo PPDAC]]: se decide **antes** de recolectar datos, y de ella depende si después va a ser posible aislar el efecto que se busca.

> [!note] Cómo se analiza el resultado
> Diseñar bien el experimento (esta nota) es la mitad del trabajo; la otra mitad es decidir si la diferencia observada entre tratamientos es real o puede deberse al azar. Eso es exactamente lo que hacen las pruebas de hipótesis — todavía no vistas en la clase, pero cubiertas por la skill `statistical-analysis` instalada en este proyecto (`references/test_selection_guide.md` ayuda a elegir cuál corresponde según el diseño) y por SciPy:
> ```python
> from scipy import stats
> stats.ttest_ind(tratamiento_a, tratamiento_b)        # 2 tratamientos
> stats.f_oneway(tratamiento_a, tratamiento_b, tratamiento_c)  # 3 o más (ANOVA)
> ```
> Ver [[06 - Tests de hipotesis - una y dos muestras]].

## Relacionado
- [[01 - Como dar sentido a los datos]]
- [[variable de confusión]]
- [[validez interna]]
- [[causas comunes y causas especiales]]
- [[06 - Tests de hipotesis - una y dos muestras]]
