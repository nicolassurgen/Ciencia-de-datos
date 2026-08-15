---
titulo: "Grafos y recorridos (DFS, BFS)"
materia: Algoritmos
tipo: concepto
tags:
  - algoritmos
  - maestria
  - concepto
  - python
  - tema/estructuras-no-lineales
fecha: 2026-08-15
---

# Grafos y recorridos (DFS, BFS)

## El problema, sin código todavía

Un árbol alcanza mientras la relación entre los datos sea estrictamente jerárquica: un padre, muchos hijos, sin vueltas atrás. Pero la mayoría de las relaciones del mundo real no son así. En una red de amistades, A puede ser amigo de B y B de A al mismo tiempo — no hay "padre" ni "hijo", hay una conexión simétrica. Y las conexiones pueden formar **ciclos**: A conoce a B, B conoce a C, C conoce a A. Un árbol, por definición, no permite eso. Hace falta una estructura más general.

> [!definition] Grafo
> Un conjunto de **vértices** (o nodos) y una colección de **aristas**, donde cada arista conecta un par de vértices. *"Un grafo es un conjunto de vértices y una colección de aristas, donde cada arista conecta un par de vértices."* *Fuente: [[Algorithms-4th-Edition-By-Robert Sedgewick and Kevin Wayne]], cap. 4.1.*

Un árbol es, formalmente, un caso particular de grafo: uno **conexo** (se puede llegar de cualquier vértice a cualquier otro) y **sin ciclos**. Todo lo que ya sabés de árboles sigue valiendo — nodos, aristas, recorrido recursivo — pero un grafo general no impone esas dos restricciones, y esa libertad es justamente lo que obliga a repensar cómo se recorre.

## Vocabulario

- **Grado de un vértice**: la cantidad de aristas que llegan a él. `avgDegree = 2·E / V` (cada arista suma 1 al grado de sus dos extremos, así que la suma de todos los grados es siempre el doble de la cantidad de aristas). *Fuente: [[Algorithms-4th-Edition-By-Robert Sedgewick and Kevin Wayne]], cap. 4.1.*
- **Camino**: una secuencia de vértices conectados por aristas. **Ciclo**: un camino que vuelve a su punto de partida.
- **Conexo**: hay un camino entre cualquier par de vértices. Si no lo es, el grafo se separa en **componentes conexas** — subgrafos conexos maximales.
- **Grafo disperso vs. denso**: disperso si tiene relativamente pocas aristas respecto de la cantidad de vértices posibles (como una red de rutas aéreas: la mayoría de los pares de ciudades no tiene vuelo directo); denso en el caso contrario.

## Representar un grafo: por qué diccionario y no matriz

La clase ya usa un diccionario de nodo → lista de vecinos (**lista de adyacencia**). No es la única forma de representarlo — la alternativa es una **matriz de adyacencia**, una grilla de $V \times V$ con un 1 donde hay arista y 0 donde no.

> [!important] La elección no es arbitraria: depende de cuántas aristas hay
> Una matriz de adyacencia ocupa $O(V^2)$ de espacio **siempre**, tenga el grafo pocas o muchas aristas — para un millón de ciudades, una matriz de un millón por un millón es intratable, aunque casi todos sus valores sean 0. La lista de adyacencia ocupa $O(V + E)$: solo lo que realmente existe. A cambio, preguntar "¿existen una arista entre A y B?" es instantáneo en la matriz ($O(1)$) pero cuesta recorrer la lista de vecinos en la lista de adyacencia. Para un grafo **disperso** como el de rutas aéreas de la clase (cada ciudad conecta con pocas otras, no con todas), la lista de adyacencia es la elección correcta — que es exactamente la que ya usa el código. *Fuente: [[Algorithms-4th-Edition-By-Robert Sedgewick and Kevin Wayne]], cap. 4.1.*

![[Grafo de rutas aereas.png]]

Sobre este grafo, Ushuaia queda aislada (grado 0) y Buenos Aires/Córdoba son los vértices de mayor grado (4 conexiones cada uno) — los "hubs" que la clase identificó ordenando por cantidad de vecinos.

## DFS y BFS: dos formas de explorar

> [!tip] Metáfora de Sedgewick
> *"DFS es análogo a una sola persona explorando un laberinto [...], tomando los vértices más cercanos solo cuando se encuentra con un callejón sin salida. BFS es análogo a un grupo de exploradores que se abren en abanico en todas las direcciones [...]. Los caminos de DFS tienden a ser largos y sinuosos; los caminos de BFS son cortos y directos."* *Fuente: [[Algorithms-4th-Edition-By-Robert Sedgewick and Kevin Wayne]], cap. 4.1.*

Un explorador solo (DFS) se mete por un pasillo hasta el fondo antes de volver a probar otro. Un grupo que se abre en abanico (BFS) cubre primero todo lo cercano antes de alejarse. Ninguno es "mejor" en general — resuelven preguntas distintas, y por eso la clase usa una estructura de datos distinta para cada uno: **pila** (implícita, vía recursión) para DFS, **cola** (`collections.deque`) para BFS. La diferencia de comportamiento sale exclusivamente de esa elección: es el mismo recorrido "quitar un elemento pendiente y agregar sus vecinos", cambiando solo si el elemento que se retira es el más nuevo (pila → profundidad) o el más viejo (cola → anchura).

### Paso a paso: la recursión de DFS, incluido el "retroceder"

Esta es la recursión más difícil de las que aparecen en la clase, porque combina dos cosas nuevas a la vez: un **caso base distinto** al de árboles ("ya visité este nodo" en vez de "no tengo hijos") y un **retroceso explícito** cuando un camino se termina y hay que volver a probar otra rama. Vale la pena trazarla completa, con el código y el grafo reales de la clase:

```python
def dfs(grafo, nodo, visitados=None):
    if visitados is None:
        visitados = set()
    if nodo in visitados:        # CASO BASE: ya pasé por acá, corto
        return visitados
    visitados.add(nodo)
    for vecino in grafo[nodo]:
        dfs(grafo, vecino, visitados)
    return visitados
```

```python
rutas = {
    "Rosario":      ["Buenos Aires", "Córdoba"],
    "Buenos Aires": ["Rosario", "Córdoba", "Mendoza", "Bariloche"],
    "Córdoba":      ["Rosario", "Buenos Aires", "Mendoza", "Salta"],
    "Mendoza":      ["Buenos Aires", "Córdoba", "Bariloche"],
    "Salta":        ["Córdoba"],
    "Bariloche":    ["Buenos Aires", "Mendoza"],
    "Ushuaia":      [],
}
```

Traza real, ejecutada sobre este grafo exacto (`dfs(rutas, "Rosario")`) — cada línea nueva es una llamada que **baja** un nivel; cada `<- retrocede` es una llamada que terminó su `for` y **vuelve** a la llamada de arriba, que sigue con su próximo vecino pendiente:

```
dfs(Rosario)                      NUEVO. Lo marco. Recorro vecinos: [Buenos Aires, Córdoba]
│
├─ dfs(Buenos Aires)              NUEVO. Lo marco. Recorro vecinos: [Rosario, Córdoba, Mendoza, Bariloche]
│  │
│  ├─ dfs(Rosario)                YA VISITADO -> CASO BASE, retorna sin hacer nada
│  │
│  ├─ dfs(Córdoba)                NUEVO. Lo marco. Recorro vecinos: [Rosario, Buenos Aires, Mendoza, Salta]
│  │  │
│  │  ├─ dfs(Rosario)             YA VISITADO -> retorna
│  │  ├─ dfs(Buenos Aires)        YA VISITADO -> retorna
│  │  │
│  │  ├─ dfs(Mendoza)             NUEVO. Lo marco. Recorro vecinos: [Buenos Aires, Córdoba, Bariloche]
│  │  │  │
│  │  │  ├─ dfs(Buenos Aires)     YA VISITADO -> retorna
│  │  │  ├─ dfs(Córdoba)          YA VISITADO -> retorna
│  │  │  │
│  │  │  ├─ dfs(Bariloche)        NUEVO. Lo marco. Recorro vecinos: [Buenos Aires, Mendoza]
│  │  │  │  ├─ dfs(Buenos Aires)  YA VISITADO -> retorna
│  │  │  │  └─ dfs(Mendoza)       YA VISITADO -> retorna
│  │  │  │  Bariloche agotó su for   <- RETROCEDE a Mendoza
│  │  │  │
│  │  │  Mendoza agotó su for        <- RETROCEDE a Córdoba
│  │  │
│  │  ├─ dfs(Salta)               NUEVO. Lo marco. Recorro vecinos: [Córdoba]
│  │  │  └─ dfs(Córdoba)          YA VISITADO -> retorna
│  │  │  Salta agotó su for           <- RETROCEDE a Córdoba
│  │  │
│  │  Córdoba agotó su for            <- RETROCEDE a Buenos Aires
│  │
│  ├─ dfs(Mendoza)                YA VISITADO -> retorna
│  ├─ dfs(Bariloche)              YA VISITADO -> retorna
│  Buenos Aires agotó su for          <- RETROCEDE a Rosario
│
├─ dfs(Córdoba)                   YA VISITADO -> retorna
Rosario agotó su for                 <- fin

Orden real de visita: Rosario, Buenos Aires, Córdoba, Mendoza, Bariloche, Salta
```

Notá que **Ushuaia nunca aparece** — no hay forma de llegar a ella desde Rosario, así que la recursión ni la menciona; queda afuera del conjunto `visitados` devuelto, que es justamente cómo la clase detecta que está desconectada.

> [!important] "Retroceder" no es magia: es la pila de llamadas haciendo lo de siempre
> No hace falta escribir ningún código especial para "volver atrás" — es exactamente el mismo mecanismo de pila de bandejas de [[recursion y memoizacion]]: cuando `dfs(Bariloche)` termina su `for` y hace `return`, el control vuelve al `for` de `dfs(Mendoza)` **en el punto exacto donde se había ido**, con `vecino` avanzando a la siguiente vuelta. Lo único distinto respecto de la recursión sobre árboles es que acá el "caso base" no es una condición fija de la estructura (como "no tengo hijos"), sino una condición que **cambia mientras la recursión corre**: `visitados` empieza vacío y se va llenando a medida que se avanza, así que la misma llamada `dfs(Córdoba)` que fue "nueva" la primera vez es "caso base" todas las veces siguientes. Sin ese conjunto compartido, el `Rosario → Córdoba → Rosario → Córdoba → ...` de un ciclo nunca terminaría — sería el equivalente en grafos del `RecursionError` de una recursión sin caso base.

### Paso a paso: la cola de BFS, sin recursión

BFS no usa recursión — usa una **cola** de caminos parciales, y por eso no hay "retroceso": nunca se abandona un camino a mitad de camino, simplemente se van probando todos los caminos de longitud 1, después todos los de longitud 2, etc., en el orden en que entraron a la cola (FIFO: primero el que entró primero). Trazando `camino_mas_corto(rutas, "Rosario", "Salta")` con el mismo grafo de arriba:

```python
from collections import deque

def camino_mas_corto(grafo, origen, destino):
    if origen == destino:
        return [origen]
    visitados = {origen}
    cola = deque([[origen]])          # cola de CAMINOS parciales, no de nodos sueltos
    while cola:
        camino = cola.popleft()       # saco el más antiguo -> por niveles de distancia
        ultimo = camino[-1]
        for vecino in grafo[ultimo]:
            if vecino in visitados:
                continue
            nuevo = camino + [vecino]
            if vecino == destino:
                return nuevo           # primer camino que llega = el más corto
            visitados.add(vecino)
            cola.append(nuevo)
    return None
```

| Paso | Cola al empezar (últimos nodos de cada camino) | Saco el camino que termina en... | Qué agrego a la cola |
|---|---|---|---|
| 1 | `[Rosario]` | Rosario | `Rosario→Buenos Aires`, `Rosario→Córdoba` |
| 2 | `[Buenos Aires, Córdoba]` | Buenos Aires | `...→Mendoza`, `...→Bariloche` (Rosario y Córdoba ya visitados, se saltean) |
| 3 | `[Córdoba, Mendoza, Bariloche]` | Córdoba | ¡`Córdoba → Salta` es el destino! Devuelve `[Rosario, Córdoba, Salta]` sin seguir |

Tres cosas para notar, en contraste directo con la traza de DFS de arriba:

1. **No hay una sola "rama activa"**: en el paso 2, la cola tiene simultáneamente un camino que termina en Córdoba, otro en Mendoza y otro en Bariloche — todos "vivos" a la vez, esperando su turno. DFS, en cambio, tenía en todo momento un único camino activo (la rama por la que había bajado la recursión).
2. **Ushuaia nunca entra a la cola**: como no tiene vecinos, ningún camino puede extenderse hacia ella — igual que en DFS, queda afuera sin necesidad de tratarla como caso especial.
3. **El primer camino que llega, gana**: apenas aparece `Salta` como vecino de algún camino en la cola, la función corta y devuelve — no hace falta terminar de vaciar la cola. Por eso el camino devuelto es garantizado el más corto: cualquier camino más largo a Salta todavía estaría esperando en una posición más atrasada de la cola.

### Por qué ambos cuestan $O(V+E)$

Ni DFS ni BFS visitan ningún vértice dos veces (el conjunto de visitados lo evita), así que el costo total tiene dos partes: marcar cada vértice una vez ($V$ pasos) y, para cada vértice marcado, recorrer completa su lista de vecinos. Sumar la longitud de **todas** las listas de vecinos del grafo da exactamente $2E$ (cada arista aparece dos veces: una en la lista de cada uno de sus dos extremos) — de ahí que el costo total sea proporcional a $V + E$, sin importar si el recorrido es en profundidad o en anchura. *Fuente: [[Algorithms-4th-Edition-By-Robert Sedgewick and Kevin Wayne]], cap. 4.1 (Proposiciones A y B).*

> [!tip] BFS y la distancia más corta, demostrado por inducción
> Que el primer camino que BFS encuentra a un vértice sea el más corto (en cantidad de saltos) no es casualidad: en cualquier momento del recorrido, la cola contiene primero todos los vértices a distancia $k$ de la fuente y después todos los de distancia $k+1$ — nunca se mezclan fuera de orden, porque cada vértice nuevo que entra a la cola está exactamente un salto más lejos que el vértice que lo agregó. *Fuente: [[Algorithms-4th-Edition-By-Robert Sedgewick and Kevin Wayne]], cap. 4.1 (Proposición B).*

## El mismo caso de uso que usa la bibliografía

El ejemplo de la clase —rutas aéreas entre ciudades, BFS para encontrar la ruta con menos escalas— no es un ejemplo inventado para la ocasión: es, casi literalmente, el ejemplo canónico de Sedgewick, bajo el nombre **"Grados de separación"** (*Degrees of Separation*, el nombre del programa en el libro). El libro corre el mismo algoritmo sobre una red real de rutas aéreas (`routes.txt`) para encontrar la cantidad mínima de escalas entre dos aeropuertos, y conecta la idea con dos casos más conocidos: el "juego de Kevin Bacon" (grados de separación entre actores, vía películas compartidas) y el **número de Erdős** en matemática (grados de separación entre matemáticos, vía coautoría de papers con el matemático Paul Erdős). *Fuente: [[Algorithms-4th-Edition-By-Robert Sedgewick and Kevin Wayne]], cap. 4.1.*

> [!example] Aplicaciones típicas de grafos
> Sedgewick da una lista de dominios donde el mismo patrón (ítem = vértice, relación = arista) aparece una y otra vez: mapas (intersección–calle), la web (página–link), circuitos (dispositivo–cable), cronogramas (tarea–restricción de orden), software (método–llamada entre módulos), redes sociales (persona–amistad). El grafo de islas-por-especie-compartida que arma la clase a partir de los datos de pingüinos es una instancia más de este mismo patrón: dos islas "vecinas" no porque estén cerca geográficamente, sino porque **comparten una característica** — la misma lógica con la que se arman los sistemas de recomendación ("dos productos son parecidos si los compraron los mismos clientes"). *Fuente: [[Algorithms-4th-Edition-By-Robert Sedgewick and Kevin Wayne]], cap. 4.1.*

## Un matiz sobre la recursión de DFS

La versión recursiva de DFS que usa la clase es la más clara para entender el algoritmo, pero tiene un límite práctico: cada llamada recursiva ocupa un lugar en la pila de llamadas (ver [[recursion y memoizacion]]), así que un grafo muy grande y muy "en cadena" puede agotar esa pila. La alternativa es una versión **iterativa**, con una pila explícita (una lista de Python usada con `.append()`/`.pop()`) en vez de recursión — mismo resultado, sin el límite de profundidad de la pila de llamadas:

```python
def dfs_iterativo(grafo, origen):
    visitados = {origen}
    pila = [origen]
    while pila:
        nodo = pila.pop()
        for vecino in grafo[nodo]:
            if vecino not in visitados:
                visitados.add(vecino)
                pila.append(vecino)
    return visitados
```

*Fuente: [[Essential Algorithms A Practical Approach to Computer Algorithms]], cap. 13.* Nótese el paralelismo exacto con `camino_mas_corto` (BFS) de la clase: es el mismo esqueleto —sacar un elemento pendiente, marcarlo, encolar sus vecinos no visitados— cambiando únicamente `pila.pop()` (el último agregado) por `cola.popleft()` (el primero agregado).

## Lo que viene después

BFS encuentra el camino con **menos saltos**, asumiendo que todas las conexiones "pesan" lo mismo. Si las aristas tuvieran un costo distinto —por ejemplo, duración real de vuelo en vez de solo "existe vuelo"—, BFS ya no alcanzaría para hallar el camino más *barato*, solo el más *corto en escalas*. Para eso existen los algoritmos de camino mínimo en grafos con peso (el más conocido, el algoritmo de Dijkstra), que quedan fuera del alcance de esta clase introductoria.

## Relacionado
- [[árboles]]
- [[recursion y memoizacion]]
- [[notación Big O y familias de complejidad]]
- [[listas, tuplas, diccionarios y conjuntos]]
- [[hashing y hashabilidad]]
- [[02 - Programacion imperativa]]
