---
titulo: ¿Cómo dar sentido a los datos?
materia: Estadística
tipo: apunte
clase: 1
fecha: 2026-07-31
tags:
  - estadistica
  - maestria
  - tema/introduccion
  - pensamiento-estadistico
---

# Tema 1 — ¿Cómo dar sentido a los datos?

> [!abstract] Idea central de la clase
> Los datos por sí solos no dicen nada. Se transforman en **información** cuando se recolectan y analizan al servicio de una **pregunta** bien planteada. Ese recorrido —de la pregunta a la conclusión— es un proceso lógico y **circular**, y la Estadística acompaña *todas* sus etapas, no solo el cálculo.
>
> $$\text{INFORMACIÓN} = \text{datos con sentido} = \text{respuesta a preguntas}$$

---

## 1. Seis casos para empezar a pensar como estadístico

La profe abrió con seis situaciones históricas. No son anécdotas: cada una ilustra una forma distinta de "dar sentido a los datos" y anticipa temas del curso. Las amplío porque en las diapositivas solo quedan enunciadas.

> [!example]- Caso 1 — John Snow: *¿Qué tenían en común las personas que enfermaban?*
> Londres, epidemia de cólera de **1854**. La teoría dominante culpaba a los "miasmas" (aire viciado). Snow, en cambio, **mapeó** las muertes sobre un plano de la ciudad y notó que se concentraban alrededor de una bomba de agua pública en Broad Street. Al retirar la manija de la bomba, los casos cayeron. Es un ejemplo temprano de **razonamiento con datos espaciales** y de buscar el **factor común** detrás de un fenómeno. Considerado un origen de la epidemiología moderna.

> [!example]- Caso 2 — Florence Nightingale: *¿Cómo convencerías al gobierno de que debía actuar?*
> Guerra de Crimea. Nightingale documentó que la mayoría de los soldados no morían en batalla, sino por **infecciones evitables** en los hospitales. Para persuadir a las autoridades diseñó un gráfico hoy famoso (el *diagrama de rosa* o *coxcomb*). Lección: los datos necesitan una **visualización efectiva** para mover decisiones. Fue una pionera de la estadística aplicada a la salud pública.

> [!example]- Caso 3 — Ignaz Semmelweis: *¿Qué podría estar ocurriendo?*
> Viena, hospital con dos salas de maternidad. En una, la mortalidad materna por **fiebre puerperal** era muchísimo mayor que en la otra. La diferencia: en la sala con más muertes atendían médicos que venían de hacer autopsias **sin lavarse las manos**. Semmelweis introdujo el lavado con solución clorada y la mortalidad se desplomó. Ejemplo de **comparación entre grupos** para aislar una causa (años antes de la teoría de los gérmenes).

> [!example]- Caso 4 — Abraham Wald: *¿Dónde reforzarías el blindaje?*
> Segunda Guerra Mundial. Los aviones volvían de combate con impactos de bala concentrados en ciertas zonas (alas, cola). La intuición decía: blindar donde hay más impactos. Wald razonó al revés: esos son los aviones que **sobrevivieron**; hay que blindar donde **no** hay impactos, porque los aviones alcanzados ahí no volvieron. Es el ejemplo clásico de **sesgo de supervivencia** (survivorship bias) y de por qué importa qué unidades *no* están en tus datos.

> [!example]- Caso 5 — Challenger: *¿Lanzarías el transbordador?*
> **1986**. El lanzamiento estaba programado, había presión por no postergarlo, pero también dudas técnicas. Las juntas ("O-rings") perdían elasticidad con el frío y esa mañana la temperatura era muy baja. Los datos disponibles sugerían el riesgo, pero no se analizaron ni comunicaron bien. El transbordador explotó. Lección dura sobre **decisión bajo incertidumbre** y sobre presentar la evidencia de forma que se entienda a tiempo.

> [!example]- Caso 6 — Ernest Codman: *¿Cómo comprobarías si los tratamientos realmente eran exitosos?*
> Un cirujano que a principios del siglo XX propuso algo revolucionario: hacer **seguimiento sistemático de cada paciente** para registrar el *resultado final* del tratamiento (su idea del "end result"). No alcanza con afirmar que algo funciona: hay que **medir y registrar** los resultados. Antecedente de la medicina basada en evidencia y de la evaluación de la calidad.

> [!tip] Hilo común
> En los seis casos, alguien se hizo una **pregunta**, buscó **datos pertinentes** (no cualquier dato) y los **comparó, mapeó o visualizó** para llegar a una conclusión que cambió una decisión. Eso es pensamiento estadístico.

---

## 2. De la realidad a la información

El punto de partida no es el dato, es la **situación real** que genera un problema y **preguntas para responder**. Hace falta un genuino *compromiso con la problemática*.

![[Realidad a informacion.png]]

Para responder esas preguntas se necesitan datos… **pero no cualquier dato**. El tipo de pregunta condiciona qué datos hay que recolectar y cómo.

---

## 3. El ciclo estadístico (PPDAC)

> [!important] Hay que empezar por las preguntas y seguir un camino **circular**
> El proceso no es una línea recta que termina: las conclusiones suelen abrir **nuevas preguntas** y reinician el ciclo.

Las etapas, en orden:

1. **P — Planteo del Problema** → definir qué queremos responder.
2. **P — Planificación del Estudio Estadístico** → diseñar cómo obtendremos los datos.
3. **D — Recolección de Datos** → conseguir los datos pertinentes.
4. **A — Análisis de los Datos** → describir, resumir, inferir.
5. **C — Obtención de Conclusiones** → interpretar en el contexto del problema.

> [!warning] Advertencia clave
> Aunque los "métodos estadísticos" se concentran en la **recolección** y el **análisis**, no pueden desvincularse del resto. Un buen cálculo sobre un mal diseño no salva nada.
>
> **Los métodos estadísticos NO SUPLEN las falencias de diseño.**

---

## 4. Cuestiones a definir en el planteo del problema

Antes de recolectar nada, hay que responder: *¿qué unidades queremos estudiar? ¿qué información necesitamos de ellas? ¿nos interesa alguna medida que resuma esa información?*

### Población y unidad elemental

> [!definition] Población
> Conjunto de **todos** los elementos (unidades elementales) bajo estudio. Puede ser **finita o infinita**.
>
> Debe estar **perfectamente delimitada en tiempo y espacio**. Para definirla se usan **criterios de inclusión / exclusión**.

> [!definition] Unidad elemental
> Cada uno de los elementos que componen la población. Es la "unidad de análisis" sobre la que medimos las variables.

**¿Por qué importa definir bien la población?** Porque de eso depende la [[validez externa]] de las conclusiones: hasta qué grupo tengo derecho a extender lo que encontré.

---

## 5. Variables

> [!definition] Variable
> Cualquier **característica** que puede asumir **diferentes valores** en las unidades elementales.

> [!note] ¿Por qué clasificar las variables?
> Las herramientas de análisis que se pueden aplicar dependen, entre otras cosas, del **tipo de variable** y de la **escala** con que se mida. Por eso conviene definir esto con claridad desde el principio.

### 5.1. Cualitativas vs. cuantitativas

- **Cualitativas** → sus "valores" son en realidad **categorías o niveles**, *aunque se codifiquen con números*. (Que codifiques "Sí = 1 / No = 0" no las vuelve numéricas.)
	- *Ejemplos:* máximo nivel educativo, material de construcción de una vivienda, presencia de un síntoma, condición de defectuoso, opinión sobre una ley.
- **Cuantitativas** → sus valores son **numéricos** (tiene sentido operar con ellos).

### 5.2. Dentro de las cuantitativas: discretas vs. continuas

- **Discretas** → sus valores se asocian a los números **enteros**, casi siempre a los naturales y el 0, porque surgen de **contar**.
	- *Ejemplos:* nº de integrantes de una familia, nº de habitaciones de una vivienda, nº de imperfecciones de un rollo de alambre.
- **Continuas** → sus valores se asocian a los números **reales** y generalmente surgen de una **medición**.
	- *Ejemplos:* ingreso familiar, peso de un componente, diámetro de tubos, nivel de colesterol en sangre.

> [!tip] Regla mnemotécnica
> **Cuento → discreta. Mido → continua.**

---

## 6. Escalas de medición

Cuatro escalas, en orden creciente de "qué operaciones permiten". Cada escala **acumula** las capacidades de la anterior.

| Escala | ¿Distingue? | ¿Ordena? | ¿Diferencias? | ¿Cocientes? | Cero absoluto | Asociada a | Ejemplo |
|---|:---:|:---:|:---:|:---:|:---:|---|---|
| **Nominal** | ✅ | ❌ | ❌ | ❌ | — | Cualitativas | Material de la vivienda; motivo de consulta |
| **Ordinal** | ✅ | ✅ | ❌ | ❌ | — | Cuali/cuanti* | Nivel de estudios; nivel de contaminación (bajo/medio/alto) |
| **Intervalo** | ✅ | ✅ | ✅ | ❌ | No | Cuantitativas | Temperatura en °C |
| **Razón** | ✅ | ✅ | ✅ | ✅ | **Sí** | Cuantitativas | Nivel de colesterol; peso; ingreso |

\* Ver la nota sobre ordinales más abajo.

**Detalle de cada una:**

- **Nominal** — solo permite *distinguir* una unidad de otra. Una casa de ladrillo es distinta de una de adobe, pero no hay un orden. *(Asociada a variables cualitativas.)*
- **Ordinal** — distingue **y ordena**. Secundaria completa es "más" que primaria completa; nivel medio de contaminación es mayor que bajo. **Diferencio y ordeno**, pero las distancias entre categorías no son necesariamente comparables.
- **Intervalo** — distingue, ordena y permite **restar** (diferencias), pero **no cocientes**, porque el **0 no es absoluto**. 20 °C es 10 grados más que 10 °C… pero **no es "el doble" de calor** (el 0 °C es convencional, no ausencia de temperatura).
- **Razón** — permite todo, **incluidos los cocientes**, porque el **0 es absoluto**. Alguien con 220 mg/l de colesterol tiene 20 mg/l más *y* un 10 % más que alguien con 200 mg/l. Esa afirmación de "10 % más" solo es válida en escala de razón.

> [!note] Las variables ordinales son un caso frontera
> Se pueden tratar **como cualitativas si tienen pocos niveles** o **como cuantitativas si tienen muchos**. Es una decisión del analista según el objetivo.

> [!tip] Para el análisis, ¿qué distinción importa más?
> Entre **intervalo y razón**, para el análisis de datos **no suele importar** la diferencia. Lo que **sí importa** siempre es distinguir si la variable cuantitativa es **discreta o continua**.

> [!info] Material complementario (no visto en clase) — Otra forma de nombrar lo mismo
> Las herramientas de ciencia de datos (Pandas, scikit-learn) no suelen hablar de "nominal/ordinal/intervalo/razón" — usan una clasificación más práctica y equivalente: **continuous** (cuantitativa continua), **discrete** (cuantitativa discreta), **categorical** (cualitativa, incluida la nominal), **ordinal** (igual que acá) y **binary** (categórica de solo 2 niveles, un caso particular de categorical). Es la misma idea de la clase, con otro vocabulario — el que vas a encontrar en la documentación de las librerías. *Fuente: [[Practical Statistics for Data Scientists]] (Bruce & Bruce), cap. 1.*

### Mapa de la clasificación

![[Escalas y estructura de variables.png]]

---

## 7. Parámetro

> [!definition] Parámetro
> Una **medida que resume información de todas las unidades de la población**. Se simbolizan generalmente con **letras griegas**.

Ejemplos:
- Proporción de viviendas de la población donde predomina la madera → $\pi$
- Nivel de colesterol **promedio** de las personas de la población → $\mu$

> [!info] Adelanto conceptual
> El parámetro es una característica de la **población** (normalmente desconocido). Cuando trabajamos con una **muestra**, calculamos un **estadístico** (con letras latinas, p. ej. $\bar{x}$, $p$) para *estimarlo*. Esa distinción es el corazón de la inferencia que viene más adelante. → [[parámetro vs estadístico]]

---

## 8. Planificación del estudio estadístico

Planteadas las preguntas, surge el **diseño** del estudio. Principales clasificaciones:

### Censo vs. muestreo
- **Estudio poblacional (censo)** → se observan *todas* las unidades. Las conclusiones son definitivas para esa población.
- **Estudio por muestreo** → se observa una parte. Requiere **herramientas de inferencia** para generalizar a toda la población, con cierto **margen de error** y **riesgos controlados**. Importa definir el **tipo** y el **tamaño** de la muestra.

> [!info] Material complementario (no visto en clase) — ¿Qué significa "el tipo" de muestra?
> - **Muestreo aleatorio simple** → cada unidad de la población tiene la **misma probabilidad** de ser elegida en cada extracción; no hay subgrupos de por medio.
> - **Muestreo estratificado** → se divide la población en **estratos** (subgrupos homogéneos, ver [[estratificación]]) y se muestrea aleatoriamente **dentro de cada estrato** — asegura representación de subgrupos que un muestreo simple podría pasar por alto.
> - **Con reposición vs. sin reposición** → con reposición, una unidad elegida **vuelve** a la población y puede salir sorteada de nuevo; sin reposición, una vez elegida **queda afuera** del resto de las extracciones.
>
> Más muestra no arregla una muestra mal seleccionada: la encuesta de *Literary Digest* de 1936 (ver [[validez externa]]) encuestó a 10 millones de personas mal elegidas y predijo mal una elección que Gallup acertó con apenas 2.000 personas bien seleccionadas. *Fuente: [[Practical Statistics for Data Scientists]] (Bruce & Bruce), cap. 2.*

### Experimento
Se estudia el **efecto de uno o más factores** sobre variables de respuesta, **introduciendo cambios deliberados** en esos factores y tratando de **controlar** los factores no controlables. → [[diseño de experimentos]]

### Transversal vs. longitudinal (según el tiempo)
- **Transversal** → un **corte** en un momento del tiempo (una foto).
- **Longitudinal** → se estudia el comportamiento a **través del tiempo**, o se sigue a un mismo grupo (**cohorte**) en distintos momentos (una película).

---

## 9. Recolección de los datos

Dos grandes vías según el origen:

- **Fuentes secundarias** → datos **ya existentes**, recolectados por otros (bases de entidades públicas o privadas).
- **Fuentes primarias** → mecanismos de **primera mano** que consultan directamente a personas, familias, instituciones, clientes, alumnos, industrias, etc.

En esta etapa se **definen los instrumentos** de registro, se **entrena y supervisa** a quienes hacen el relevamiento.

> [!definition] Trazabilidad
> Posibilidad de **identificar, rastrear y recuperar** las unidades de las que se extrajeron los datos (mediante códigos elaborados a tal fin). Permite recuperar características de interés: en qué horario se produjo, con qué máquina o lote de materia prima, con qué equipo se midió, etc.

---

## 10. La matriz de datos

Terminada la recolección, se cuenta con una **matriz de datos**: los **individuos en las filas** y las **variables en las columnas**.

|  | Var. X | Var. Y | … | Var. Z |
|---|---|---|---|---|
| **1** | $x_1$ | $y_1$ | … | $z_1$ |
| **2** | $x_2$ | $y_2$ | … | $z_2$ |
| ⋮ | ⋮ | ⋮ | | ⋮ |
| **n (o N)** | $x_n$ | $y_n$ | … | $z_n$ |

Con la matriz armada **comienza la etapa de análisis**. (Nota: se usa $n$ para el tamaño de una **muestra** y $N$ para el de una **población**.)

> [!note] En código, esto es un DataFrame
> La matriz de datos, tal cual, es lo que en Pandas se llama un `DataFrame`: individuos en las filas (el `Index`), variables en las columnas. Ver [[01 - Introduccion a Series y DataFrame]].

---

## 11. Análisis de los datos

Se realizan muchas tareas, en capas:

> [!note]+ Tratamiento primario
> Se analiza la **calidad** de los datos: se corrigen datos erróneos, se transforman si es necesario, se eliminan **outliers**, se completan **datos faltantes**, etc.

> [!note]+ Análisis descriptivo
> Se construyen **gráficos y tablas** y se obtienen **medidas de resumen** (indicadores) para describir el conjunto.
> - Si se trabajó con **toda la población** → las conclusiones son **definitivas**.
> - Si se trabajó con una **muestra** → hace falta pasar a herramientas inferenciales.
>
> *En código*: las medidas de resumen se calculan con [[04 - Agregaciones y estadistica descriptiva|NumPy]] o `df.describe()` de [[01 - Introduccion a Series y DataFrame|Pandas]]; los gráficos, con [[01 - Introduccion y primer grafico|Matplotlib]] o [[01 - Introduccion a Seaborn|Seaborn]] (más directo para esto último, ver [[02 - El estudio de la variabilidad]]).

> [!note]+ Análisis inferencial
> Se aplican herramientas como **intervalos de confianza** y **pruebas de hipótesis** para extender las conclusiones **de la muestra a toda la población**.
>


> [!tip] Consistencia de los datos
> Otra tarea importante: verificar la **coherencia entre respuestas**. Si no la hay, es probable que haya datos falsos o que la pregunta no se haya comprendido. Por eso, al diseñar cuestionarios, a veces se **repite intencionalmente** la misma cuestión redactada de dos formas distintas y mezclada, como forma de **validación**.

---

## 12. Conclusiones y validez

En la etapa de conclusiones hay que **tomar todos los resultados** de los análisis y **concluir en el contexto del problema planteado**.

Se habla de **validez** en dos sentidos:

> [!definition] Validez externa
> Cuando los resultados son **aplicables a grupos mayores o distintos** de los que efectivamente se observaron. Depende de haber definido bien la población y de cómo se obtuvo la muestra.

> [!definition] Validez interna
> Cuando las **comparaciones** hechas *dentro* de la investigación **no están sesgadas**.

**Ejemplos para pensar la validez externa (¿puedo generalizar?):**
- Se estudió la efectividad de una vacuna **solo en varones adultos**. ¿Puedo hablar de su efectividad para **toda** la población? 🤔
- Encuesta de opinión sobre cursos de posgrado, pero se entrevista **solo a los alumnos del posgrado en Calidad**. ¿Es la opinión de **todos** los alumnos de posgrado? 🤔
- ¿Qué pasa si analizo datos de personas que **respondieron voluntariamente**? (sesgo de autoselección) 🤔

> [!info] Material complementario (no visto en clase) — [[sesgo de autoselección]]
> Ocurre cuando quienes forman parte de la muestra lo hacen por una decisión **propia** (responder una encuesta, escribir una reseña), y esa decisión está relacionada con lo que se quiere medir. El ejemplo clásico: la encuesta de *Literary Digest* de 1936 encuestó a más de 10 millones de personas y predijo mal la elección presidencial de EE. UU.; Gallup, con solo 2.000 personas bien seleccionadas, acertó. Desarrollo completo en la nota aparte. *Fuente: [[Practical Statistics for Data Scientists]] (Bruce & Bruce), cap. 2.*

**Ejemplo para pensar la validez interna (¿la comparación es limpia?):**
- Una empresa fabrica el mismo producto en dos plantas de **localidades distintas**. Usa materia prima del proveedor **A en una planta** y del **B en la otra**, y compara la calidad resultante. ¿Puede concluir que un proveedor es mejor? **No limpiamente**: la localidad, la maquinaria y otros factores están **confundidos** con el proveedor. La diferencia observada podría deberse a la planta, no a la materia prima. → [[variable de confusión]]

---

## 13. Estudios exploratorios vs. confirmatorios

Puede ocurrir que **todavía no tengamos preguntas** que responder. Ahí caben los **estudios exploratorios**, que permiten:
- familiarizarnos con la temática,
- identificar variables importantes y descartar otras,
- **formular hipótesis** o preguntas para responder más adelante.

Luego, ya con hipótesis formuladas, un **estudio confirmatorio** —diseñado especialmente— las **pone a prueba**.

![[Exploratorio a confirmatorio.png]]

---

## 14. Cierre — El pensamiento estadístico

> [!quote] Síntesis de la clase
> La **Estadística** proporciona métodos para **obtener, organizar y resumir** datos que se convierten luego en **información útil**, y provee herramientas para la **toma de decisiones en presencia de variabilidad**.
>
> Antes de obtener los datos hace falta un **correcto planteo del problema** y una **adecuada planificación**. En todas estas etapas, el papel de la Estadística es **primordial**.
>
> Y por encima de los métodos y herramientas específicas está lo más importante: el **pensamiento estadístico**.

---

## Conceptos para desarrollar en notas aparte
- [[población y muestra]]
- [[validez externa]] · [[validez interna]]
- [[parámetro vs estadístico]]
- [[escalas de medición]]
- [[sesgo de supervivencia]] · [[sesgo de autoselección]]
- [[variable de confusión]]
- [[diseño de experimentos]]

## Preguntas de repaso
1. ¿Por qué el ciclo PPDAC se dibuja como circular y no como una lista de 5 pasos que se hacen una sola vez?
2. "20 °C es el doble de calor que 10 °C" — ¿es una afirmación válida? ¿Por qué depende de la escala de medición?
3. ¿Cuál es la diferencia entre un parámetro y un estadístico, y por qué usan notaciones distintas (griega vs. latina)?
4. Una encuesta de opinión sobre cursos de posgrado entrevista solo a alumnos del posgrado en Calidad — ¿qué tipo de validez está en juego, y por qué?
5. ¿Por qué "más muestra" no arregla necesariamente una muestra mal seleccionada? (pensar en el caso *Literary Digest* vs. Gallup)

## Preguntas que me quedaron
-
-

## Para la próxima clase
-
