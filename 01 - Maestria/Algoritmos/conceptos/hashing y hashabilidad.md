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
