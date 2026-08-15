---
titulo: "Clase 3 — Estructuras no lineales y complejidad algorítmica"
materia: Algoritmos
tipo: apunte
clase: 3
fecha: 2026-08-15
tags:
  - algoritmos
  - maestria
  - python
  - estructuras-no-lineales
  - tema/estructuras-no-lineales
---

# Algoritmos · Clase 3 — Estructuras no lineales y complejidad algorítmica

> [!abstract] Idea central de la clase
> Esta clase cierra dos cosas que quedaron abiertas. La primera: la clase 1 vio estructuras **lineales** —listas, tuplas, diccionarios, conjuntos—, pero muchísima información real no es lineal: se ramifica (una taxonomía) o se conecta (una red social). Para eso existen los **árboles** y los **grafos**, y para recorrerlos hace falta la recursión de la clase 2. La segunda: veníamos **midiendo** diferencias de rendimiento enormes con un cronómetro (buscar en un conjunto miles de veces más rápido que en una lista; Fibonacci recursivo con casi 2,7 millones de llamadas). Hoy se aprende a **predecirlas sin medir**, con la notación **Big O**.
>
> Dos ideas para llevarse:
> 1. **La misma recursión de la clase 2, aplicada a una estructura que se ramifica en vez de una que se reduce de a uno.** Un árbol es, literalmente, una definición recursiva: cada hijo es la raíz de un árbol más chico.
> 2. **La complejidad no es una curiosidad teórica: es lo que separa un análisis que corre en un café de uno que nunca termina.** Pasar de O(n²) a O(n log n) da más ganancia que comprar una máquina mil veces más rápida.

> [!note] Convención de esta nota
> Los callouts **"Puente con Estadística"**, cualquier tramo marcado como **"ampliación"**, y las notas al pie de gráfico que dicen "verificado en este entorno" son agregados míos — no los dio el profesor. El resto sigue de cerca la clase (notebook `Clase3_Estructuras_no_lineales_y_complejidad.ipynb` y `Actividad_Clase3.ipynb`).

---

## 1. Árboles

Un **árbol** es una estructura donde cada nodo puede tener varios **hijos**, y cada nodo tiene exactamente un **padre** — salvo la **raíz**, que no tiene ninguno. Un nodo sin hijos es una **hoja**. Se representa sin necesitar nada nuevo: un diccionario con un valor y una lista de hijos, cada uno de los cuales es a su vez un árbol completo:

```python
arbol = {
    "nombre": "Vertebrados",
    "hijos": [
        {"nombre": "Aves", "hijos": [
            {"nombre": "Pingüino", "hijos": []},
            {"nombre": "Águila",   "hijos": []},
        ]},
        {"nombre": "Mamíferos", "hijos": [
            {"nombre": "Ballena", "hijos": []},
            {"nombre": "Perro",   "hijos": []},
        ]},
    ],
}
```

Esa autosemejanza —`arbol["hijos"][0]` es un árbol completo, con la misma forma que el original— es la propiedad que hace que la recursión funcione tan bien: recorrer todo el árbol es "hacer algo con el nodo actual, y hacer lo mismo con cada hijo". El caso base aparece solo: si un nodo no tiene hijos, el bucle no se ejecuta ninguna vez y la recursión frena.

```python
def contar_nodos(nodo):
    total = 1                            # me cuento a mí mismo
    for hijo in nodo["hijos"]:
        total += contar_nodos(hijo)      # más lo que traiga cada subárbol
    return total

def altura(nodo):
    if not nodo["hijos"]:
        return 1
    return 1 + max(altura(h) for h in nodo["hijos"])
```

Tres líneas para recorrer una estructura de profundidad arbitraria — escribir lo mismo con bucles anidados exigiría saber de antemano cuántos niveles tiene el árbol, y no se sabe.

> [!tip] Si la recursión ramificada todavía no se siente natural
> A diferencia de `factorial` (una sola llamada recursiva por nivel), `contar_nodos` hace **una llamada por cada hijo** y las va acumulando en `total` a medida que cada una termina. Traza completa, línea por línea, sobre un árbol chico de 4 nodos, en [[árboles]].

### El árbol de decisión

Acá está la conexión directa con minería de datos: un **árbol de decisión** —uno de los modelos de clasificación más usados— es literalmente un árbol. Cada nodo interno hace una **pregunta** sobre una variable, cada rama es una **respuesta**, cada hoja es una **predicción**. Construido a mano sobre el dataset de pingüinos (`aleta_mm > 206 → Gentoo`; si no, `pico_mm > 45 → Chinstrap`, si no, `Adelie`):

![[Arbol de decision - pinguinos.png]]

```python
def predecir(nodo, pinguino):
    if "prediccion" in nodo:                    # CASO BASE: llegué a una hoja
        return nodo["prediccion"]
    if nodo["pregunta"] == "aleta_mm > 206":
        rama = "si" if pinguino["aleta_mm"] > 206 else "no"
    else:
        rama = "si" if pinguino["pico_mm"] > 45 else "no"
    return predecir(nodo[rama], pinguino)       # CASO RECURSIVO: bajo un nivel
```

**95,0 % de exactitud con dos preguntas escritas a mano**, sobre las 342 mediciones completas (cifra recalculada de forma independiente contra el dataset real, coincide con el notebook de clase). La estructura de datos, el recorrido y la predicción son exactamente lo mismo que la clase ya construyó a mano — la diferencia con un algoritmo real de árboles de decisión es solo que ese algoritmo prueba **todos** los cortes posibles en vez de que una persona los elija mirando una tabla.

> [!tip] `predecir` es más simple de lo que parece: un solo camino, no una ramificación
> A diferencia de `contar_nodos`, acá cada nivel sigue **una sola** rama (`si` o `no`) y se limita a reenviar hacia arriba, sin tocarla, la respuesta que le llega de abajo. Traza completa con un pingüino concreto en [[árboles]].

> [!tip] Ampliación — vocabulario y recorridos que no vimos en clase
> El árbol de la clase se recorre siempre "nodo primero, después los hijos" (recorrido **preorder**). Existen otras formas —**postorder** (procesar el nodo después de sus hijos, necesario cuando el resultado de un nodo depende de sus hijos, como evaluar una expresión aritmética) y **level-order** (por niveles, con una cola en vez de recursión, el mismo principio que el BFS de la sección 2)— y vocabulario adicional (nivel/profundidad, ancestro/descendiente, grado, árbol binario) que amplían esto en [[árboles]].

---

## 2. Grafos

Un **grafo** generaliza el árbol: un conjunto de **nodos** conectados por **aristas**, sin las restricciones del árbol — puede haber ciclos, un nodo puede tener varios "padres", puede haber partes desconectadas. Un árbol es, formalmente, un caso particular de grafo: uno conexo y sin ciclos.

La forma más práctica de representarlo es un diccionario donde cada clave es un nodo y su valor es la lista de vecinos (**lista de adyacencia**):

![[Grafo de rutas aereas.png]]

```python
rutas = {
    "Rosario":      ["Buenos Aires", "Córdoba"],
    "Buenos Aires": ["Rosario", "Córdoba", "Mendoza", "Bariloche"],
    "Córdoba":      ["Rosario", "Buenos Aires", "Mendoza", "Salta"],
    "Mendoza":      ["Buenos Aires", "Córdoba", "Bariloche"],
    "Salta":        ["Córdoba"],
    "Bariloche":    ["Buenos Aires", "Mendoza"],
    "Ushuaia":      [],                     # nodo aislado
}
```

Recorrer un grafo tiene una complicación que el árbol no tenía: los **ciclos** (Rosario conecta con Córdoba, Córdoba con Rosario — recorrer ingenuamente va y viene para siempre). La solución es llevar registro de los nodos ya **visitados** con un `set`, porque preguntar "¿ya estuve acá?" tiene que ser instantáneo.

**DFS** (*depth-first search*) se mete todo lo que puede por un camino antes de retroceder — es recursivo, y se parece al recorrido del árbol:

```python
def dfs(grafo, nodo, visitados=None):
    if visitados is None:
        visitados = set()
    if nodo in visitados:
        return visitados
    visitados.add(nodo)
    for vecino in grafo[nodo]:
        dfs(grafo, vecino, visitados)
    return visitados
```

> [!tip] La recursión más difícil de la clase, trazada línea por línea
> `dfs` combina dos cosas nuevas a la vez: un caso base que **cambia mientras la recursión corre** (`visitados` se va llenando) y un **retroceso explícito** cuando un camino se agota. Traza completa —incluyendo exactamente en qué momento cada llamada "retrocede" a la anterior— corriendo sobre este mismo grafo de rutas, en [[grafos y recorridos (DFS, BFS)]].

**BFS** (*breadth-first search*) recorre por niveles, con una **cola** (`collections.deque`) en vez de recursión. Su propiedad valiosa: el primer camino que encuentra a un nodo es el más corto en cantidad de saltos.

```python
from collections import deque

def camino_mas_corto(grafo, origen, destino):
    if origen == destino:
        return [origen]
    visitados = {origen}
    cola = deque([[origen]])
    while cola:
        camino = cola.popleft()
        for vecino in grafo[camino[-1]]:
            if vecino in visitados:
                continue
            nuevo = camino + [vecino]
            if vecino == destino:
                return nuevo
            visitados.add(vecino)
            cola.append(nuevo)
    return None
```

> [!tip] DFS o BFS, ¿cuál uso?
> **DFS**: para explorar todo, detectar ciclos, encontrar componentes conexas. **BFS**: cuando importa la distancia — camino más corto en saltos, "amigos de amigos", grados de separación. Los dos visitan cada nodo y cada arista una sola vez; cambia el orden, no el costo.

> [!tip] Ampliación — por qué ambos cuestan lo mismo, y el mismo ejemplo en la bibliografía
> El costo de ambos es $O(V+E)$: se marca cada nodo una vez y, para cada uno, se recorre su lista de vecinos completa — sumadas todas, dan $2E$. Y el ejemplo de la clase (rutas aéreas, BFS para menos escalas) no es una elección arbitraria: es prácticamente el ejemplo canónico de la bibliografía, bajo el nombre "Degrees of Separation" — el mismo patrón detrás del número de Erdős en matemática y el "juego de Kevin Bacon". Desarrollo completo en [[grafos y recorridos (DFS, BFS)]].

Un grafo construido desde datos, no a mano: dos islas quedan conectadas si comparten alguna especie de pingüino, usando la **intersección de conjuntos** (`&`) de la clase 1:

```python
comunes = especies_por_isla[isla_a] & especies_por_isla[isla_b]
if comunes:
    grafo_islas[isla_a].append(isla_b)
    grafo_islas[isla_b].append(isla_a)
```

Este patrón —construir un grafo de similitud a partir de datos tabulares— es la base de los sistemas de recomendación y de la detección de comunidades.

---

## 3. Notación Big O

Medir con cronómetro tiene tres problemas: depende de la máquina, del momento, y del tamaño de la prueba usada. Lo que hace falta no es cuánto tarda **hoy**, sino **cómo crece el tiempo cuando crecen los datos** — eso es lo que captura la notación Big O, contando **operaciones elementales** en función del tamaño de la entrada $n$.

**Reglas prácticas** para calcular la complejidad de un código: descartar las constantes (`O(3n)` es `O(n)`); quedarse con el término dominante (`O(n² + n)` es `O(n²)`); los bucles secuenciales se **suman**; los bucles anidados se **multiplican**; se analiza el **peor caso**, salvo que se aclare lo contrario.

| Notación | Nombre | Ejemplo típico | ¿n=1.000 escala a n=1.000.000? |
|---|---|---|---|
| **O(1)** | Constante | Acceder a `lista[5]`, buscar en un `set` | Igual de rápido |
| **O(log n)** | Logarítmica | Búsqueda binaria | Apenas el doble de trabajo |
| **O(n)** | Lineal | Recorrer una lista | Mil veces más |
| **O(n log n)** | Lineal-logarítmica | Los buenos ordenamientos | Unas 2.000 veces más |
| **O(n²)** | Cuadrática | Bucles anidados | Un millón de veces más |
| **O(2ⁿ)** | Exponencial | Fibonacci recursivo, fuerza bruta | Impracticable |

Con un millón de datos: un algoritmo **O(n)** termina en 1 milisegundo; **O(n log n)**, en 20 milisegundos (prácticamente lo mismo); **O(n²)**, casi 17 minutos (un millón de veces más que el lineal); **O(2ⁿ)** ya era impracticable con n=100 (del orden de tres mil veces la edad del universo). Con n=10, en cambio, **todas** las familias terminan en microsegundos — indistinguibles a ojo. Ese es el problema práctico de fondo: con un dataset de juguete, un algoritmo desastroso se ve idéntico a uno excelente. La diferencia aparece recién con datos de verdad, que suele ser cuando ya es tarde.

> Un dato que ordena las prioridades: pasar de O(n²) a O(n log n) da más ganancia que comprar una máquina mil veces más rápida.

Analizando código de clases anteriores con este vocabulario nuevo: buscar en una **lista** es `O(n)` (peor caso: recorrer los n elementos); buscar en un **conjunto** es `O(1)` (el hashing va directo). Con un millón de elementos, la lista hace en promedio 500.000 comparaciones contra 1 del conjunto — de ahí la diferencia de miles de veces ya medida en la clase 1. Ya no es una observación empírica: es una predicción.

```python
def hay_duplicados_lento(lista):     # O(n²): compara todos contra todos
    for i in range(len(lista)):
        for j in range(i + 1, len(lista)):
            if lista[i] == lista[j]:
                return True
    return False

def hay_duplicados_rapido(lista):    # O(n): mismo resultado, con un conjunto
    vistos = set()
    for x in lista:
        if x in vistos:
            return True
        vistos.add(x)
    return False
```

Las dos funciones hacen exactamente lo mismo. La segunda es `O(n)` en vez de `O(n²)` simplemente porque usa la estructura de datos adecuada — la misma idea de la clase 1 ("elegir la estructura de datos es una decisión algorítmica"), ahora con vocabulario preciso.

**Complejidad espacial**: Big O también mide memoria. La memoización de la clase 2 es el ejemplo perfecto: Fibonacci recursivo usa `O(n)` de memoria (la pila) y `O(2ⁿ)` de tiempo; el memoizado usa `O(n)` de memoria (el diccionario) y `O(n)` de tiempo. Se paga un diccionario y se gana una eternidad — el mismo intercambio (*space-time tradeoff*) que aparece en los índices de una base de datos o la caché de un navegador.

> [!tip] Ampliación — la fórmula exacta detrás de "duplicá n y mirá qué pasa", y una familia que faltaba
> La tabla de arriba no incluye la familia **cúbica** $O(n^3)$ (tres bucles anidados), que sí aparece en la bibliografía estándar. Y la regla informal de verificación empírica de la clase (sección 4) tiene una versión formal con fórmula exacta —el *doubling ratio* de Sedgewick, $b = \log_2(T(2n)/T(n))$— que da el exponente preciso en vez de reconocerlo a ojo, más el resultado teórico de por qué $O(n \log n)$ es el límite exacto (no solo "bueno") del ordenamiento por comparación. Desarrollo completo en [[notación Big O y familias de complejidad]] — nota que también generaliza [[complejidad O(1) vs O(n)]], escrita en la clase 1 sobre el caso puntual lista-vs-conjunto.

---

## 4. Verificación empírica

La teoría dice que buscar en una lista es `O(n)` y en un conjunto `O(1)`. Comprobado con tamaños crecientes, midiendo el tiempo mediano de 7 repeticiones (para no dejarse engañar por un pico aislado del sistema):

![[Busqueda lista vs conjunto.png]]

| n | lista (µs) | conjunto (µs) | razón |
|---|---|---|---|
| 1.000 | 2,5 | 0,08 | 30× |
| 10.000 | 24,3 | 0,04 | 574× |
| 100.000 | 253,3 | 0,04 | 6.044× |

Al duplicarse `n`, el tiempo de la lista se duplica también (recta en el panel izquierdo) — eso es exactamente `O(n)`. El del conjunto no cambia, aunque `n` crezca cien veces: línea horizontal en el panel derecho (escala log, para poder verla) — eso es `O(1)`.

Ahora las dos versiones de "buscar duplicados": la teoría dice `O(n)` contra `O(n²)`.

![[Duplicados On2 vs On.png]]

| n | O(n²) (ms) | O(n) (ms) | razón vs. anterior |
|---|---|---|---|
| 200 | 0,21 | 0,003 | — |
| 800 | 5,09 | 0,011 | ~4,4× |
| 3.200 | 78,85 | 0,052 | ~4,1× |

Al duplicarse `n`, el tiempo de la versión cuadrática se **cuadruplica** ($2^2=4$) — la firma inconfundible de `O(n²)`. Y la ventaja de la versión con conjunto no es constante, **crece con $n$**: con 200 elementos la diferencia es modesta, con 3.200 ya es de tres órdenes de magnitud. Por eso los algoritmos malos no se detectan en pruebas chicas: se detectan en producción.

> [!tip] Cómo reconocer la complejidad midiendo
> Duplicá `n` y mirá qué le pasa al tiempo. Si no cambia, es `O(1)`. Si se duplica, `O(n)`. Si se cuadruplica, `O(n²)`. Si apenas sube, `O(log n)`.

---

## 5. Cierre

### Lo que vimos hoy

**Estructuras no lineales**
- **Árboles**: nodos, raíz, hojas, altura. Representación con diccionarios anidados y recorrido recursivo. Un árbol de decisión hecho a mano que clasifica pingüinos con 95 % de exactitud usando dos preguntas.
- **Grafos**: lista de adyacencia, el problema de los ciclos y el conjunto de visitados, DFS (recursivo) y BFS (con cola, camino más corto). Construcción de un grafo desde datos tabulares.

**Complejidad algorítmica**
- Por qué medir con reloj no alcanza, y qué captura Big O.
- Las familias — O(1), O(log n), O(n), O(n log n), O(n²), O(2ⁿ) — y qué significan con datos reales.
- Análisis de código ya escrito, y verificación empírica de que las curvas medidas coinciden con la teoría.
- Complejidad espacial y el intercambio memoria-tiempo.

### Tres ideas para llevarse

1. **La complejidad importa más que el hardware.** Pasar de `O(n²)` a `O(n log n)` da más ganancia que una máquina mil veces más rápida.
2. **Los algoritmos malos no se detectan con datos chicos.** Con n=200 la diferencia era modesta; con n=3.200, enorme. Siempre probar con volúmenes realistas.
3. **Mismo resultado, distinto costo.** Las dos funciones de duplicados devuelven lo mismo; una es viable y la otra no. La diferencia fue elegir bien la estructura de datos.

---

## Conceptos para desarrollar en notas aparte
- [[árboles]]
- [[grafos y recorridos (DFS, BFS)]]
- [[notación Big O y familias de complejidad]]
- [[complejidad O(1) vs O(n)]]

## Preguntas de repaso
1. ¿Por qué la propiedad "cada hijo de un nodo es, a su vez, la raíz de un árbol" es lo que hace que la recursión sea la herramienta natural para recorrer árboles, y qué hace de caso base en un recorrido de árbol sin necesidad de escribirlo explícitamente?
2. Un grafo no dirigido puede tener ciclos y un árbol no. ¿Por qué eso obliga a llevar un conjunto de nodos "visitados" al recorrer un grafo, y qué pasaría si no se llevara ese registro?
3. ¿Cuál es la diferencia estructural entre DFS y BFS (qué estructura de datos usa cada uno para decidir el orden de exploración), y por qué esa diferencia hace que BFS garantice encontrar el camino más corto en cantidad de saltos y DFS no?
4. Si un algoritmo hace `5n² + 200n + 1000` operaciones, ¿cuál es su notación Big O y por qué se puede ignorar tanto la constante `5` como el término `200n`?
5. Dos funciones resuelven el mismo problema ("¿hay duplicados en esta lista?"), una recorriendo todos los pares y otra usando un conjunto. Explicá por qué tienen complejidades distintas (`O(n²)` contra `O(n)`) a pesar de devolver siempre el mismo resultado, y qué le pasa a la diferencia de tiempos entre ambas a medida que crece `n`.

## Preguntas que me quedaron
-
-

## Para la próxima clase
**Clase 4 — Algoritmos de búsqueda y ordenamiento.** Aplica todo lo de hoy a los algoritmos clásicos: búsqueda lineal contra binaria, y los tres ordenamientos elementales —burbuja, selección e inserción—. Se implementan, se analiza su complejidad, y se mide si se comportan como predice el análisis.

## Actividad
Está en **`Actividad_Clase3.ipynb`** (Moodle): recorrer un árbol de taxonomía de minería de datos, construir y analizar un grafo de similitud entre especies de pingüinos con DFS/BFS/componentes conexas, y determinar experimentalmente la complejidad de una función desconocida. Se entrega antes del viernes 21 de agosto.
