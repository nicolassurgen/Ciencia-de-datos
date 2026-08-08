---
titulo: Condicionales y evaluación de verdad
materia: Algoritmos
tipo: concepto
tags:
  - algoritmos
  - maestria
  - concepto
  - python
  - tema/condicionales
fecha: 2026-08-08
---

# Condicionales y evaluación de verdad

Un programa que ejecuta siempre las mismas instrucciones, en el mismo orden, sirve para calcular pero no para tomar decisiones. Clasificar un pingüino según su masa, o tratar distinto un dato que falta, exige que el resultado dependa de los datos de entrada. Esa dependencia es lo que resuelve un condicional.

> [!definition] Condicional
> Estructura que ejecuta un bloque de código **solo si** se cumple una condición (una expresión que evalúa a `True` o `False`). En Python el bloque se delimita con `:` y **sangría** — no con llaves `{ }` como en otros lenguajes; la indentación es sintaxis, no estética.

```python
masa = 3200

if masa > 4000:
    print("Esta línea está DENTRO del if")
print("Esta está AFUERA: se ejecuta siempre")
# Esta está AFUERA: se ejecuta siempre
```

## `if` / `elif` / `else`: se evalúan en orden, gana la primera verdadera

`elif` encadena condiciones adicionales. Python las revisa **en orden** y ejecuta **solo la primera** que da verdadera — el resto ni se mira.

```python
masa = 4500
if masa > 5000:
    categoria = "muy grande"
elif masa > 4000:
    categoria = "grande"
elif masa > 3500:
    categoria = "mediano"
else:
    categoria = "chico"
print(categoria)   # grande
```

> [!warning] El orden importa: un error clásico que no avisa
> Si las condiciones sobre un mismo rango se escriben de **menor a mayor**, la primera que se cumple "atrapa" el caso y las siguientes nunca se alcanzan:
> ```python
> masa = 5500   # debería dar "muy grande"
> if masa > 3500:
>     categoria = "mediano"      # 5500 > 3500 es True -> entra ACÁ y corta
> elif masa > 4000:
>     categoria = "grande"
> elif masa > 5000:
>     categoria = "muy grande"
> print(categoria)   # mediano  <- INCORRECTO, pero sin ningún error
> ```
> No lanza ninguna excepción: el programa corre y da un resultado mal. Son los errores más peligrosos, porque no se anuncian. **Regla práctica: encadenar condiciones sobre rangos siempre de la más restrictiva a la más general.**

## Condiciones compuestas

`and`, `or`, `not` combinan condiciones. `in` es una forma más legible de preguntar "¿es alguno de estos?":

```python
isla = "Dream"

if isla == "Dream" or isla == "Torgersen":
    print("Isla chica")

if isla in ["Dream", "Torgersen"]:   # mismo resultado, más legible
    print("Isla chica")
```

> [!tip] Evaluación de cortocircuito (*short-circuit*)
> En `a or b`, si `a` ya es verdadero, Python **ni siquiera evalúa** `b` — el resultado ya está decidido. Lo mismo con `a and b`: si `a` es falso, `b` no se evalúa. Esto no es solo una curiosidad de rendimiento: permite escribir a propósito código como `dato is not None and dato > 0`, donde el segundo chequeo (`dato > 0`) solo se ejecuta si el primero ya garantizó que `dato` no es `None` — evitando así un error si se intentara comparar `None > 0`. *Fuente: [[Python-for-Data-Analysis]], cap. 2.*

> [!note] Comparaciones encadenadas
> Python permite escribir `3500 < masa < 4500` como una sola expresión, equivalente a `3500 < masa and masa < 4500` pero más legible — sintaxis propia de Python, no universal en otros lenguajes. *Fuente: [[Python-for-Data-Analysis]], cap. 2.*

## La trampa del truthy/falsy

Dentro de un `if`, Python no exige literalmente `True`/`False`: convierte cualquier valor a un booleano implícito. Y varios valores "vacíos" cuentan como `False` aunque **no sean lo mismo que "falta el dato"**:

```python
masa_cero = 0.0
masa_faltante = None

print(bool(masa_cero))       # False  <- ¡pero el dato SÍ existe, vale 0!
print(bool(masa_faltante))   # False
print(bool(""))              # False  <- texto vacío
print(bool([]))              # False  <- lista vacía
print(bool(0))                # False  <- entero cero
```

> [!important] `if masa:` no distingue "falta el dato" de "el dato es cero"
> Si se escribe `if masa:` para preguntar "¿hay un valor?", un pingüino con masa real `0.0` (raro, pero posible en otras variables: temperatura, saldo, conteo) se trataría igual que uno sin dato. Eso puede cambiar una conclusión entera en un análisis. La forma correcta de preguntar por un faltante es explícita:
> ```python
> if masa is None:      # correcto: solo True cuando falta el dato
>     ...
> ```

> [!note] `pass`: un bloque que no hace nada, a propósito
> Como Python delimita bloques por sangría (no por llaves), un `if` no puede quedar con el cuerpo vacío — hace falta escribir algo. `pass` es una instrucción que literalmente no hace nada, y sirve para dejar un bloque "pendiente" mientras se decide qué va ahí, o para un caso que a propósito no requiere ninguna acción:
> ```python
> if masa is None:
>     pass   # todavía no se decidió qué hacer con este caso
> else:
>     procesar(masa)
> ```
> *Fuente: [[Python-for-Data-Analysis]], cap. 2.*

## Puente con Estadística

Esta distinción es la versión de código de una pregunta que la materia de Estadística plantea sobre el mismo problema: un valor `0` es un **dato válido** (una medición que dio cero), mientras que un faltante es la **ausencia** de medición — tratarlos igual (por ejemplo al promediar) distorsiona el análisis. Ver [[datos faltantes y None]] y el [[tratamiento primario]] de Estadística.

## Relacionado
- [[02 - Programacion imperativa]]
- [[datos faltantes y None]]
- [[is vs == (identidad vs igualdad)]]
- [[bucles for, while y el patron acumulador]]
