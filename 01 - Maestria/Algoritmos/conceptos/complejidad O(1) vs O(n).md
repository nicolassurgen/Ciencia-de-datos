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
