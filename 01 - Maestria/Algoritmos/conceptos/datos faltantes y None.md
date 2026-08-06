---
titulo: Datos faltantes y None
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

# Datos faltantes y None

> [!definition] `None`
> Valor especial de Python que representa **ausencia de información**: "acá no hay dato". No es `0`, no es texto vacío, no es `False` — es una categoría propia.

```python
print(None == 0)     # False -> None no es cero
print(None == "")    # False -> None no es texto vacío
print(sexo is None)  # True  -> forma recomendada de comparar (ver is vs ==)
```

## Por qué aparecen en datos reales

Un CSV real trae campos vacíos (`Adelie,Torgersen,,,,,`): mediciones que no se tomaron, respuestas en blanco, sensores que fallaron. Como **todo llega como texto** al leer un CSV, esos vacíos son cadenas `""`, no `None` todavía — hay que convertirlos explícitamente:

```python
def a_numero(texto):
    if texto == "":
        return None
    return float(texto)
```

> [!warning] Los faltantes rompen las conversiones
> `float("")` lanza `ValueError: could not convert string to float: ''`. Representar el faltante como `None` **antes** de intentar convertir es la forma honesta de manejarlo.

## La decisión que más importa: no tratarlos como cero

```python
# Contar faltantes
faltantes = sum(1 for p in pinguinos if p["masa_g"] is None)

# Promedio EXCLUYENDO faltantes (¡no tratarlos como 0!)
masas = [p["masa_g"] for p in pinguinos if p["masa_g"] is not None]
promedio = sum(masas) / len(masas)
```

> [!important] Decisión del analista, no de la herramienta
> Si se tratara a los faltantes como cero, el promedio bajaría **artificialmente**. Qué hacer con los faltantes (excluir, imputar, marcar) es una decisión del analista, no algo que la herramienta resuelve sola. Enlaza directamente con el [[tratamiento primario]] de Estadística.

## Puente con Tecnologías

El patrón de `if p["masa_g"] is not None` (filtrar a mano) es exactamente lo que reemplazan las máscaras booleanas de NumPy (ver [[06 - Comparaciones, mascaras y filtrado booleano]]) y `df.dropna()`/`df.fillna()` de Pandas (ver [[04 - Datos faltantes]]) — mismo problema, sin el loop explícito. Ahí `None` pasa a llamarse `NaN` dentro de una columna numérica.

## Relacionado
- [[01 - Introduccion a la programacion]]
- [[tipos primitivos en Python]]
- [[is vs == (identidad vs igualdad)]]
- [[tratamiento primario]]
- [[04 - Datos faltantes]]
- [[06 - Comparaciones, mascaras y filtrado booleano]]
