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

> [!example] Un experimento de ingeniería completo: sembradora neumática
> Para comparar dos sembradoras de maíz, se usaron dos lotes de campo similares: cuál sembradora va a cada lote se decidió **por sorteo** (aleatorización), las bolsas de semilla usadas fueron del mismo peso y se asignaron también al azar, y ambos lotes se sembraron el **mismo día y con el mismo clima** — para que la única diferencia sistemática entre los dos grupos fuera, efectivamente, la sembradora. Es un ejemplo más concreto que el genérico "tratamiento A vs. tratamiento B": muestra en la práctica qué significa "controlar todo lo demás" al diseñar un experimento real. *Fuente: [[Estadística para la resolución de problemas en Ingeniería]], cap. 1.*

## Principios clave

> [!important] Aleatorización
> Asignar los tratamientos **al azar** a las unidades experimentales. Es la herramienta principal contra las [[variable de confusión|variables de confusión]]: si algo no controlado influye, la aleatorización tiende a repartirlo parejo entre los grupos comparados, protegiendo la [[validez interna]].

> [!important] Replicación
> Aplicar cada tratamiento a **más de una** unidad experimental. Permite estimar la variabilidad **dentro** de cada tratamiento y así distinguir un efecto real de simple ruido (variabilidad natural, ver [[causas comunes y causas especiales]]).

> [!important] Bloqueo
> Agrupar unidades **similares** entre sí (bloques) antes de asignar tratamientos, y comparar **dentro** de cada bloque. Sirve para neutralizar una fuente de variabilidad conocida (p. ej. comparar proveedores dentro de cada planta) que de otro modo se confundiría con el factor de interés.

> [!important] ¿Por qué hace falta un grupo de control?
> Sin un grupo de control que reciba un tratamiento de referencia (o ningún tratamiento), no hay garantía de que "todo lo demás se mantuvo igual" entre lo que se mide antes y después. Comparar el resultado de un tratamiento nuevo contra un valor histórico (un "baseline" de otra época, otras condiciones) deja sin controlar cualquier otro factor que haya cambiado con el tiempo — exactamente el problema que resuelve tener un grupo comparable, tratado en paralelo y bajo las mismas condiciones. Es la misma lógica de la aleatorización, aplicada a la necesidad de tener con qué comparar.

> [!tip] Ciego y doble ciego (*blind* / *double-blind*)
> En un experimento **ciego**, las unidades experimentales (personas, en un ensayo clínico) no saben qué tratamiento están recibiendo — evita que el solo hecho de *saberse* tratado influya en el resultado medido. En uno **doble ciego**, tampoco lo saben quienes administran el tratamiento o evalúan la respuesta — evita que las expectativas del investigador influyan, consciente o inconscientemente, en cómo se mide o registra el resultado. No siempre es posible (no se puede "cegar" cuál sembradora se está usando), pero cuando aplica es una protección adicional contra sesgos que la aleatorización sola no cubre.

> [!warning] El estadístico de comparación se decide antes de mirar los datos
> Elegir **qué** métrica se va a usar para comparar los tratamientos (la media, una proporción, otra medida) *después* de ver cómo salieron los resultados abre la puerta a elegir, sin darse cuenta, la métrica que más favorece la conclusión que ya se esperaba encontrar. Definir el criterio de comparación **antes** de ejecutar el experimento es un principio de diseño, no de análisis posterior — protege contra ese sesgo del investigador incluso antes de llegar a cualquier prueba de hipótesis.

> [!note] Los límites éticos del diseño experimental
> No todo lo que mejora la validez de un experimento es automáticamente aceptable. Un caso real y discutido: en 2014, una red social manipuló el tono emocional del contenido mostrado a cientos de miles de usuarios, para medir el efecto sobre sus propias publicaciones, sin pedirles consentimiento explícito más allá de los términos de uso generales del servicio. En experimentos de negocio (precios, títulos, diseño de una página) rara vez se pide consentimiento explícito a cada participante, pero existe un límite ético entre eso y una intervención que pueda afectar el bienestar de las personas — un diseño técnicamente impecable no exime de esa consideración. *Fuente: [[Practical Statistics for Data Scientists]] (Bruce & Bruce), cap. 3.*

## Por qué un buen diseño es indispensable

> [!warning] Los métodos estadísticos NO suplen las falencias de diseño
> Un cálculo impecable sobre datos mal diseñados no salva la conclusión. El diseño experimental es la etapa de **Planificación** del [[el ciclo estadístico (PPDAC)|ciclo PPDAC]]: se decide **antes** de recolectar datos, y de ella depende si después va a ser posible aislar el efecto que se busca.

> [!note] Cómo se analiza el resultado
> Diseñar bien el experimento (esta nota) es la mitad del trabajo; la otra mitad es decidir si la diferencia observada entre tratamientos es real o puede deberse al azar. Eso es exactamente lo que hacen las pruebas de hipótesis — todavía no vistas en la clase, pero ya cubiertas por SciPy:
> ```python
> from scipy import stats
> stats.ttest_ind(tratamiento_a, tratamiento_b)        # 2 tratamientos
> stats.f_oneway(tratamiento_a, tratamiento_b, tratamiento_c)  # 3 o más (ANOVA)
> ```
> Ver [[06 - Tests de hipotesis - una y dos muestras]].

## Relacionado
- [[estudio observacional vs experimental]]
- [[causalidad vs asociación]]
- [[01 - Como dar sentido a los datos]]
- [[variable de confusión]]
- [[validez interna]]
- [[causas comunes y causas especiales]]
- [[06 - Tests de hipotesis - una y dos muestras]]
