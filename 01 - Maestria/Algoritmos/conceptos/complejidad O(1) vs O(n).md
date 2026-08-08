---
titulo: "Complejidad O(1) vs O(n)"
materia: Algoritmos
tipo: concepto
tags:
  - algoritmos
  - maestria
  - concepto
  - python
  - tema/introduccion
fecha: 2026-08-03
---

# Complejidad O(1) vs O(n)

> [!definition] Notación O grande (Big-O)
> Forma de describir cómo **crece el tiempo** (o la memoria) que toma una operación a medida que **crece el tamaño de los datos** ($n$). No mide segundos concretos, sino la **forma** en que el costo escala.

## Los dos casos de la clase

- **O(1) — tiempo constante**: la operación tarda **lo mismo** sin importar cuántos elementos haya. Buscar una clave en un **diccionario** o un elemento en un **conjunto** es O(1), gracias al [[hashing y hashabilidad|hashing]].
- **O(n) — tiempo lineal**: el costo **crece proporcional** a $n$. Buscar un elemento en una **lista** es O(n): en el peor caso hay que recorrerla entera.

```python
# Buscar en una lista -> O(n): en el peor caso recorre TODOS los elementos
elemento in lista

# Buscar en un conjunto o diccionario -> O(1): va directo, sin recorrer
elemento in conjunto
```

> [!tip] O(1) no es sinónimo de "usa hashing"
> El hashing es la forma más común de lograr tiempo constante, pero no la única. Elegir el elemento del medio de una lista por posición fija (`lista[len(lista)//2]`) también es O(1): sin importar si la lista tiene 10 o 10 millones de elementos, acceder por índice tarda lo mismo, porque no hace falta recorrer nada — la posición en memoria se calcula directo. La idea general de O(1) es "cantidad fija de pasos, sin importar $n$", no "usa un diccionario". *Fuente: [[Essential Algorithms A Practical Approach to Computer Algorithms]], cap. 1.*

## Otras operaciones y su costo

No solo "buscar" tiene un costo distinto según la estructura — **modificar** también:

- `lista.append(x)` es O(1): agregar al final no requiere mover nada.
- `lista.insert(0, x)` (insertar al principio, o en cualquier posición intermedia) es **O(n)**: hay que correr todos los elementos posteriores un lugar para hacer espacio. Si el programa inserta seguido al principio de una lista, conviene `collections.deque` (una estructura pensada para agregar/quitar rápido en ambos extremos) en vez de `list`.
- `lista_a + lista_b` dentro de un `for` (recrear la lista completa en cada vuelta del patrón acumulador) es más caro que `lista_a.extend(lista_b)`: el operador `+` construye una lista **nueva** cada vez, copiando todo lo anterior, mientras que `.extend()` agrega en el lugar. Sobre pocos elementos no se nota; sobre un bucle con muchas iteraciones, la diferencia es real.

*Fuente: [[Python-for-Data-Analysis]], cap. 3.*

## Por qué importa en la práctica

> [!important] Elegir la estructura es una decisión algorítmica
> Con un millón de elementos, un conjunto puede resolver "¿está?" **miles de veces más rápido** que una lista. No es un detalle de estilo: es la diferencia entre un análisis que corre en segundos y uno que no termina nunca.

## Relación con las estructuras de datos

Esta es la razón práctica detrás de la elección entre estructuras vista en [[listas, tuplas, diccionarios y conjuntos]]: si el uso principal de una colección es **preguntar pertenencia** repetidamente (¿está este valor?, ¿ya lo vi?), conviene un `set` o las claves de un `dict`, no una lista.

## Puente con Tecnologías

Esta es, en el fondo, la razón de ser de NumPy: un `for` en Python puro recorriendo un array es lento no por ser O(n) en sí, sino porque cada paso paga el costo extra de ser código interpretado. Vectorizar con [[03 - Ufuncs y operaciones vectorizadas|ufuncs]] no cambia la complejidad (sigue siendo O(n) internamente), pero ejecuta ese recorrido en código compilado — de ahí la diferencia de velocidad real entre "hacerlo a mano" (esta clase) y `np.sum(x)`.

## Relacionado
- [[01 - Introduccion a la programacion]]
- [[hashing y hashabilidad]]
- [[listas, tuplas, diccionarios y conjuntos]]
- [[03 - Ufuncs y operaciones vectorizadas]]
