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

## Cuándo usarla y cuándo no

> [!tip] Regla práctica
> Las comprensiones son ideales para **transformaciones simples de una línea**: aplicar una función, filtrar con una condición. Si hace falta más de una condición anidada, varios pasos, o un cuerpo largo, conviene escribir el `for` completo — el código corto no sirve de nada si nadie lo entiende a simple vista. Legibilidad por encima de compacidad.

## Puente con Tecnologías

Una comprensión de lista es el equivalente conceptual, en Python puro, de una operación **vectorizada** de NumPy o de un `.apply()`/máscara booleana de Pandas: ambos expresan "transformar/filtrar todos los elementos" sin escribir el bucle explícito. La diferencia real es de **rendimiento**: una comprensión de lista sigue ejecutando el bucle por dentro (uno por uno, en Python interpretado); un `array` de NumPy lo hace en código compilado. Por eso `[x**2 for x in lista]` y `array ** 2` dan el mismo resultado pero no el mismo tiempo de ejecución sobre datasets grandes — ver [[complejidad O(1) vs O(n)]] y [[03 - Ufuncs y operaciones vectorizadas]].

## Relacionado
- [[02 - Programacion imperativa]]
- [[bucles for, while y el patron acumulador]]
- [[condicionales y evaluacion de verdad]]
- [[03 - Ufuncs y operaciones vectorizadas]]
