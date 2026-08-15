---
titulo: Árboles
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

# Árboles

## El problema, sin código todavía

Pensá en el organigrama de una empresa, o en la carpeta de un sistema de archivos, o en la clasificación biológica de los seres vivos. Los tres tienen algo en común que las listas de la clase 1 no pueden capturar bien: **se ramifican**. Un gerente tiene varios empleados a cargo, y cada uno de ellos puede tener los suyos. Una carpeta contiene archivos y otras carpetas, que a su vez contienen más archivos y carpetas. No hay forma natural de escribir eso "uno detrás de otro" en una lista sin perder la jerarquía.

Lo que sí tienen estos tres ejemplos es una propiedad más sutil: **cada parte del organigrama es, a su vez, un organigrama más chico**. Si le pedís a un gerente intermedio "mostrame tu equipo", lo que te muestra —él más toda la gente a su cargo, con su propia estructura interna— es un organigrama completo, solo que más chico que el de la empresa entera. Esa autosemejanza (una estructura hecha de copias más chicas de sí misma) es exactamente la señal de que conviene un **árbol**, y de que la recursión de la clase 2 va a ser la herramienta natural para recorrerlo.

> [!definition] Árbol
> Estructura formada por **nodos**: cada nodo puede tener varios **hijos**, y cada nodo tiene exactamente un **padre** — salvo uno, la **raíz**, que no tiene ninguno. Un nodo sin hijos es una **hoja**.

Vale la pena tener a mano la definición recursiva explícita, porque es literalmente lo que ya está escrito en el diccionario anidado de la clase:

> [!definition] Definición recursiva de árbol
> Un árbol es, o bien un único nodo raíz, o bien un nodo raíz conectado a una o más colecciones de árboles más chicos (sus subárboles). *"You can recursively define a tree to be either: a single root node — or a root node connected by branches to one or more smaller trees."* *Fuente: [[Essential Algorithms A Practical Approach to Computer Algorithms]], cap. 10.*

Esto no es una curiosidad teórica: es la razón exacta por la que `arbol["hijos"][0]` en el código de la clase **es un árbol completo** con la misma forma que el original, y por la que la receta de recorrido (procesar el nodo, después repetir lo mismo con cada hijo) funciona sin tener que saber de antemano cuántos niveles tiene el árbol.

## Vocabulario

Ya visto en clase: **nodo**, **raíz**, **hijo/padre**, **hoja**, **subárbol**, **altura** (cantidad de niveles). Cuatro términos más, de uso constante en cualquier lectura futura sobre árboles:

- **Nivel / profundidad**: la distancia desde un nodo hasta la raíz. La raíz está en el nivel 0. *"A node's level or depth in the tree is the distance from the node to the root."* *Fuente: [[Essential Algorithms A Practical Approach to Computer Algorithms]], cap. 10.*
- **Ancestro / descendiente**: los hijos de un nodo, los hijos de sus hijos, etc., son sus **descendientes**; el padre de un nodo, el padre de su padre, etc., hasta la raíz, son sus **ancestros**.
- **Grado de un nodo**: la cantidad de hijos que tiene. El grado del árbol es el máximo grado entre todos sus nodos.
- **Árbol binario**: un árbol donde cada nodo tiene **como máximo dos** hijos (a diferencia del árbol de la clase, donde `hijos` puede tener cualquier cantidad de elementos). Es el caso particular más estudiado en la bibliografía de estructuras de datos, porque simplifica mucho el análisis.

> [!tip] Una fórmula que cuantifica algo que ya calculaste en clase
> Para un árbol binario con $N$ nodos, la cantidad de ramas (conexiones padre-hijo) es siempre $N - 1$ — cada nodo, salvo la raíz, aporta exactamente una rama hacia su padre. Es el mismo tipo de relación que ya viste al escribir `contar_nodos` y `contar_hojas`: la estructura del árbol determina de antemano ciertas cantidades, sin necesidad de recorrerlo. *Fuente: [[Essential Algorithms A Practical Approach to Computer Algorithms]], cap. 10.*

## Paso a paso: así se desenrolla la recursión sobre un árbol

La recursión de la clase 2 (factorial, Fibonacci) tenía **una sola** llamada recursiva por nivel: `factorial(4)` llama a `factorial(3)`, que llama a `factorial(2)`, en una fila derecha. Sobre un árbol aparece algo nuevo que suele ser el punto donde más cuesta seguirle el rastro: **en cada nivel puede haber varias llamadas recursivas, una por cada hijo**, y hay que verlas terminar todas antes de que el nivel de arriba pueda calcular su propia respuesta. Vale la pena trazarlo con una lupa, sobre un árbol chico:

```
        A
       / \
      B   C
      |
      D
```

```python
arbol_chico = {
    "nombre": "A",
    "hijos": [
        {"nombre": "B", "hijos": [
            {"nombre": "D", "hijos": []},
        ]},
        {"nombre": "C", "hijos": []},
    ],
}

def contar_nodos(nodo):
    total = 1                            # me cuento a mí mismo
    for hijo in nodo["hijos"]:
        total += contar_nodos(hijo)      # más lo que traiga cada subárbol
    return total
```

Trazando `contar_nodos(A)` — igual que con factorial, primero se **baja** llamando, después se **sube** devolviendo, pero acá el descenso se ramifica:

```
contar_nodos(A)                                     total = 1, hijos = [B, C]
│
├─ contar_nodos(B)                                   total = 1, hijos = [D]
│  │
│  └─ contar_nodos(D)                                total = 1, hijos = []
│     └─ D no tiene hijos: el for no se ejecuta ninguna vez  <- CASO BASE, acá se da vuelta
│     contar_nodos(D) devuelve 1
│  │
│  B recibe el 1 de D: total = 1 + 1 = 2
│  contar_nodos(B) devuelve 2
│
├─ A recibe el 2 de B: total = 1 + 2 = 3   (todavía falta sumar lo que traiga C)
│
├─ contar_nodos(C)                                   total = 1, hijos = []
│  └─ C no tiene hijos: el for no se ejecuta            <- CASO BASE
│  contar_nodos(C) devuelve 1
│
A recibe el 1 de C: total = 3 + 1 = 4
contar_nodos(A) devuelve 4
```

> [!important] La diferencia con factorial: el "sube respondiendo" pasa por un `for`, no por una sola llamada
> En `factorial`, cada nivel espera **una** respuesta y hace **una** cuenta con ella (`n * factorial(n-1)`). En `contar_nodos`, cada nivel espera **varias** respuestas —una por cada hijo, en el orden en que aparecen en la lista `hijos`— y las va **acumulando** en `total` a medida que cada llamada recursiva del `for` termina y devuelve. `A` no calcula nada hasta no haber recibido la respuesta completa de `B` (que a su vez esperó la de `D`); recién ahí sigue con `C`. Es la misma fe recursiva de siempre ("confío en que `contar_nodos(hijo)` me da el resultado correcto para ese subárbol"), aplicada una vez por cada hijo en vez de una sola vez.

Con `altura` pasa exactamente lo mismo, cambiando "sumar todo lo que traen los hijos" por "quedarme con el máximo":

```python
def altura(nodo):
    if not nodo["hijos"]:
        return 1
    return 1 + max(altura(h) for h in nodo["hijos"])
```

`altura(D)` devuelve 1 (hoja, caso base) → `altura(B)` devuelve `1 + max(1) = 2` → `altura(C)` devuelve 1 (hoja) → `altura(A)` devuelve `1 + max(2, 1) = 3`. Tres niveles (A, B/C, D), que es correcto: el camino más largo desde la raíz es A→B→D.

## Los cuatro recorridos

La clase ya recorrió árboles con esta receta: procesar el nodo, después repetir con cada hijo. Eso tiene nombre — es un recorrido **preorder** (primero el nodo, después los hijos). Pero no es la única forma de recorrer un árbol, y **cuándo** procesás el nodo respecto de sus hijos no es un detalle menor: cambia qué preguntas podés responder.

La forma más clara de ver la diferencia es con un árbol que representa una expresión aritmética. Cada nodo interno es una operación, cada hoja es un número:

```
Expresión: (5 + 4) * 6 + 3

              +
            /   \
          *       3
        /   \
      +       6
    /   \
   5     4
```

```python
class NodoSuma:
    def __init__(self, izq, der):
        self.izq, self.der = izq, der
    def evaluar(self):
        return self.izq.evaluar() + self.der.evaluar()

class NodoProducto:
    def __init__(self, izq, der):
        self.izq, self.der = izq, der
    def evaluar(self):
        return self.izq.evaluar() * self.der.evaluar()

class NodoNumero:
    def __init__(self, valor):
        self.valor = valor
    def evaluar(self):
        return self.valor

expr = NodoSuma(NodoProducto(NodoSuma(NodoNumero(5), NodoNumero(4)), NodoNumero(6)), NodoNumero(3))
print(expr.evaluar())   # 57
```

> [!important] Por qué evaluar la expresión ES un recorrido postorder
> Para calcular el valor de un nodo `+` o `*`, hace falta conocer **primero** el valor de sus dos hijos — no hay forma de "procesar" la suma antes de haber bajado a ambos subárboles y vuelto con sus resultados. Esa es la diferencia exacta entre preorder y postorder: no cambia el camino que recorre la recursión, cambia **en qué momento** se procesa el nodo actual respecto de sus hijos. *Fuente: [[Data Structures and Algorithms with Python]], cap. 6.*

| Recorrido | Orden | Sobre el árbol de arriba | Cuándo se procesa el nodo |
|---|---|---|---|
| **Preorder** | nodo → hijos | `+ * + 5 4 6 3` (notación prefija) | Antes de bajar a los hijos — es lo que ya hace la clase |
| **Postorder** | hijos → nodo | `5 4 + 6 * 3 +` (notación postfija) | Después de haber procesado ambos hijos — necesario cuando el resultado de un nodo depende de sus hijos |
| **Inorder** | hijo izq. → nodo → hijo der. | `((5 + 4) * 6) + 3` (notación infija) | Entre ambos hijos — solo tiene sentido en árboles binarios, donde "izquierda" y "derecha" están definidas |
| **Level-order** | nivel por nivel | `+, *, 3, +, 6, 5, 4` | Ancho antes que profundo — necesita una **cola**, no recursión |

El primer tramo de la tabla (preorder/postorder/inorder) se recorre igual que ya lo hace la clase, cambiando solo el lugar de la línea que "procesa" el nodo respecto del bucle sobre los hijos. El último (**level-order**) es distinto de raíz: en vez de bajar todo lo posible por una rama antes de retroceder, primero visita todos los nodos de un nivel y recién después pasa al siguiente — necesita una cola (`collections.deque`), no una llamada recursiva. Esta misma idea —recorrer "por niveles" con una cola en vez de "en profundidad" con recursión— reaparece en la próxima nota con otro nombre: **BFS**, ver [[grafos y recorridos (DFS, BFS)]].

## El árbol de decisión

La conexión más directa con minería de datos: un **árbol de decisión** para clasificación es, literalmente, un árbol. Cada nodo interno hace una pregunta sobre una variable, cada rama es una respuesta posible, y cada hoja es una predicción. Recorrerlo para clasificar un caso nuevo es exactamente el mismo patrón recursivo ya visto: mirar el nodo actual, y si no es una hoja, seguir por la rama que corresponda.

Con el árbol construido a mano en clase (`aleta_mm > 206 → Gentoo`; si no, `pico_mm > 45 → Chinstrap`, si no, `Adelie`) sobre las 342 mediciones completas del dataset de pingüinos:

![[Arbol de decision - pinguinos.png]]

Dos preguntas alcanzan para separar casi perfectamente las tres especies con **95,0 % de exactitud** — el gráfico muestra por qué: las líneas de corte (206 mm de aleta, 45 mm de pico) efectivamente separan las tres nubes de puntos de colores, con muy pocos casos mal clasificados cerca de los bordes. Verificado recalculando sobre el dataset real (`seaborn-data/penguins.csv`), no solo tomado del apunte de clase.

### Paso a paso: `predecir` es recursión de un solo camino, no ramificada

A diferencia de `contar_nodos` (que llama recursivamente a **cada** hijo y después combina todas las respuestas), `predecir` sigue **una sola rama** en cada nivel — se parece más al patrón derecho de `factorial` que al patrón ramificado de arriba. Trazando un pingüino con `aleta_mm=195` y `pico_mm=48`:

```python
arbol_decision = {
    "pregunta": "aleta_mm > 206",
    "si": {"prediccion": "Gentoo"},
    "no": {
        "pregunta": "pico_mm > 45",
        "si": {"prediccion": "Chinstrap"},
        "no": {"prediccion": "Adelie"},
    },
}

def predecir(nodo, pinguino):
    if "prediccion" in nodo:                    # CASO BASE: llegué a una hoja
        return nodo["prediccion"]
    if nodo["pregunta"] == "aleta_mm > 206":
        rama = "si" if pinguino["aleta_mm"] > 206 else "no"
    else:
        rama = "si" if pinguino["pico_mm"] > 45 else "no"
    return predecir(nodo[rama], pinguino)       # CASO RECURSIVO: bajo un nivel
```

```
predecir(raíz, pingüino)                         raíz = {"pregunta": "aleta_mm > 206", ...}
│  "prediccion" no está en raíz -> no es hoja, sigo
│  pregunta: ¿aleta_mm (195) > 206?  ->  NO  ->  rama = "no"
│  return predecir(raíz["no"], pingüino)
│
└─ predecir(nodo_pico, pingüino)                 nodo_pico = {"pregunta": "pico_mm > 45", ...}
   │  "prediccion" no está en nodo_pico -> no es hoja, sigo
   │  pregunta: ¿pico_mm (48) > 45?  ->  SÍ  ->  rama = "si"
   │  return predecir(nodo_pico["si"], pingüino)
   │
   └─ predecir({"prediccion": "Chinstrap"}, pingüino)
      │  "prediccion" SÍ está en el nodo  <- CASO BASE, acá se da vuelta
      └─ return "Chinstrap"

   predecir(nodo_pico, ...) recibe "Chinstrap" y lo devuelve tal cual
predecir(raíz, ...) recibe "Chinstrap" y lo devuelve tal cual
```

Cada nivel no combina nada (no hay `+` ni `max` como en `contar_nodos`): simplemente **reenvía hacia arriba**, sin cambios, lo que le devolvió el nivel de abajo. Es el patrón recursivo más simple posible sobre un árbol — bajar por un único camino hasta una hoja, y subir la respuesta intacta hasta el llamado original.

> [!warning] Dos cosas distintas se llaman igual: "árbol de decisión"
> El término **"árbol de decisión"** en machine learning (el de arriba: clasificar datos con preguntas sobre variables) no es lo mismo que **"árbol de decisión"** en teoría de algoritmos y teoría de juegos, donde se usa para modelar secuencias de decisiones en problemas combinatorios (por ejemplo, un árbol de jugadas posibles en tic-tac-toe, con minimax para elegir la mejor). Comparten la misma estructura —nodo interno = decisión, hoja = resultado final— pero resuelven problemas distintos: uno aprende de datos, el otro explora posibilidades. *Fuente: [[Essential Algorithms A Practical Approach to Computer Algorithms]], cap. 12.*

## Cuánto cuesta operar sobre un árbol

Todo lo anterior asumió implícitamente que recorrer un árbol tarda lo que tarda porque hay que visitar cada nodo una vez — proporcional a $N$. Pero hay una pregunta más fina, relevante en particular para un **árbol binario de búsqueda** (donde además cada nodo tiene un valor, y el hijo izquierdo tiene valores menores, el derecho mayores): ¿de qué depende el costo de **buscar** algo en el árbol, en vez de recorrerlo entero?

> [!important] Todo depende de la altura, no de la cantidad de nodos
> En un árbol binario de búsqueda, buscar, insertar o borrar cuesta tiempo proporcional a la **altura** del árbol, no a la cantidad de nodos. Con $N$ nodos, dos casos extremos son posibles:
>
> | | Árbol balanceado | Árbol degenerado ("palo") |
> |---|---|---|
> | Forma | Cada nodo reparte parejo a izquierda y derecha | Cada nodo tiene un solo hijo, en fila |
> | Altura | $O(\log N)$ | $O(N)$ |
> | Buscar / insertar | $O(\log N)$ | $O(N)$ |
>
> El caso degenerado no es hipotético: insertar valores **ya ordenados** (1, 2, 3, 4...) en un árbol binario de búsqueda produce exactamente esa forma de "palo" extendido hacia un solo lado. *"When the tree is a stick or even close to being a stick, the efficiency characteristics of a binary search tree are no better than that of a linked list."* *Fuente: [[Data Structures and Algorithms with Python]], cap. 6 y 10.*

Dato adicional para dimensionar el caso típico (no el peor, el promedio): construyendo un árbol binario de búsqueda con $N$ claves en orden aleatorio, la altura promedio se acerca a $2{,}99 \lg N$ — sigue siendo logarítmica, muy lejos del caso degenerado. *Fuente: [[Algorithms-4th-Edition-By-Robert Sedgewick and Kevin Wayne]], cap. 3.2 (resultado de L. Devroye).*

Esta distinción —mismo tipo de estructura, costo radicalmente distinto según su forma— es el primer ejemplo concreto de por qué hace falta un lenguaje más preciso que "más rápido" o "más lento" para hablar de costo. Ese lenguaje es la notación Big O, desarrollada en [[notación Big O y familias de complejidad]].

## Relacionado
- [[01 - Introduccion a la programacion]]
- [[02 - Programacion imperativa]]
- [[recursion y memoizacion]]
- [[grafos y recorridos (DFS, BFS)]]
- [[notación Big O y familias de complejidad]]
- [[complejidad O(1) vs O(n)]]
