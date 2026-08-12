---
titulo: El estudio de la variabilidad en un conjunto de datos
materia: Estadística
tipo: apunte
clase: 2
fecha: 2026-08-01
tags:
  - estadistica
  - maestria
  - tema/variabilidad
  - estadistica-descriptiva
---

# Tema 2 — El estudio de la variabilidad en un conjunto de datos

> [!abstract] Idea central de la clase
> Todo proceso y todo fenómeno produce **variabilidad**: si medimos una característica sobre varias unidades, los valores no son idénticos. El objetivo del análisis descriptivo es **representar, resumir y entender ese patrón de variabilidad**. Las herramientas que usamos (gráficos y medidas) dependen del **tipo de variable** (cualitativa, cuantitativa discreta o continua) y de si los datos tienen o no una **dimensión temporal**.
>
> Para describir una distribución nos interesan tres cosas: **dónde se centra**, **cuánto se dispersa** y **qué forma tiene**.

> [!info] Enlace con el Tema 1
> Ya vimos el ciclo PPDAC y el [[tratamiento primario]] de los datos. Este tema es el corazón del **análisis descriptivo**: qué hacemos con los datos ya depurados de una **variable**, provengan de una **muestra** o de una **población**. → [[el ciclo estadístico (PPDAC)]]

---

## 1. ¿De dónde viene la variabilidad? El proceso y sus fuentes

La profe arrancó modelando un **proceso de producción genérico**: entran insumos, el proceso los transforma y sale un **producto o servicio**. Sobre ese producto **monitoreamos alguna característica** (peso, diámetro, etc.), y esa característica **varía**.

Las **fuentes de variabilidad** que alimentan al proceso:

- **Mano de obra**
- **Máquinas**
- **Materia prima**
- **Métodos de producción**
- **Métodos de medición** (¡el propio instrumento mide con error!)
- **Medio ambiente**

![[Ishikawa - 6M.png]]

> [!note] Esto es un diagrama causa-efecto (Ishikawa / "espina de pescado")
> Ese esquema de fuentes que confluyen en un proceso es, en la práctica, un **diagrama de Ishikawa** y las categorías clásicas son las **6 M**: Mano de obra, Máquinas, Materiales, Métodos, Medición y Medio ambiente. Es una herramienta habitual en control de calidad para organizar las posibles causas de variabilidad. → [[diagrama de Ishikawa]]

**El mismo esquema sirve fuera de la industria.** Ejemplo de la clase — *efecto de un medicamento en pacientes con cierta enfermedad*:

- Entradas: características personales, estadío de la enfermedad, cuestiones genéticas, dosis / forma de aplicación, presencia de enfermedades adicionales.
- Proceso: aplicación del medicamento.
- Salida: el **efecto**, que monitoreamos midiendo una característica (p. ej. *tiempo de remisión de los síntomas*), que **varía de paciente a paciente**.

> [!tip] Un marco conceptual útil (Shewhart / Deming)
> La variabilidad suele separarse en dos tipos:
> - **Causas comunes** → variabilidad "natural", inherente al proceso cuando funciona de forma estable. Produce un patrón **predecible**.
> - **Causas especiales (o asignables)** → algo puntual y ajeno al funcionamiento normal (una máquina desajustada, un lote de materia prima defectuoso). Rompen la estabilidad.
>
> Esta distinción explica por qué más adelante importa si los datos muestran o no un **comportamiento estable en el tiempo**.

---

## 2. ¿Cómo representamos / modelizamos la variabilidad?

**Punto de partida:** un conjunto de datos de **una única variable** —cualitativa, cuantitativa discreta o continua—, de una **muestra o una población**, y con el **tratamiento primario ya hecho** (datos depurados).

> [!important] Regla que atraviesa todo el tema
> **El tipo de variable determina qué gráfico y qué medidas puedo usar.** No se resume igual un motivo de queja (cualitativa) que un diámetro (continua).

La forma más básica de representar la variabilidad es la **distribución de frecuencias**: una tabla que dice, para cada valor o categoría, cuántas veces aparece.

| Frecuencia | Símbolo | Qué mide |
|---|---|---|
| **Absoluta** | $f_i$ | Cantidad de casos en la categoría/valor $i$ |
| **Relativa** | $h_i = f_i / n$ | Proporción del total (útil para comparar entre conjuntos de distinto tamaño) |
| **Absoluta acumulada** | $F_i$ | Casos hasta $i$ (solo tiene sentido si la variable está ordenada) |
| **Relativa acumulada** | $H_i$ | Proporción acumulada hasta $i$ |

> [!warning] Las acumuladas necesitan orden
> Solo se pueden acumular frecuencias si la variable tiene un **orden natural** (ordinal, discreta o continua). Para una variable **nominal** no tiene sentido "acumular": no hay un antes y un después entre las categorías.

---

## 3. Distribuciones y gráficos según el tipo de variable

### 3.1. Variable cualitativa — *Situación 1: quejas de una ferretería*

Empresa de ferretería con envíos en todo el país; se registraron **350 quejas** del primer cuatrimestre. Variable: **motivo principal de la queja** (nominal).

| Motivo | $f_i$ | $h_i$ |
|---|---:|---:|
| Factura no se corresponde con lo pedido | 115 | 0.33 |
| Envases en malas condiciones | 76 | 0.22 |
| Productos con dimensiones incorrectas | 58 | 0.17 |
| Presencia de manchas o poros | 40 | 0.11 |
| Productos con golpes o abolladuras | 25 | 0.07 |
| Envío no coincidente con lo pedido | 21 | 0.06 |
| Pedido llegó con retraso | 15 | 0.04 |
| **Total** | **350** | **1.00** |

Gráficos apropiados para una cualitativa:

- **Gráfico de torta (circular)** → muestra la composición, qué fracción del total representa cada motivo.
- **Gráfico de barras** → compara las frecuencias entre categorías (más fácil de leer que la torta cuando hay muchas categorías).
- **Diagrama de Pareto** → barras **ordenadas de mayor a menor** + una **curva de frecuencia acumulada**.

> [!example] El diagrama de Pareto y la regla 80/20
> El Pareto ordena los motivos por frecuencia y superpone el porcentaje acumulado. Sirve para identificar los **"pocos vitales"**: las categorías que concentran la mayor parte del problema. Aquí, **Factura + Envases + Dimensiones** ya explican cerca del 70 % de las quejas → es donde conviene concentrar los esfuerzos de mejora. Es una de las herramientas clásicas de la gestión de la calidad — junto con el histograma, el diagrama de Ishikawa, la estratificación y algunas otras que se van viendo en el curso, conforman las llamadas **"7 herramientas básicas de la calidad"**. → [[diagrama de Pareto]]
>
> Ojo: "frecuencia" no es la única forma de medir importancia en un Pareto — también se puede ordenar por **costo** o por **tiempo insumido**, y el resultado puede cambiar por completo qué categoría conviene priorizar. Ver el desarrollo de este matiz en [[diagrama de Pareto]].

> [!tip] Evitar el gráfico de torta en la práctica
> Aunque acá se lo menciona como opción, en la práctica profesional se tiende a **evitarlo**: comparar ángulos o áreas es más difícil visualmente que comparar la altura de barras alineadas. Un gráfico de barras casi siempre comunica lo mismo con menos ambigüedad.

### 3.2. Variable cuantitativa discreta — *Situación 2: imperfecciones por pieza*

Muestra aleatoria de $n = 50$ piezas metálicas; se contó el **número de imperfecciones** de cada una (discreta, surge de contar).

| Nº imperf. | $f_i$ | $h_i$ | $F_i$ | $H_i$ |
|---:|---:|---:|---:|---:|
| 0 | 23 | 0.46 | 23 | 0.46 |
| 1 | 17 | 0.34 | 40 | 0.80 |
| 2 | 7 | 0.14 | 47 | 0.94 |
| 3 | 1 | 0.02 | 48 | 0.96 |
| 4 | 2 | 0.04 | 50 | 1.00 |

Gráficos apropiados para una discreta:

- **Diagrama de bastones** → un "palito" en cada valor entero, de altura igual a su frecuencia. **No** se usan barras anchas pegadas: los valores son puntos aislados, no intervalos.
- **Función de distribución acumulada empírica** → gráfico **escalonado** que muestra $H_i$: para cada valor, qué proporción de datos es **menor o igual** a él. Salta en cada valor observado. Desarrollo completo, con ejemplo de por qué es más fácil de leer que dos histogramas superpuestos al comparar grupos, en [[función de distribución acumulada (CDF empírica)]].

### 3.3. Variable cuantitativa continua — *Situación 3: diámetro de piezas*

Muestra de $n = 120$ piezas; se midió el **diámetro en mm** (continua, surge de medir). Como los valores casi no se repiten, se agrupan en **intervalos de clase** (aquí de amplitud 3):

| Intervalo (mm) | $f_i$ | $h_i$ | $F_i$ | $H_i$ |
|---|---:|---:|---:|---:|
| (89, 92] | 8 | 0.07 | 8 | 0.07 |
| (92, 95] | 8 | 0.07 | 16 | 0.14 |
| (95, 98] | 24 | 0.20 | 40 | 0.34 |
| (98, 101] | 21 | 0.17 | 61 | 0.51 |
| (101, 104] | 29 | 0.24 | 90 | 0.75 |
| (104, 107] | 14 | 0.12 | 104 | 0.87 |
| (107, 110] | 12 | 0.10 | 116 | 0.97 |
| (110, 113] | 4 | 0.03 | 120 | 1.00 |

Gráficos apropiados para una continua:

- **Histograma** → barras **pegadas** (sin espacio entre ellas), porque los intervalos son contiguos. La superficie/altura representa la frecuencia de cada intervalo. Es el gráfico rey para ver la **forma** de la distribución.
- **Polígono de frecuencias** → une los puntos medios de las cimas del histograma; ayuda a visualizar la silueta.
- **Ojiva** (polígono de frecuencias acumuladas) → curva creciente de $H_i$; permite leer percentiles gráficamente. Ver [[función de distribución acumulada (CDF empírica)]] para el desarrollo completo.
- **Diagrama de tallo y hoja (*stem-and-leaf*)** → muestra la forma **sin perder los datos originales**. La parte izquierda del "|" es el tallo (dígitos mayores) y la derecha son las hojas (último dígito). Es como un histograma acostado, pero conserva los valores. Ver [[diagrama de tallo y hoja]] para la flexibilidad en cómo elegir tallo/hoja.
- **Diagrama de puntos (dot plot)** → con pocas decenas de datos, cada observación se dibuja como un punto individual sobre una recta numérica, sin agrupar en absoluto — es el caso de los *dotplots* de diámetro y longitud usados más adelante para comparar las Máquinas 1 y 2 (sección 7). Ver [[diagrama de puntos (dot plot)]].

> [!note] Ojo con la notación de intervalos
> `(89, 92]` es **abierto a la izquierda y cerrado a la derecha**: incluye 92 pero no 89. Así cada dato cae en un único intervalo y no hay ambigüedad en los límites. Esta forma de definir los límites se llama **a límites nominales**; existe una alternativa, **a límites reales**, que usa intervalos abiertos con una cifra decimal extra (por ejemplo, `88,5 – 91,5`) para evitar depender de la convención de "abierto/cerrado" — ambas resuelven el mismo problema de ambigüedad, con notación distinta.

> [!tip] ¿Cuántos intervalos usar? Una regla práctica
> No hay una única respuesta correcta, pero una guía habitual es tomar la **raíz cuadrada** del número de datos como cantidad aproximada de intervalos: $k \approx \sqrt{n}$, y la amplitud de cada uno como $(y_{\max}-y_{\min})/k$, redondeada a un número "cómodo" para leer. Con muy pocos intervalos se pierde la forma de la distribución (todo cae en 2 o 3 barras); con demasiados, cada barra tiene tan pocos datos que el gráfico se vuelve ruidoso y deja de mostrar un patrón claro. *Fuente: [[Estadística para la resolución de problemas en Ingeniería]], cap. 2.*

> [!warning] No borres los bins vacíos
> Si un dato mucho más extremo que el resto obliga a usar intervalos de amplitud fija, pueden aparecer **bins sin ningún dato** antes de llegar a ese extremo. Son información real (muestran el salto entre el grueso de los datos y el valor atípico) y no deben eliminarse para que el gráfico se vea más prolijo.

> [!note] En código
> `sns.countplot()` / `sns.barplot()` para cualitativas, `sns.histplot(discrete=True)` para discretas, `sns.histplot()` / `sns.kdeplot()` para continuas — ver [[05 - Distribuciones (histplot, kdeplot, ecdfplot)]] y [[06 - Variables categoricas (boxplot, violinplot, barplot)]] de Seaborn. Todos parten de un DataFrame de Pandas, no de la tabla de frecuencias armada a mano.

---

## 4. ¿Y si los datos están a través del tiempo?

Cuando la variable se registra **a lo largo del tiempo** y **no muestra un comportamiento estable**, **no tiene sentido construir una distribución de frecuencias**: aplastar el tiempo en una tabla borra justamente la información más importante (la evolución, las tendencias, los picos).

> [!example] El diagrama de Nightingale (guerra de Crimea)
> El gráfico de mortalidad del ejército británico que mostró la profe (causas de muerte antes/después de la comisión sanitaria) es un ejemplo clásico: **es una serie de tiempo**, no una distribución de frecuencias. Lo relevante ahí es cómo **cae la mortalidad tras la intervención sanitaria**, algo que solo se ve respetando el eje temporal. (Es el mismo caso de Florence Nightingale que vimos en el Tema 1.) → [[series de tiempo]]

> [!important] El orden de los pasos importa: primero graficar contra el tiempo, después resumir
> No es "si el proceso resulta no ser estable, entonces graficar contra el tiempo" — para saber si es estable **hay que graficarlo contra el tiempo primero**. La regla, tal como la da la bibliografía de la materia: *"si para un conjunto de datos se cuenta con información del orden en el que las unidades fueron seleccionadas o en el que fueron medidas, antes de construir la distribución de frecuencias o realizar cualquier otro análisis con esos datos, es importante evaluar si el comportamiento de la variable es estable, analizando el gráfico de series cronológicas."* Recién si ese gráfico muestra un comportamiento estable tiene sentido seguir con distribución de frecuencias, histograma y medidas de resumen sobre el conjunto completo — si no es estable, hay que describir cada tramo estable por separado, no el conjunto entero. *Fuente: [[Estadística para la resolución de problemas en Ingeniería]], cap. 2.*

> [!tip] Patrones típicos a buscar en una serie de tiempo
> Al graficar contra el tiempo, conviene tener en mente algunas formas típicas que puede tomar el gráfico, porque cada una sugiere una causa distinta: **tendencia creciente o decreciente** sostenida, **comportamiento cíclico** (sube y baja de forma repetitiva), **cambio de nivel** (un salto puntual que se mantiene después), **cambio de variabilidad** (el proceso se vuelve más o menos disperso con el tiempo, aunque el centro no cambie), y **comportamiento estable** (sin ninguno de los patrones anteriores — el caso ideal si se busca un proceso bajo control). Un ejemplo de negocio moderno: las ventas trimestrales de un producto pueden mostrar a la vez una tendencia creciente año a año **y** un patrón estacional (una caída sistemática en el mismo trimestre de cada año) — dos patrones superpuestos en la misma serie. *Fuente: [[Estadística para la resolución de problemas en Ingeniería]], cap. 2.*

---

## 5. La forma de la distribución (el patrón de variabilidad)

Volviendo a estudios **sin tiempo**, la **forma** del histograma (o del tallo y hoja, o del bastones) nos dice mucho:

- **Simétrica / centrada** → los datos se reparten de forma pareja a ambos lados del centro.
- **Asimétrica a la derecha** (sesgo positivo) → la mayoría de los valores son bajos y hay una **cola larga hacia los valores altos**.
- **Asimétrica a la izquierda** (sesgo negativo) → la mayoría de los valores son altos y hay una **cola larga hacia los valores bajos**.

> [!tip] Cómo recordar el sentido de la asimetría
> La asimetría se nombra por **dónde está la cola**, no dónde está el pico. Cola hacia la derecha → asimétrica **a la derecha**. En estas distribuciones, la **media es "arrastrada" hacia la cola**, así que típicamente: asimétrica a la derecha → media > mediana; asimétrica a la izquierda → media < mediana.

También importa el **número de modas** (picos): unimodal (uno), bimodal (dos), etc. Un histograma bimodal suele ser señal de que hay **dos grupos mezclados** (ver estratificación abajo).

> [!note] Un chequeo cuantitativo, no solo visual
> En una distribución razonablemente simétrica, la mediana queda **equidistante** de $q_1$ y $q_3$ ($q_3 - \text{mediana} \approx \text{mediana} - q_1$); cuando esa igualdad se rompe para un lado, es una señal cuantitativa de asimetría. La descripción cualitativa de arriba ("cola a la derecha/izquierda") también se puede resumir en un solo número — ver [[coeficiente de asimetría (skewness)]].

---

## 6. La distribución frente a especificaciones (valores de referencia)

Un histograma cobra más sentido cuando se lo mira **contra lo que se pretende** (los límites de especificación). En el ejemplo de la clase, los **pesos de un producto** (entre 205 y 235, con límites de referencia marcados en el gráfico) se grafican junto a esas líneas para ver si el proceso cumple.

> [!tip] Estratificar para encontrar la causa
> Los "datos globales" pueden ocultar comportamientos distintos. Al **estratificar** (separar) los mismos pesos **por máquina**, aparece que cada máquina tiene su propio centro y dispersión. La estratificación es clave para pasar de "hay variabilidad" a "**esta** es la fuente de la variabilidad". → [[estratificación]]

> [!important] Centrado y variabilidad, juntos, determinan si un proceso cumple
> Cumplir una especificación no depende solo de la dispersión ni solo del centrado: depende de **ambos a la vez**. Un proceso puede estar perfectamente centrado en el valor objetivo pero tener tanta variabilidad que igual se salga de los límites; o tener muy poca variabilidad pero estar descentrado y quedar sistemáticamente corrido hacia un límite. Hay cuatro combinaciones posibles: (1) bien centrado y variabilidad aceptable → cumple; (2) mal centrado, variabilidad aceptable → no cumple, pero se arregla ajustando el centro del proceso; (3) bien centrado, variabilidad excesiva → no cumple, y hace falta reducir la dispersión (una intervención distinta, sobre las fuentes de variabilidad); (4) mal centrado y variabilidad excesiva → no cumple por las dos razones a la vez. Distinguir en cuál de los cuatro casos está un proceso real es lo que decide qué tipo de intervención corresponde.
>
> Una forma descriptiva de cuantificar "variabilidad aceptable": construir los intervalos $\bar y \pm k s$ para $k=1,2,3$ y ver qué proporción de los datos cae dentro de cada uno. En datos razonablemente simétricos y sin atípicos extremos suele encontrarse algo así como 66-70 % dentro de $\bar y \pm s$, 95-96 % dentro de $\bar y \pm 2s$, y prácticamente el 100 % dentro de $\bar y \pm 3s$ — con datos muy asimétricos estos porcentajes cambian, así que conviene verificarlos con los datos reales en vez de asumirlos. Desarrollo completo en [[medidas de dispersión]]. *Fuente: [[Estadística para la resolución de problemas en Ingeniería]], cap. 2.*

---

## 7. ¿En qué difieren dos conjuntos de datos?

Al comparar varios conjuntos (los [[diagrama de puntos (dot plot)|dotplots]] de diámetro y longitud de las Máquinas 1 y 2), conviene mirar **tres dimensiones**:

1. **Centro / posición** → ¿alrededor de qué valor se ubican? (¿una máquina produce piezas sistemáticamente más grandes?)
2. **Dispersión / variabilidad** → ¿qué tan concentrados o esparcidos están? (¿una máquina es más consistente que la otra?)
3. **Forma** → ¿simétrica, asimétrica, con atípicos?

Para cuantificar esto necesitamos **medidas de centrado** y **medidas de variabilidad**. Además del dotplot, la forma habitual de comparar grupos con un [[boxplot]] es dibujar uno **al lado del otro**, uno por grupo — ver [[boxplot]] para el detalle.

---

## 8. Medidas de centrado (posición)

> [!definition] Media (promedio)
> Suma de todos los valores dividida por la cantidad de valores:
> $$\bar{y} = \frac{1}{n}\sum_{i=1}^{n} y_i$$
> Usa **toda** la información, pero es **NO robusta**: un solo valor atípico la puede correr mucho.

> [!definition] Mediana
> Valor que **acumula el 50 %** de las observaciones ordenadas; deja la mitad de los datos por debajo. En la notación de la clase:
> $$\text{Mediana} = x^{*} \ \text{tal que} \ F(x^{*}) = 0{,}50$$
> (donde $F$ es la proporción acumulada). Es **robusta**: no la afectan los valores extremos.

> [!definition] Promedio truncado (*trimmed mean*)
> Se elimina un cierto porcentaje de datos en **cada extremo** de la distribución y se promedian los restantes (p. ej. `trim = 0.1` descarta el 10 % de cada lado). Es un **compromiso**: aprovecha casi todos los datos pero gana robustez frente a atípicos.

> [!definition] Moda
> El valor o categoría **más frecuente**. Es la única medida de centro que también sirve para variables **cualitativas nominales**.
>
> Para una variable **cuantitativa continua sin agrupar**, la moda casi nunca es informativa: al no repetirse casi ningún valor exactamente, "el más frecuente" suele ser un artefacto de la precisión de medición. Ahí conviene agruparla en intervalos (sección 3.3) y hablar de la **clase modal**, o directamente mirar la forma con un histograma.

> [!info] Ver también (no visto en clase) — Media geométrica
> $$\bar{y}_G = \sqrt[n]{y_1 \cdot y_2 \cdots y_n}$$
> Solo se define para valores positivos, y es menos sensible a atípicos que la media aritmética; se usa para promediar índices o tasas de crecimiento relativas, donde importa el efecto multiplicativo acumulado. Desarrollo completo en [[medidas de posición]].

> [!note] ¿Qué medida puedo usar según la escala?
> - **Nominal** → solo **moda**.
> - **Ordinal** → moda y **mediana / percentiles**.
> - **Cuantitativa** → todas (media, mediana, truncado, moda). La **media y el promedio truncado** requieren variable cuantitativa (o ordinal con muchas categorías).
>
> *En código*: `np.mean()`, `np.median()`, `scipy.stats.trim_mean()` — ver [[04 - Agregaciones y estadistica descriptiva]] de NumPy y [[03 - Estadistica descriptiva]] de SciPy, o `df['columna'].mode()` de Pandas para la moda.

> [!info] Ver también (no visto en clase)
> [[medidas de posición]] amplía esta lista con la **media y mediana ponderadas** — la misma idea de centro, pero dándole más peso a algunos datos que a otros.

---

## 9. Percentiles y cuartiles

Con la **misma lógica de la mediana** se definen otros cortes de la distribución ordenada:

- **Cuartiles** → dividen en 4 partes. $q_1$ (primer cuartil) acumula el **25 %**; $q_2$ = mediana = 50 %; $q_3$ (tercer cuartil) acumula el **75 %**.
	$$q_1 = x^{*} \ \text{tal que} \ F(x^{*}) = 0{,}25$$
- **Percentiles** → dividen en 100 partes. $P_{35}$ acumula el **35 %** de los datos ordenados.
	$$P_{35} = x^{*} \ \text{tal que} \ F(x^{*}) = 0{,}35$$

> [!warning] No siempre hay un valor exacto
> Especialmente en **variables discretas**, puede no existir un dato que acumule *exactamente* ese porcentaje. Por eso hay **distintos métodos de interpolación** para estimar percentiles, y software distinto puede dar valores levemente distintos. Los percentiles se pueden calcular para variables de escala **ordinal o superior**.
>
> Uno de esos métodos, a modo de referencia: para el percentil de orden $\alpha$ sobre $n$ datos ordenados, se calcula $E=\alpha \cdot n$; si $E$ tiene parte decimal, el percentil es el dato en la posición $E$ redondeada hacia arriba; si $E$ es entero, se promedian los datos en las posiciones $E$ y $E+1$. Desarrollo completo (con ejemplo numérico paso a paso) en [[medidas de posición]].

> [!note] Divisiones más finas: quintiles y deciles
> La misma lógica de cuartiles/percentiles se aplica con **quintiles** (5 partes) y **deciles** (10 partes) — aparecen seguido al describir distribuciones de ingreso ("el quintil más rico", "el decil más pobre"), donde reportar solo la media tendría poco sentido por la asimetría típica de esos datos.

---

## 10. Medidas de variabilidad (dispersión)

> [!definition] Rango
> $$\text{rango} = x_{\max} - x_{\min}$$
> La máxima diferencia del conjunto. Simple, pero **muy NO robusto**: depende únicamente de los dos valores más extremos.

> [!definition] Rango intercuartílico (RIQ / IQR)
> $$\text{RIQ} = q_3 - q_1$$
> Amplitud del **50 % central** de los datos. **Robusto**: al ignorar el 25 % de cada extremo, no lo afectan los atípicos. Es el compañero natural de la mediana.

Promediar directamente los desvíos $y_i - \bar{y}$ no sirve como medida de dispersión: por construcción de la media, los desvíos positivos y negativos se cancelan y esa suma da siempre cero, sin importar cuánto varíen los datos. Elevar cada desvío al **cuadrado** antes de sumarlo resuelve el problema (el resultado ya no se cancela, y además penaliza más los desvíos grandes) — a costa de dejar el resultado en unidades al cuadrado, algo que después corrige la raíz cuadrada. (Desarrollo completo de este razonamiento en [[medidas de dispersión]].)

> [!definition] Varianza y desvío estándar
> La **varianza** es (casi) el promedio de los **desvíos al cuadrado** respecto de la media:
> $$s^{2} = \frac{\sum_{i=1}^{n}(y_i - \bar{y})^{2}}{n-1}$$
> El **desvío (o desviación) estándar** es su raíz, y tiene las **mismas unidades que la variable** (deshace el efecto de haber elevado al cuadrado):
> $$s = \sqrt{s^{2}}$$
> Se interpreta como un "promedio" de cuánto se aparta cada dato de la media. Es **NO robusto** (se calcula a partir de la media y de cuadrados, que amplifican los extremos).

> [!info] ¿Por qué se divide por $n-1$ y no por $n$?
> Cuando los datos son una **muestra** y se usa $\bar{y}$ (estimada de los propios datos) para estimar la variabilidad de la **población**, dividir por $n$ subestima. Dividir por $n-1$ (los **grados de libertad**) corrige ese sesgo. En una **población** completa, en cambio, se divide por $N$ y se usa la letra griega $\sigma^2$ (varianza poblacional) y $\sigma$ (desvío poblacional). → [[grados de libertad]]

> [!definition] Coeficiente de variación (CV)
> Es una medida de dispersión **relativa** y **adimensional**:
> $$CV = \frac{s}{\bar{y}} \times 100\ \%$$
> Sirve para **comparar la variabilidad de variables con distintas unidades o escalas** (p. ej. ¿varía más el diámetro o el peso?). Regla útil: un mismo $s$ "pesa" distinto según el tamaño de la media.

**Tabla resumen — robustez frente a valores atípicos:**

| Medida | Tipo | ¿Robusta? | Va de la mano con |
|---|---|:---:|---|
| Media | Centro | ❌ | Desvío estándar |
| Mediana | Centro | ✅ | RIQ |
| Promedio truncado | Centro | ✅ (parcial) | — |
| Rango | Dispersión | ❌ | — |
| RIQ | Dispersión | ✅ | Mediana |
| Varianza / Desvío estándar | Dispersión | ❌ | Media |

> [!tip] Combiná centro + dispersión coherentes
> Si describís con la **media**, acompañala con el **desvío estándar**. Si usás la **mediana** (porque hay atípicos o asimetría), acompañala con el **RIQ**. Mezclar media con RIQ o mediana con desvío es menos coherente.

> [!example] Todas las medidas juntas, sobre el diámetro de la clase
> ```python
> import numpy as np
> from scipy import stats
>
> np.std(Datos["Diametro"], ddof=1)   # 5.205162 -> desvío estándar muestral (ddof=1, ver n-1 arriba)
> CV = np.std(Datos["Diametro"], ddof=1) * 100 / np.mean(Datos["Diametro"])
> print(CV)                            # 5.169545
> stats.iqr(Datos["Diametro"])        # 7.442181
> Datos["Diametro"].min(), Datos["Diametro"].max()   # (89.22963, 112.90296)
> ```
> Un CV de ~5,2 % es bajo: el diámetro varía poco en relación a su propia media (~100,7 mm) — el proceso es bastante estable. (La clase lo calculó en R; acá está el mismo cálculo, mismos números, en Python.)

> [!info] Ver también (no visto en clase)
> [[medidas de dispersión]] agrega el **MAD** (desviación absoluta mediana): un robusto de dispersión todavía más resistente a atípicos que el RIQ.

---

## 11. Qué pasa con los atípicos (el ejemplo en Python)

La clase mostró un ejemplo muy claro de robustez, calculado en R. Así se reproduce en Python, partiendo de un vector "sano":

```python
import numpy as np
from scipy import stats

x = [2, 4, 3, 6, 3, 7, 5, 8, 7, 4]
np.mean(x)               # 4.9
stats.trim_mean(x, 0.1)  # 4.875
np.median(x)             # 4.5
```

Ahora se reemplaza el 8 por un valor cada vez más extremo:

| Dato extremo | Media | Media truncada (0.1) | Mediana |
|---|---:|---:|---:|
| … 8 … (original) | 4.9 | 4.875 | 4.5 |
| … **18** … | 5.9 | 4.875 | 4.5 |
| … **80** … | **12.1** | 4.875 | 4.5 |

> [!important] La lección
> Un **único** valor atípico dispara la **media** (de 4.9 a 12.1), mientras que la **mediana** y la **media truncada** ni se inmutan. Por eso, ante distribuciones **asimétricas o con atípicos**, la mediana suele describir mejor "el valor típico".

> [!note] En código
> `np.mean`/`np.median` son de NumPy; `stats.trim_mean` es de [[03 - Estadistica descriptiva|SciPy]] — no existe un equivalente en NumPy puro. Ver también [[robustez estadística]].

---

## 12. Diagrama de caja y bigotes (*boxplot*)

Resume la distribución con **cinco números** (el *five-number summary*, que en Python se obtiene con `pandas.Series.describe()`): mínimo, $q_1$, mediana, $q_3$, máximo.

**Anatomía de la caja** (ejemplo del diámetro, `describe()`: Min 89.23 · Q1 96.58 · Mediana 100.73 · Media 100.69 · Q3 104.03 · Max 112.90):

![[Anatomia del boxplot.png]]

- La **caja** va de $q_1$ a $q_3$ → contiene el **50 % central**; su largo **es el RIQ**.
- La **línea interna** es la **mediana**.
- Los **bigotes** se extienden hasta el dato más lejano que **no** sea atípico.

### Detección de atípicos con el boxplot

> [!important] Criterio del 1.5 · RIQ
> Se considera **valor atípico** cualquier dato que caiga a **más de 1.5 RIQ** por fuera de los cuartiles, es decir, fuera de las "vallas":
> $$[\,q_1 - 1{,}5 \cdot \text{RIQ}\ ,\ \ q_3 + 1{,}5 \cdot \text{RIQ}\,]$$
> Los bigotes llegan hasta el último dato **dentro** de esas vallas; los que quedan afuera se dibujan como **puntos individuales**.

> [!example] En el ejemplo de las imperfecciones
> `describe()`: Min 0 · Q1 0 · Mediana 1 · Media 0.84 · Q3 1 · Max 4; con [[03 - Estadistica descriptiva|`scipy.stats.iqr(x)`]] `= 1`. Como $q_3 + 1{,}5\cdot\text{RIQ} = 1 + 1{,}5 = 2{,}5$, las piezas con **3 y 4** imperfecciones aparecen como **atípicos** (los puntos por encima del bigote). El boxplot lo confirma visualmente. El comparar boxplot, tallo y hoja y diagrama de bastones del mismo conjunto muestra cómo cada gráfico ilumina algo distinto.

> [!tip] El uso más frecuente: varios boxplots uno al lado del otro
> Un solo boxplot ya sirve, pero donde más rinde es dibujando **uno por grupo** sobre el mismo eje — exactamente lo que hace falta para la pregunta de la sección 7 (¿en qué difieren la Máquina 1 y la Máquina 2?). Desarrollo completo, más la mención de un gráfico emparentado que muestra más detalle (el violin plot), en [[boxplot]].

---

## Mapa mental del tema

![[Mapa mental variabilidad.png]]

---

## Conceptos para desarrollar en notas aparte
- [[distribución de frecuencias]]
- [[histograma]] · [[diagrama de tallo y hoja]] · [[boxplot]] · [[diagrama de puntos (dot plot)]]
- [[función de distribución acumulada (CDF empírica)]] · [[coeficiente de asimetría (skewness)]]
- [[diagrama de Pareto]] · [[diagrama de Ishikawa]]
- [[medidas de posición]] · [[medidas de dispersión]]
- [[robustez estadística]] · [[valores atípicos]]
- [[coeficiente de variación]]
- [[causas comunes y causas especiales]]

## Preguntas de repaso
1. ¿Por qué no tiene sentido construir una distribución de frecuencias para datos que vienen a través del tiempo y no son estables?
2. Un histograma es asimétrico a la derecha (cola larga hacia valores altos) — ¿la media es mayor o menor que la mediana? ¿Por qué?
3. ¿Por qué se divide por $n-1$ y no por $n$ al calcular la varianza muestral?
4. En el ejemplo de las imperfecciones por pieza (Q1 = 0, Q3 = 1, RIQ = 1), ¿a partir de cuántas imperfecciones un dato se considera atípico según el criterio del boxplot?
5. Si una distribución tiene atípicos, ¿por qué conviene describirla con mediana + RIQ en vez de media + desvío estándar?
6. Un proceso puede estar perfectamente centrado en el valor objetivo y aun así no cumplir con la especificación — ¿cómo es posible? ¿Qué otra cosa hay que revisar además del centrado?
7. ¿Qué diferencia hay entre agrupar datos en un histograma y agrupar percentiles? ¿Por qué un histograma y una tabla de percentiles no "cortan" los datos de la misma forma?

## Actividad
La cátedra complementó esta clase con cuatro casos aplicados de ingeniería y gestión (viscosidad de un proceso, comparación de laboratorios, tiempo de resolución de reclamos, elección de un lote de producción) — resueltos en detalle, con datos reales y traducidos a Python, en [[02.1 - Casos aplicados]].

## Preguntas que me quedaron
-
-

## Para la próxima clase
-
