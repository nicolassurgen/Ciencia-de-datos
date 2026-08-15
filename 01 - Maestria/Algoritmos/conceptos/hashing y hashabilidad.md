---
titulo: Hashing y hashabilidad
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

# Hashing y hashabilidad

> [!definition] Hash
> Un "código" numérico que se calcula a partir del **contenido** de un objeto, usado internamente para **ubicarlo rápidamente** en estructuras como diccionarios y conjuntos.

> [!definition] Hasheable
> Un objeto es **hasheable** si se le puede calcular un hash **estable** — es decir, si es [[mutabilidad e inmutabilidad|inmutable]]. `str`, `int`, `float` y `tuple` son hasheables; `list` y `dict` **no**.

## Por qué las claves de un diccionario deben ser inmutables

El diccionario **no busca clave por clave**: calcula el hash de la clave que buscás y va directo a donde debería estar guardado el valor correspondiente. Si la clave pudiera cambiar después de insertada, ese hash quedaría desactualizado y el valor se "perdería" — el diccionario ya no sabría dónde buscarlo.

```python
d = {("Torgersen", 2007): 39.1}   # una tupla SÍ puede ser clave
# d = {["Torgersen", 2007]: 39.1}  # TypeError: unhashable type: 'list'
```

Por eso las **tuplas** sirven como clave de diccionario y las **listas** no.

## Ver el hash directamente

`hash()` es la función que calcula ese código:

```python
hash(45)                # 45      -> en CPython, un entero es su propio hash (para cualquier tamaño práctico)
hash(45.0)               # 45      -> 45 y 45.0 hashean IGUAL (se comparan como iguales con ==)
hash(True)                # 1
hash((1, 2, (2, 3)))     # funciona: tupla de elementos hasheables
hash([1, 2, 3])           # TypeError: unhashable type: 'list'
hash((1, 2, [2, 3]))     # TypeError: también, aunque sea una tupla — porque contiene una lista adentro
```

> [!warning] `hash()` de un string no es estable entre ejecuciones
> A diferencia de los números, `hash("algún texto")` da un valor **distinto cada vez que se reinicia Python** (por diseño: es una protección de seguridad contra ataques que explotan colisiones de hash predecibles). No hay que depender de que un hash de string dé siempre el mismo número — solo hay que confiar en que, **dentro de la misma ejecución**, el mismo string siempre hashea igual, que es lo único que un diccionario necesita para funcionar.

*Fuente: [[Data Structures and Algorithms with Python]], cap. 5; [[Python-for-Data-Analysis]], cap. 3.*

## Qué es una colisión

Por dentro, el hash se usa para elegir **una posición** dentro de una tabla de tamaño fijo (por ejemplo, `hash(clave) % tamaño_tabla`). Dos claves distintas pueden dar la misma posición — eso es una **colisión**. Un ejemplo simple: guardar empleados por legajo en una tabla de 100 posiciones usando `legajo % 100` como hash — los legajos 145 y 245 colisionan, porque ambos dan resto 45. Un buen algoritmo de hashing no elimina las colisiones (son inevitables si hay más claves posibles que posiciones), pero sí las reparte lo más parejo posible; qué hacer cuando ocurren (encadenar los valores, buscar otra posición) es un tema de implementación de tablas hash que la materia todavía no desarrolla — alcanza con saber que el mecanismo existe y por qué. *Fuente: [[Essential Algorithms A Practical Approach to Computer Algorithms]], cap. 8.*

## La misma idea explica la velocidad de diccionarios y conjuntos

Buscar por hash es lo que permite que preguntar "¿está esta clave/este elemento?" en un diccionario o un conjunto sea **prácticamente instantáneo**, sin importar cuántos elementos tenga la estructura — a diferencia de recorrer una lista de punta a punta. Ver [[complejidad O(1) vs O(n)]].

## Puente con Tecnologías

Es la misma razón por la que el `Index` de un DataFrame de Pandas tiene que ser inmutable (ver [[01 - Introduccion a Series y DataFrame]]): Pandas usa hashing por debajo para que `df.loc["etiqueta"]` sea rápido, igual que un diccionario. Un índice mutable rompería esa tabla de hashes.

## Relacionado
- [[01 - Introduccion a la programacion]]
- [[mutabilidad e inmutabilidad]]
- [[complejidad O(1) vs O(n)]]
- [[listas, tuplas, diccionarios y conjuntos]]
- [[01 - Introduccion a Series y DataFrame]]
