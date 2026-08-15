---
titulo: "Clase 1 — Introducción a la programación en Python"
materia: Algoritmos
tipo: apunte
clase: 1
fecha: 2026-08-01
tags:
  - algoritmos
  - maestria
  - python
  - estructuras-de-datos
  - tema/introduccion
---

# Algoritmos · Clase 1 — Introducción a la programación en Python

> [!abstract] Idea central de la clase
> Un **algoritmo** es una receta que transforma datos. Antes de escribir esa receta hay que saber **qué formas puede tomar un dato** dentro de la computadora. La clase recorre esas formas de menor a mayor: desde un número suelto (**tipos primitivos**) hasta una tabla completa (**estructuras de datos**), y cierra armando un **dataset real "a mano"**, sin librerías.
>
> Dos ideas para llevarse:
> 1. **La estructura de datos que elegís es una decisión algorítmica** (buscar en un conjunto fue miles de veces más rápido que en una lista).
> 2. **Las herramientas cómodas esconden trabajo, no lo eliminan**: entender el mecanismo es lo que te permite diagnosticar cuando algo falla.

> [!info] Puente con Estadística
> Los tipos de Python se corresponden directo con los tipos de variable del otro curso: `int`/`float` → **cuantitativas** (discreta/continua), `str` → **cualitativas**, `bool` → **binarias**, `None` → **datos faltantes**. Representar bien los datos acá es la base para el [[tratamiento primario]] y el análisis descriptivo de allá. → [[variables|Variables y escalas]]

> [!note] Convención de esta nota
> Los callouts **"Puente con Estadística"** y **"Puente con Tecnologías"** (este de acá abajo incluido) son agregados míos para conectar con el resto de la maestría — no los dio la profesora. El resto sigue de cerca la clase.

> [!info] Puente con Tecnologías
> A propósito, esta clase **no usa NumPy ni Pandas** — la idea es entender qué hay "debajo" antes de usar la versión rápida (la segunda idea para llevarse, arriba). Cuando llegues a esas notas vas a reconocer todo esto con otro nombre: un `array` de NumPy es una [[listas, tuplas, diccionarios y conjuntos|lista]] con superpoderes (ver [[01 - Introduccion y arrays]]); un `DataFrame` de Pandas es, en el fondo, una [[lista de diccionarios y JSON|lista de diccionarios]] con índice (ver [[01 - Introduccion a Series y DataFrame]]); y la razón de ser de NumPy es precisamente evitar los loops de Python que hoy escribiste a mano (ver [[complejidad O(1) vs O(n)]] y [[03 - Ufuncs y operaciones vectorizadas]]).

---

## 1. El entorno: Google Colab

**Colab** es un cuaderno (*notebook*) que corre en servidores de Google: no hay nada que instalar. Se compone de **celdas**:

- **Celdas de texto** → explicaciones, títulos, fórmulas. No se ejecutan.
- **Celdas de código** → contienen Python y **sí** se ejecutan (`Shift + Enter`).

```python
# Todo lo que empieza con # es un COMENTARIO: Python lo ignora.
print("Hola, Maestría en Minería de Datos")
```

`print()` es una **función**: le pasamos algo entre paréntesis y lo muestra en pantalla.

> [!warning] Dos trampas del primer día
> 1. Una celda muestra automáticamente el resultado de la **última línea**, aunque no uses `print`. Para ver varias cosas, poné `print` en cada una.
> 2. Las celdas **comparten memoria**, pero se ejecutan **en el orden en que las corrés**, no en el que están escritas. Es la causa nº 1 de errores raros en notebooks. (Si algo se pone raro: reiniciá el entorno y ejecutá todo de arriba abajo.)

> [!tip] Leer los errores sin miedo
> Los errores son parte normal del trabajo. Python te dice **en qué línea** falló y **qué tipo** de error fue. Leer la **última línea** del mensaje resuelve el 90 % de los casos. Ejemplo: `print("hola"` sin cerrar el paréntesis → `SyntaxError: incomplete input`.

---

## 2. Tipos de datos primitivos

Un **tipo de dato** define qué valores puede tomar algo y qué operaciones tienen sentido. Podés sumar dos números; no tiene sentido dividir dos palabras. Los cinco primitivos:

| Tipo | Python | Ejemplo | Para qué sirve | Variable estadística |
|---|---|---|---|---|
| Entero | `int` | `42`, `-7`, `0` | Contar (filas, edad, año) | Cuantitativa discreta |
| Real | `float` | `3.14`, `39.1` | Medir (peso, temperatura, precio) | Cuantitativa continua |
| Texto | `str` | `"Adelie"` | Nombres, categorías, etiquetas | Cualitativa |
| Lógico | `bool` | `True`, `False` | Respuestas sí/no | Binaria |
| Vacío | `NoneType` | `None` | "Acá no hay dato" | Dato faltante |

La función `type()` dice de qué tipo es un valor:

```python
print(type(42))        # int
print(type(39.1))      # float
print(type("Adelie"))  # str
print(type(True))      # bool
print(type(None))      # NoneType
```

### `int` vs `float`: por qué importa

Un `int` es **exacto**; un `float` es una **aproximación** (la máquina guarda los decimales en una cantidad finita de bits), y de ahí salen sorpresas:

```python
print(0.1 + 0.2)                     # 0.30000000000000004
print(0.1 + 0.2 == 0.3)              # False (!)
print(round(0.1 + 0.2, 10) == 0.3)   # True -> la forma correcta de comparar
```

> [!important] Regla práctica con reales
> **Nunca compares dos `float` con `==`.** Compará si su diferencia es menor a una tolerancia chica. Esto reaparece al evaluar modelos. (El motivo profundo es la representación binaria de punto flotante, estándar **IEEE 754**: números como 0.1 no tienen representación exacta en base 2 — el mecanismo completo, con la analogía de por qué esto ya pasa en base 10 con 1/3, está en [[tipos primitivos en Python]].)

### Operaciones aritméticas

```python
a, b = 17, 5
print(a + b)    # suma            22
print(a - b)    # resta           12
print(a * b)    # producto        85
print(a / b)    # división        3.4   <- SIEMPRE devuelve float
print(a // b)   # división entera 3     <- descarta el resto
print(a % b)    # resto (módulo)  2     <- lo que sobra
print(a ** b)   # potencia        1419857
```

> [!note] El módulo `%` es más útil de lo que parece
> Sirve para detectar múltiplos, repartir en grupos y recorrer en forma circular. El uso más común: **¿es par?**
> ```python
> print(10 % 2 == 0)   # True  -> par
> print(7 % 2 == 0)    # False -> impar
> ```

---

## 3. Variables

Una **variable** es un nombre que le ponemos a un valor para reutilizarlo. Se crea con `=`, que no significa "igual" sino **"asignále a la izquierda lo de la derecha"**.

```python
especie = "Adelie"        # str
largo_pico_mm = 39.1      # float
cantidad_medida = 152     # int
esta_en_riesgo = False    # bool
sexo = None               # dato faltante
```

### Tipado dinámico

No hay que **declarar** el tipo: Python lo deduce del valor, y una misma variable puede cambiar de tipo. Es cómodo, pero también una fuente clásica de errores.

```python
x = 10
print(x, type(x))          # 10 <class 'int'>
x = "ahora soy texto"
print(x, type(x))          # ahora soy texto <class 'str'>
```

### Nombres de variables

- Letras, números y `_`, pero **no** pueden empezar con número.
- Distinguen mayúsculas: `edad` ≠ `Edad`.
- Convención Python: `minusculas_con_guiones_bajos` (*snake_case*).
- **Elegí nombres que expliquen qué guardan**: `largo_pico_mm` es infinitamente mejor que `x1`. Es lo que te permite releer tu propio código dentro de un mes.

### Conversión de tipos (*casting*)

```python
texto = "39.1"
numero = float(texto)      # texto -> real
print(int(39.9))           # 39  <- int() TRUNCA hacia cero, NO redondea
print(round(39.9))         # 40  <- round() sí redondea
print(str(39.1) + " mm")   # número -> texto para concatenar
```

> [!warning] `int()` trunca, no redondea
> `int(39.9)` es `39`. Confundir `int()` con `round()` genera **sesgos silenciosos** en un análisis. (Dato extra: `round()` en Python usa "redondeo bancario" —al par más cercano—, así que `round(2.5)` da `2`, no `3`. Sorprende, pero es correcto.)

### Trabajar con texto (`str`)

```python
isla = "Torgersen"
print(len(isla))       # 9  -> cantidad de caracteres
print(isla.upper())    # TORGERSEN
print(isla.lower())    # torgersen
print(isla[0])         # T  -> primer carácter (¡las posiciones empiezan en 0!)
print(isla[-1])        # n  -> último carácter
print(isla[0:4])       # Torg  -> de la 0 a la 3 (la 4 NO se incluye)
```

> [!important] La convención más importante de Python: el final del rango NO se incluye
> `isla[0:4]` toma las posiciones 0, 1, 2, 3. Esto vale para **texto, listas y —más adelante— DataFrames**. Vale la pena que se vuelva automático.

**f-strings** — la forma moderna de armar texto con variables adentro (una `f` antes de las comillas, variables entre llaves):

```python
especie, largo = "Adelie", 39.1
print(f"El pingüino {especie} tiene un pico de {largo} mm")
print(f"Redondeado: {largo:.1f} mm")   # :.1f = un decimal
```

Después de `:` va el **especificador de formato**: `.1f` significa "número decimal (`f`, de *float*) con 1 dígito después de la coma" — `.2f` daría dos dígitos, `.0f` ninguno (redondeado a entero). También se usa para separar miles (`:,` — ver el ejemplo de `promedio` más abajo) o para alinear texto en columnas (`:10s`, diez espacios de ancho). No hace falta memorizar todas las variantes: alcanza con reconocer el patrón `{valor:especificador}` y buscar el especificador puntual que haga falta cuando aparezca.

### Comparaciones y valores lógicos

Las comparaciones devuelven `True`/`False` y son la base de las decisiones (que se ven la próxima clase):

```python
largo = 39.1
print(largo > 40)      # mayor
print(largo == 39.1)   # IGUAL -> se escribe con DOS signos =
print(largo != 39.1)   # distinto
print(largo >= 39.1)   # mayor o igual
```

> [!important] `=` vs `==` — el error más frecuente de quien arranca
> `=` **asigna** un valor a una variable. `==` **pregunta** si dos cosas son iguales. No son intercambiables.

Se combinan condiciones con `and`, `or`, `not`:

```python
pico_largo = 39.1 > 35   # True
pico_ancho = 18.7 > 20   # False
print(pico_largo and pico_ancho)   # False -> exige las dos
print(pico_largo or pico_ancho)    # True  -> al menos una
print(not pico_largo)              # False -> negación
```

### `None`: el dato que no está

`None` representa **ausencia de información**; no es `0` ni texto vacío. En datos reales aparece todo el tiempo (una medición que no se tomó) y tratarlo mal arruina el análisis.

```python
sexo = None
print(sexo is None)    # True  -> forma recomendada de comparar con None
print(sexo == None)    # funciona, pero NO es lo recomendado
print(None == 0)       # False -> None no es cero
print(None == "")      # False -> None no es texto vacío
```

> [!note] `is` vs `==` (identidad vs igualdad)
> `==` pregunta si dos valores **son iguales**; `is` pregunta si son **el mismo objeto** en memoria. Para `None` se usa `is` porque `None` es único: existe una sola vez en todo el programa. Esta distinción reaparece abajo, en la "trampa de la copia compartida".

---

## 4. Estructuras de datos I: listas y tuplas

Con un valor suelto no se llega lejos: hay que **agrupar** datos. Una **estructura de datos** es una forma organizada de guardar varios valores con reglas de acceso. Listas y tuplas son **secuenciales**: mantienen orden y se accede por posición.

### 4.1. Listas — ordenada y **mutable**, entre corchetes `[ ]`

Pensala como una **columna de una tabla**. Es la estructura más usada.

```python
largos_pico = [39.1, 39.5, 40.3, 36.7, 39.3, 38.9, 39.2]
print(len(largos_pico))   # 7
```

**Indexado** — cada elemento tiene una posición. Regla a grabar a fuego: **los índices empiezan en 0**. Los negativos cuentan desde el final.

```
lista:    [39.1,  39.5,  40.3,  36.7,  39.3,  38.9,  39.2]
índice:      0      1      2      3      4      5      6
negativo:   -7     -6     -5     -4     -3     -2     -1
```

```python
print(largos_pico[0])    # 39.1  -> primero
print(largos_pico[-1])   # 39.2  -> último (siempre)
print(largos_pico[7])    # IndexError: list index out of range
```

**Rebanadas (*slicing*)** — `lista[desde:hasta]`, y de nuevo **`hasta` no se incluye**:

```python
print(largos_pico[0:3])   # [39.1, 39.5, 40.3]  -> posiciones 0,1,2
print(largos_pico[:3])    # lo mismo (si arranca en 0 se omite)
print(largos_pico[2:])    # del tercero en adelante
print(largos_pico[-2:])   # los dos últimos
print(largos_pico[::2])   # uno de cada dos (el tercer número es el paso)
print(largos_pico[::-1])  # al revés (paso negativo)
```

**Modificar** — una lista es **mutable**:

```python
m = [39.1, 39.5, 40.3]
m[0] = 38.0          # cambiar un elemento
m.append(36.7)       # agregar al final
m.insert(1, 99.9)    # insertar en una posición
m.remove(99.9)       # eliminar por VALOR
ultimo = m.pop()     # eliminar por POSICIÓN (por defecto el último) y devolverlo
```

**Funciones útiles sobre números:**

```python
print(sum(largos_pico))                        # suma
print(min(largos_pico), max(largos_pico))      # mínimo y máximo
print(sum(largos_pico) / len(largos_pico))     # promedio
print(sorted(largos_pico))   # devuelve una lista NUEVA ordenada
```

> [!note] `sorted()` vs `.sort()`
> `sorted(lista)` **devuelve una copia** ordenada y deja la original intacta. `lista.sort()` **modifica la original** y no devuelve nada. → En la **clase 4** se abre la caja de `sorted()` para ver cómo se implementa un algoritmo de ordenamiento y por qué el de Python es tan rápido.

> [!warning] Trampa clásica: las listas se comparten, no se copian
> Asignar una lista a otra variable **no crea una copia**: ambas apuntan al mismo objeto.
> ```python
> a = [1, 2, 3]
> b = a          # NO es una copia: a y b son el mismo objeto
> b.append(4)
> print(a)       # [1, 2, 3, 4]  <- ¡a también cambió!
> ```
> La forma correcta de copiar: `b = a.copy()` (o `list(a)`, o `a[:]`). Esto conecta con `is` vs `==`: `a is b` sería `True` en el primer caso.

**Listas dentro de listas → una tabla** (lista de filas, cada fila una lista):

```python
tabla = [
    ["Adelie",    "Torgersen", 39.1, 3750],
    ["Adelie",    "Biscoe",    37.8, 3400],
    ["Gentoo",    "Biscoe",    46.1, 4500],
]
print(tabla[2][3])   # 4500  -> fila 2, columna 3
```

`tabla[2][3]` se lee de izquierda a derecha: **fila 2**, y de ella **columna 3**. Ya se vuelve incómodo: hay que **acordarse** de que la columna 3 es la masa. El diccionario (bloque 4) resuelve eso.

### 4.2. Tuplas — como una lista pero **inmutable**, entre paréntesis `( )`

```python
coordenada = (-34.6, -58.4)     # latitud, longitud de Buenos Aires
print(coordenada[0])            # se accede igual que una lista
coordenada[0] = 0.0             # TypeError: no admite asignación
```

> [!tip] ¿Para qué querríamos algo que no se puede cambiar?
> 1. **Seguridad** — si un dato no debe cambiar (una coordenada, una fecha de nacimiento), la inmutabilidad lo garantiza.
> 2. **Velocidad** — son más livianas y rápidas que las listas.
> 3. **Se pueden usar como clave de un diccionario** (las listas no).
>
> Regla: colección de *varias cosas del mismo tipo que van a cambiar* → **lista**; *un registro con campos fijos* → **tupla**.

**Desempaquetado** — repartir una tupla en varias variables de una:

```python
pinguino = ("Adelie", "Torgersen", 39.1, 3750)
especie, isla, pico, masa = pinguino
```

**Truco derivado** — intercambiar dos variables sin auxiliar (se usa en ordenamiento, clase 4):

```python
x, y = 10, 20
x, y = y, x      # ahora x=20, y=10
```

---

## 5. Estructuras de datos II: diccionarios y conjuntos

### 5.1. Diccionarios — pares **clave → valor**, entre llaves `{ }`

Resuelven el problema de `tabla[2][3]`: en vez de acceder **por posición**, accedemos **por nombre**.

```python
pinguino = {
    "especie": "Adelie",
    "isla": "Torgersen",
    "largo_pico_mm": 39.1,
    "masa_g": 3750,
}
print(pinguino["especie"])   # Adelie  -> el acceso se autoexplica
print(pinguino["masa_g"])    # 3750
```

**Reglas:**
- Las **claves** deben ser únicas e **inmutables** (texto, números, tuplas — **nunca** listas).
- Los **valores** pueden ser cualquier cosa (incluso otros diccionarios o listas).
- Pedir una clave que no existe → `KeyError`.

> [!note] Por qué las claves deben ser inmutables (*hashables*)
> El diccionario ubica cada valor calculando un "código" (hash) de la clave. Si la clave pudiera cambiar, ese código quedaría desactualizado y el valor se "perdería". Por eso las tuplas sirven como clave (no cambian) y las listas no. Esta misma idea de hashing explica por qué buscar en diccionarios y conjuntos es tan rápido (ver 5.2).

**`.get()`** — la forma **segura** de acceder (devuelve `None` o un valor por defecto si la clave falta):

```python
print(pinguino.get("edad"))                # None (no explota)
print(pinguino.get("edad", "sin dato"))    # sin dato
```

**Modificar / agregar / eliminar y recorrer:**

```python
pinguino["masa_g"] = 3800          # modificar
pinguino["anio_medicion"] = 2007   # agregar
del pinguino["isla"]               # eliminar

print(list(pinguino.keys()))       # claves
print(list(pinguino.values()))     # valores
print(list(pinguino.items()))      # pares (clave, valor)
print("especie" in pinguino)       # True  -> ¿existe la clave?
```

> [!important] La estructura estrella: lista de diccionarios = un dataset
> Combinando ambas ideas se obtiene la representación estándar de un **dataset**: una **lista** (las filas) de **diccionarios** (los campos de cada fila). Es la forma en que viaja la info en la web (**JSON**) y la antesala directa del **DataFrame de Pandas** (clase 5).
> ```python
> pinguinos = [
>     {"especie": "Adelie", "isla": "Torgersen", "pico_mm": 39.1, "masa_g": 3750},
>     {"especie": "Gentoo", "isla": "Biscoe",    "pico_mm": 46.1, "masa_g": 4500},
> ]
> print(pinguinos[1]["especie"])   # Gentoo -> registro 1, campo especie
> ```
> Cada corchete **baja un nivel** en la estructura.

### 5.2. Conjuntos — sin orden y **sin repetidos**, con llaves `{ }`

Es el conjunto matemático de siempre.

```python
islas = {"Torgersen", "Biscoe", "Biscoe", "Dream", "Torgersen"}
print(islas)       # los repetidos desaparecen solos
print(len(islas))  # 3
```

**Uso más frecuente: valores únicos de una columna** (responder *"¿cuántas categorías tiene esta variable?"*, una de las primeras preguntas de toda exploración):

```python
columna = ["Adelie", "Adelie", "Gentoo", "Chinstrap", "Gentoo"]
print(set(columna))        # {'Adelie', 'Gentoo', 'Chinstrap'}
print(len(set(columna)))   # 3 categorías distintas
```

**Operaciones de conjunto** (base conceptual de los *joins* entre tablas, clase 5):

```python
a = {"Torgersen", "Biscoe"}
b = {"Biscoe", "Dream"}
print(a | b)   # unión: en alguno de los dos
print(a & b)   # intersección: en los dos
print(a - b)   # diferencia: en a y no en b
print(a ^ b)   # diferencia simétrica: en uno solo
```

> [!important] Elegir la estructura es una decisión algorítmica
> Preguntar *"¿este elemento está?"* en un **conjunto** es **inmediato** sin importar el tamaño; en una **lista** hay que recorrerla entera. Con un millón de elementos, el conjunto puede ser **miles de veces** más rápido. En jerga: la búsqueda es $O(1)$ (tiempo constante) en un conjunto/diccionario, frente a $O(n)$ (lineal) en una lista. → Es el tema central de la **clase 3**. No es un detalle: es la diferencia entre un análisis que corre en segundos y uno que no termina nunca.

---

## 6. Resumen de las cuatro estructuras

| Estructura | Sintaxis | ¿Ordenada? | ¿Modificable? | ¿Repetidos? | Uso típico |
|---|---|:---:|:---:|:---:|---|
| **Lista** | `[1, 2, 3]` | Sí | Sí | Sí | Una columna, una secuencia |
| **Tupla** | `(1, 2, 3)` | Sí | **No** | Sí | Un registro fijo, una coordenada |
| **Diccionario** | `{"a": 1}` | Sí (por inserción) | Sí | Claves no | Un registro con campos nombrados |
| **Conjunto** | `{1, 2, 3}` | **No** | Sí | **No** | Valores únicos, pertenencia rápida |

---

## 7. Caso aplicado: un dataset real, a mano

El dataset **Palmer Penguins** (344 pingüinos, 3 especies, 3 islas de la Antártida) es un clásico moderno para enseñar análisis de datos, con algo valioso: **valores faltantes reales**. Se lee **sin Pandas**, usando solo lo de la clase, para ver qué hay debajo de las herramientas cómodas.

**Leer el CSV y convertirlo en lista de diccionarios:**

```python
import urllib.request, csv

URL = "https://raw.githubusercontent.com/mwaskom/seaborn-data/master/penguins.csv"
with urllib.request.urlopen(URL) as r:
    texto = r.read().decode("utf-8")

lineas = texto.splitlines()
filas = list(csv.DictReader(lineas))   # usa la 1ª fila como claves
print(filas[0])   # un diccionario por pingüino
```

`csv.DictReader` produce **una lista de diccionarios** a partir de un archivo real. Dos observaciones clave:

- **Todo llega como texto (`str`)**: el CSV no sabe de tipos. Convertir cada campo al tipo correcto es el primer paso de cualquier preparación de datos.
- Hay **campos vacíos** (`Adelie,Torgersen,,,,,`) → son los datos faltantes, los `None` del bloque 2.

> [!warning] Los faltantes rompen las conversiones
> ```python
> float("")   # ValueError: could not convert string to float: ''
> ```
> No se puede convertir la cadena vacía a número. La decisión más honesta al principio es **representar el faltante como `None`**:
> ```python
> def a_numero(texto):
>     if texto == "":
>         return None
>     return float(texto)
> ```
> (La sintaxis de `def` e `if` se ve en detalle la próxima clase.)

**Preguntas sobre los datos, con lo de hoy:**

```python
# Valores únicos -> CONJUNTOS
especies = {p["especie"] for p in pinguinos}

# Contar faltantes de masa
faltantes = sum(1 for p in pinguinos if p["masa_g"] is None)

# Promedio EXCLUYENDO faltantes (¡no tratarlos como 0!)
masas = [p["masa_g"] for p in pinguinos if p["masa_g"] is not None]
promedio = sum(masas) / len(masas)
```

> [!note] Adelanto de sintaxis: esto es una comprensión
> La forma `[algo for elemento in coleccion if condicion]` (y su versión con `{ }` para conjuntos) se llama **comprensión** — una forma compacta de "recorrer y filtrar" en una sola línea. Se explica en detalle recién en la clase 2, en [[comprensiones de listas]]; acá se usa un poco antes porque es, con diferencia, la forma más natural de responder este tipo de pregunta sobre los datos. Si por ahora resulta más clara escrita como un `for` de toda la vida, es exactamente equivalente:
> ```python
> masas = []
> for p in pinguinos:
>     if p["masa_g"] is not None:
>         masas.append(p["masa_g"])
> ```

> [!important] Decisión del analista, no de la herramienta
> El promedio se calcula sobre las mediciones **válidas**. Si se tratara a los faltantes como cero, el promedio bajaría **artificialmente**. Qué hacer con los faltantes es una decisión **del analista**. (Enlaza con el [[tratamiento primario]] de Estadística.)

**"Group by" a mano** — masa promedio por especie, con un diccionario de acumuladores:

```python
suma, conteo = {}, {}
for p in pinguinos:
    if p["masa_g"] is None:
        continue
    e = p["especie"]
    suma[e] = suma.get(e, 0) + p["masa_g"]
    conteo[e] = conteo.get(e, 0) + 1
# promedio por especie = suma[e] / conteo[e]
```

> [!tip] El mismo patrón, más idiomático: `setdefault()` y `defaultdict`
> `dict.get(clave, 0)` es la forma más explícita de "leer o usar un valor por defecto", pero no la única. `collections.defaultdict(int)` hace lo mismo automáticamente, sin repetir el `.get(..., 0)` en cada línea — desarrollo completo, con el mismo ejemplo llevado un paso más allá, en [[listas, tuplas, diccionarios y conjuntos]].

Todo eso, en la **clase 5** con Pandas, es una línea:

```python
df.groupby("especie")["masa_g"].mean()
```

> [!tip] La moraleja del caso
> Escribir el `group by` a mano muestra **cuánto código** y **cuánto lugar para equivocarse** esconde esa única línea. Ahora ya sabés **qué hace por dentro** — esa es la diferencia entre *usar* una herramienta y *entenderla*.

---

## 8. Errores comunes (consolidado)

Aparecieron dispersos en la clase; conviene tenerlos juntos porque los vas a ver mil veces:

| Error | Qué significa | Causa típica |
|---|---|---|
| `SyntaxError` | Python no entiende la línea | Falta un `)`, `:`, comilla sin cerrar |
| `IndexError` | Índice fuera de rango | `lista[7]` en una lista de 7 elementos (válidos 0–6) |
| `KeyError` | La clave no existe en el diccionario | `dic["edad"]` sin esa clave → usar `.get()` |
| `TypeError` | Operación inválida para ese tipo | Modificar una tupla; sumar `str` + `int` |
| `ValueError` | Tipo correcto, valor imposible | `float("")` o `float("hola")` |

> [!note] Leé siempre la **última** línea del traceback: ahí está el tipo de error y el mensaje.

---

## 9. Mapa de la clase

![[Mapa de la clase - DATO.png]]

---

## Conceptos para desarrollar en notas aparte
- [[tipos primitivos en Python]]
- [[mutabilidad e inmutabilidad]]
- [[indexado y slicing]]
- [[is vs == (identidad vs igualdad)]]
- [[listas, tuplas, diccionarios y conjuntos]]
- [[hashing y hashabilidad]]
- [[complejidad O(1) vs O(n)]]
- [[datos faltantes y None]]
- [[lista de diccionarios y JSON]]

## Preguntas de repaso
1. ¿Por qué `0.1 + 0.2 == 0.3` da `False` en Python, y cuál es la forma correcta de comparar dos `float`?
2. ¿Qué diferencia hay entre `int(39.9)` y `round(39.9)`?
3. Si hacés `b = a` con `a` una lista y después modificás `b`, ¿qué pasa con `a`? ¿Cómo se copia una lista de verdad?
4. ¿Por qué las claves de un diccionario tienen que ser inmutables (hashables)?
5. ¿Por qué buscar un elemento en un `set` es $O(1)$ y en una `list` es $O(n)$? Si necesito preguntar "¿está esto?" muchas veces, ¿qué estructura conviene?

## Preguntas que me quedaron
-
-

## Para la próxima clase
**[[02 - Programacion imperativa|Clase 2 — Programación imperativa]]:** condicionales, bucles, funciones propias y **recursión**. Con eso se pueden escribir algoritmos de verdad, no solo manipular datos.

## Actividad
Consigna en **`Actividad_Clase1.ipynb`** (aula de Moodle). Se entrega **antes de la clase 2**.
