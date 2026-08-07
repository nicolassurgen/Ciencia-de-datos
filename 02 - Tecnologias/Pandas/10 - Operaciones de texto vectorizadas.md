---
titulo: "Pandas - Operaciones de texto vectorizadas"
materia: Pandas
tipo: apunte
tags:
  - pandas
  - tecnologias
  - python
  - tema/limpieza-de-datos
fuente: "pandas — Working with text data (pandas.pydata.org/docs/user_guide/text.html); Python Data Science Handbook (Jake VanderPlas) — Parte III"
---

# Operaciones de texto vectorizadas

## El problema: los métodos de string de Python no vectorizan solos

```python
datos = ["Adelie", "adelie", "GENTOO", None, "Chinstrap"]
[s.capitalize() for s in datos]   # ValueError/AttributeError apenas aparece un None
```

Un loop a mano sobre texto se rompe apenas hay un dato faltante (ver [[datos faltantes y None]] de Algoritmos), y hay que agregar un chequeo `if s is not None` en cada vuelta. Pandas resuelve esto con el **accessor `.str`** de una `Series`: aplica el método a cada elemento, vectorizado, con manejo de `NaN` incluido de fábrica.

```python
serie = pd.Series(datos)
serie.str.capitalize()
# 0       Adelie
# 1       Adelie
# 2       Gentoo
# 3          NaN   <- no explota, propaga el faltante
# 4    Chinstrap
```

## Métodos que espejan los de Python

Casi todos los métodos de `str` de Python tienen su versión vectorizada: `lower`, `upper`, `strip`, `len`, `startswith`, `endswith`, `replace`, `split`, entre otros.

```python
df = pd.DataFrame({"especie": [" Adelie", "Gentoo ", "adelie"], "isla": ["Torgersen", "Biscoe", "Dream"]})

df["especie"].str.strip().str.lower()
# 0    adelie
# 1    gentoo
# 2    adelie
# Name: especie, dtype: object

df["isla"].str.len()          # 9, 6, 5  -> cantidad de caracteres por celda
```

> [!important] El caso de uso más común: limpiar texto antes de analizar
> Datos reales llegan con inconsistencias — `" Adelie"`, `"adelie "`, `"ADELIE"` deberían ser la misma categoría, pero para Python son tres strings distintas. `df["col"].str.strip().str.lower()` normaliza todo antes de contar categorías con [[distribución de frecuencias|value_counts()]] — es la parte de [[tratamiento primario|tratamiento primario]] que le toca al texto.

## Métodos con expresiones regulares

Un segundo grupo de métodos acepta regex y sigue las convenciones del módulo `re` de Python:

| Método | Equivalente en `re` | Qué hace |
|---|---|---|
| `str.contains(patron)` | `re.search` | ¿el patrón aparece en la celda? → booleano |
| `str.extract(patron)` | `re.match` | extrae el grupo capturado como texto nuevo |
| `str.findall(patron)` | `re.findall` | todas las coincidencias, como lista |
| `str.replace(patron, nuevo)` | — | reemplaza el patrón |
| `str.count(patron)` | — | cuenta ocurrencias |

```python
nombres = pd.Series(["Graham Chapman", "John Cleese", "Terry Gilliam"])

nombres.str.contains("Chapman")
# 0     True
# 1    False
# 2    False
# dtype: bool

nombres.str.extract(r'([A-Za-z]+)', expand=False)   # primer nombre de cada celda
# 0    Graham
# 1      John
# 2     Terry
# dtype: object
```

> [!tip] `str.contains()` es la forma vectorizada de un `in` con condición
> Es el equivalente de texto a las [[06 - Comparaciones, mascaras y filtrado booleano|máscaras booleanas]] de NumPy: devuelve una Serie de `True`/`False` que después se usa para filtrar (`df[df["col"].str.contains(...)]`).

## Acceso e indexado vectorizado

`.str[i]` y `.str[inicio:fin]` funcionan como el indexado normal de Python, pero elemento por elemento:

```python
nombres.str[0:3]
# 0    Gra
# 1    Joh
# 2    Ter
# dtype: object

nombres.str.split().str[-1]   # separar por espacio y quedarse con el último elemento (ej: apellido)
# 0    Chapman
# 1     Cleese
# 2    Gilliam
# dtype: object
```

## `get_dummies()`: de texto a columnas binarias

Cuando una columna de texto en realidad codifica **varias categorías juntas** (por ejemplo `"B|C|D"` para "nació en B, actúa en C, es escritor en D"), `str.get_dummies("|")` la separa en una columna binaria por categoría — el mismo resultado que `pd.get_dummies()` sobre una variable categórica de una sola categoría por celda.

```python
roles = pd.Series(["escritor|actor", "actor|director", "escritor"])
roles.str.get_dummies("|")
#    actor  director  escritor
# 0      1         0         1
# 1      1         1         0
# 2      0         0         1
```

> [!note] Puente con Estadística
> Convertir una variable **cualitativa** en columnas 0/1 (una por categoría) es exactamente la codificación *one-hot* — la forma en que una variable nominal (ver [[escalas de medición]]) se vuelve utilizable en un modelo numérico, sin inventar un orden donde no lo hay.

## Relacionado
- [[01 - Introduccion a Series y DataFrame]]
- [[04 - Datos faltantes]]
- [[datos faltantes y None]]
- [[tratamiento primario]]
- [[distribución de frecuencias]]
- [[escalas de medición]]
