---
titulo: Comprensiones de listas
materia: Algoritmos
tipo: concepto
tags:
  - algoritmos
  - maestria
  - concepto
  - python
  - tema/comprensiones
fecha: 2026-08-08
---

# Comprensiones de listas

El patrón "recorrer una lista y construir otra a partir de ella" (ver [[bucles for, while y el patron acumulador]]) aparece tan seguido en código real que casi siempre se repiten las mismas tres líneas: crear una lista vacía, recorrer con `for`, hacer `.append()`. Python le dio a ese patrón específico una sintaxis propia, más compacta que el `for` explícito.

> [!definition] Comprensión de lista (*list comprehension*)
> Forma compacta de escribir el patrón "recorrer una lista y armar otra a partir de ella" en una sola línea. Es sintaxis exclusiva de Python (no existe algo idéntico en la mayoría de los otros lenguajes) y aparece en prácticamente todo el código Python real.

## Equivalencia con el `for` explícito

```python
pinguinos = [{"masa_g": 3750.0}, {"masa_g": 4200.0}, {"masa_g": 3300.0}]

# Forma larga, con el patrón acumulador
masas_largo = []
for p in pinguinos:
    masas_largo.append(p["masa_g"])

# La misma cosa, en una línea
masas_corto = [p["masa_g"] for p in pinguinos]

print(masas_largo == masas_corto)   # True: son idénticas
print(masas_corto)                  # [3750.0, 4200.0, 3300.0]
```

Se lee de adentro hacia afuera: *"`p["masa_g"]`, para cada `p` en `pinguinos`"*.

## Con filtro (`if` al final)

```python
pinguinos = [
    {"especie": "Adelie",  "masa_g": 3750.0},
    {"especie": "Gentoo",  "masa_g": None},
    {"especie": "Gentoo",  "masa_g": 5200.0},
]

# Solo las masas que no faltan
masas_validas = [p["masa_g"] for p in pinguinos if p["masa_g"] is not None]
print(masas_validas)   # [3750.0, 5200.0]

# Solo los Gentoo
gentoos = [p for p in pinguinos if p["especie"] == "Gentoo"]
print(len(gentoos))    # 2
```

También existen las versiones para diccionario (`{k: v for ...}`) y conjunto (`{v for ...}`), con la misma lógica.

> [!example] Comprensión de diccionario como tabla de búsqueda
> Un uso muy frecuente: convertir una lista en un diccionario que mapea cada valor a su posición, para poder preguntar "¿en qué posición está este dato?" en O(1) en vez de recorrer la lista entera (ver [[complejidad O(1) vs O(n)]]):
> ```python
> especies = ["Adelie", "Gentoo", "Chinstrap"]
> posicion = {especie: i for i, especie in enumerate(especies)}
> print(posicion)          # {'Adelie': 0, 'Gentoo': 1, 'Chinstrap': 2}
> print(posicion["Gentoo"])  # 1  -> acceso directo, sin recorrer la lista
> ```
> *Fuente: [[Python-for-Data-Analysis]], cap. 3.*

> [!tip] Comprensiones anidadas: aplanar una lista de listas
> Cuando cada elemento de la colección es a su vez una colección, se puede recorrer ambos niveles en una sola comprensión, con dos `for` seguidos (se leen en el mismo orden en que se escribirían los `for` anidados):
> ```python
> grupos = [ ["Adelie", "Gentoo"], ["Chinstrap"], ["Adelie", "Adelie"] ]
> aplanado = [especie for grupo in grupos for especie in grupo]
> print(aplanado)   # ['Adelie', 'Gentoo', 'Chinstrap', 'Adelie', 'Adelie']
> ```
> Es exactamente el límite que menciona la regla práctica de abajo: dos niveles ya empiezan a costar de leer — a partir de ahí, casi siempre conviene el `for` explícito. *Fuente: [[Python-for-Data-Analysis]], cap. 3.*

## Cuándo usarla y cuándo no

> [!tip] Regla práctica
> Las comprensiones son ideales para **transformaciones simples de una línea**: aplicar una función, filtrar con una condición. Si hace falta más de una condición anidada, varios pasos, o un cuerpo largo, conviene escribir el `for` completo — el código corto no sirve de nada si nadie lo entiende a simple vista. Legibilidad por encima de compacidad.

> [!info] A futuro: la versión que no guarda todo en memoria
> Cambiar los corchetes por paréntesis, `(x**2 for x in range(100))`, da una **expresión generadora**: en vez de construir la lista completa de una vez, entrega los valores de a uno a medida que se piden. Útil cuando la colección es enorme y no hace falta tenerla completa en memoria al mismo tiempo. No se vio todavía en la materia — queda como referencia para cuando se trate `yield` y generadores en profundidad.

## Puente con Tecnologías

Una comprensión de lista es el equivalente conceptual, en Python puro, de una operación **vectorizada** de NumPy o de un `.apply()`/máscara booleana de Pandas: ambos expresan "transformar/filtrar todos los elementos" sin escribir el bucle explícito. La diferencia real es de **rendimiento**: una comprensión de lista sigue ejecutando el bucle por dentro (uno por uno, en Python interpretado); un `array` de NumPy lo hace en código compilado. Por eso `[x**2 for x in lista]` y `array ** 2` dan el mismo resultado pero no el mismo tiempo de ejecución sobre datasets grandes — ver [[complejidad O(1) vs O(n)]] y [[03 - Ufuncs y operaciones vectorizadas]].

## Relacionado
- [[02 - Programacion imperativa]]
- [[bucles for, while y el patron acumulador]]
- [[condicionales y evaluacion de verdad]]
- [[03 - Ufuncs y operaciones vectorizadas]]
