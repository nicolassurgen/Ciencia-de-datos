---
titulo: Bucles for, while y el patrón acumulador
materia: Algoritmos
tipo: concepto
tags:
  - algoritmos
  - maestria
  - concepto
  - python
  - tema/bucles
fecha: 2026-08-08
---

# Bucles for, while y el patrón acumulador

Sin una forma de repetir, aplicar el mismo cálculo a cada uno de los 344 pingüinos del dataset exigiría escribir la misma línea 344 veces — o copiarla y pegarla, con el riesgo de que una copia quede desactualizada cuando se corrige un error. Un bucle resuelve ese problema: describe **una vez** el tratamiento y deja que el intérprete lo repita.

> [!definition] Bucle
> Estructura que ejecuta un bloque de código varias veces, para aplicar el **mismo tratamiento** a muchos elementos sin repetir código. Es lo que permite procesar los 344 pingüinos del dataset sin escribir 344 líneas.

## `for`: recorrer una colección

`for` recorre los elementos de una colección **uno por uno**, de principio a fin. La variable de control toma, en cada vuelta, el valor del siguiente elemento.

```python
especies = ["Adelie", "Gentoo", "Chinstrap"]
for especie in especies:
    print(f"Procesando: {especie}")
# Procesando: Adelie
# Procesando: Gentoo
# Procesando: Chinstrap
```

Sobre un diccionario, por defecto se recorren las **claves**; `.items()` entrega pares `(clave, valor)` que se reparten con desempaquetado:

```python
pinguino = {"especie": "Adelie", "isla": "Torgersen", "masa_g": 3750}
for clave, valor in pinguino.items():
    print(f"{clave:10s} -> {valor}")
# especie    -> Adelie
# isla       -> Torgersen
# masa_g     -> 3750
```

## `range()`, `enumerate()` y `zip()`

`range(inicio, fin, paso)` genera una secuencia de enteros sin construir una lista completa en memoria, con la misma convención que el slicing: **el fin no se incluye**.

```python
print(list(range(5)))         # [0, 1, 2, 3, 4]
print(list(range(2, 6)))      # [2, 3, 4, 5]
print(list(range(0, 10, 2)))  # [0, 2, 4, 6, 8]
```

`enumerate()` entrega la posición junto con el elemento; `zip()` recorre dos o más colecciones **en paralelo**:

```python
especies = ["Adelie", "Gentoo", "Chinstrap"]
for i, especie in enumerate(especies):
    print(f"{i}: {especie}")
# 0: Adelie
# 1: Gentoo
# 2: Chinstrap

masas = [3700.7, 5076.0, 3733.1]
for especie, masa in zip(especies, masas):
    print(f"{especie:10s} {masa:8,.1f} g")
# Adelie      3,700.7 g
# Gentoo      5,076.0 g
# Chinstrap   3,733.1 g
```

> [!warning] `zip()` se corta con la colección más corta, sin avisar
> Si las listas tienen distinta longitud, `zip()` no da error: ignora el sobrante en silencio. Es cómodo, pero puede ocultar un problema real de los datos (por ejemplo, una columna con menos registros que otra) — conviene verificar las longitudes cuando importe.

## El patrón acumulador

La mayoría de los cálculos sobre datos siguen la misma estructura de tres pasos: **inicializar** un acumulador antes del bucle, **actualizarlo** dentro, **usarlo** después.

```python
masas = [3750.0, 3800.0, 3250.0, 4500.0, 3700.0]

total = 0        # 1) inicializar
cantidad = 0

for m in masas:  # 2) acumular
    total += m
    cantidad += 1

print(f"Promedio: {total / cantidad:,.1f} g")   # 3) usar -> Promedio: 3,800.0 g
```

Combinado con un [[condicionales y evaluacion de verdad|condicional]], el mismo patrón sirve para filtrar mientras se recorre:

```python
suma, n = 0, 0
pinguinos = [{"masa_g": 3750.0}, {"masa_g": None}, {"masa_g": 4200.0}]

for p in pinguinos:
    if p["masa_g"] is None:
        continue          # saltea este registro, sigue con el próximo
    suma += p["masa_g"]
    n += 1

print(f"Promedio sobre {n} registros válidos: {suma/n:,.1f} g")
# Promedio sobre 2 registros válidos: 3,975.0 g
```

## `break` y `continue`

- **`break`** corta el bucle por completo.
- **`continue`** saltea el resto de *esta* vuelta y pasa a la siguiente (usado arriba).

```python
pinguinos = [{"especie": "Adelie"}, {"especie": "Gentoo"}, {"especie": "Gentoo"}]
for i, p in enumerate(pinguinos):
    if p["especie"] == "Gentoo":
        print(f"Primer Gentoo en la posición {i}")
        break
# Primer Gentoo en la posición 1
```

Ese patrón — recorrer hasta encontrar y frenar con `break` — es una **búsqueda lineal**, uno de los algoritmos que la clase 4 (Big-O y algoritmos de búsqueda) analiza formalmente.

## `while`: repetir mientras una condición sea verdadera

Se usa cuando no se sabe de antemano cuántas vueltas hacen falta.

```python
valor = 1
pasos = 0
while valor < 3000:
    valor *= 2
    pasos += 1

print(f"Hicieron falta {pasos} duplicaciones")   # Hicieron falta 12 duplicaciones
```

> [!danger] El peligro del `while`: bucle infinito
> Si la condición nunca se vuelve falsa, el bucle no termina nunca. Antes de ejecutar un `while`, conviene preguntarse: *¿qué línea de acá adentro hace que la condición eventualmente falle?* Si no se puede responder, el bucle es infinito. En Colab se corta manualmente con el botón de stop.

## Puente con Tecnologías

Este patrón acumulador ("recorrer y sumar/contar a mano") es exactamente lo que reemplazan las funciones vectorizadas de NumPy (`np.sum`, `np.mean` — ver [[04 - Agregaciones y estadistica descriptiva]]) y el `groupby` de Pandas (ver [[06 - Agregacion y groupby]]): mismo cálculo, sin escribir el `for` explícito y muchísimo más rápido (ver [[complejidad O(1) vs O(n)]] sobre por qué). Vale la pena escribirlo a mano una vez, acá, para entender qué esconde esa línea de Pandas.

## Relacionado
- [[02 - Programacion imperativa]]
- [[condicionales y evaluacion de verdad]]
- [[comprensiones de listas]]
- [[datos faltantes y None]]
- [[04 - Agregaciones y estadistica descriptiva]]
- [[06 - Agregacion y groupby]]
