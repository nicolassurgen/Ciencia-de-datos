---
titulo: Validez interna
materia: Estadística
tipo: concepto
tags:
  - estadistica
  - maestria
  - concepto
  - tema/introduccion
fecha: 2026-08-03
---

# Validez interna

> [!definition] Validez interna
> Grado en el que las **comparaciones** hechas dentro de una investigación **no están sesgadas**: la diferencia observada entre grupos puede atribuirse realmente al factor de interés, y no a otra cosa que varía junto con él.

## El problema típico: variables confundidas

La amenaza más común a la validez interna es la [[variable de confusión]]: un factor extra que varía **al mismo tiempo** que el factor que se quiere estudiar, de modo que no se puede separar el efecto de uno del otro.

> [!example] Caso clásico
> Una empresa fabrica el mismo producto en dos plantas de **localidades distintas**. Usa materia prima del proveedor **A en una planta** y del **B en la otra**, y compara la calidad resultante. ¿Puede concluir que un proveedor es mejor? **No limpiamente**: la localidad, la maquinaria y otros factores están **confundidos** con el proveedor. La diferencia observada podría deberse a la planta, no a la materia prima.

## Cómo se protege la validez interna

- **[[diseño de experimentos|Diseño experimental]]**: asignar tratamientos de forma controlada (idealmente aleatoria) en vez de comparar grupos que ya diferían de antemano.
- **Aleatorización**: repartir al azar las unidades entre condiciones, para que los factores no controlados se distribuyan parejo entre grupos.
- **Bloqueo / [[estratificación]]**: agrupar unidades similares antes de comparar, para que la variabilidad "de fondo" no contamine la comparación de interés.

## Validez interna vs. validez externa

| | Pregunta que responde |
|---|---|
| **Validez interna** | Dentro del estudio, ¿la comparación es limpia? |
| **[[validez externa]]** | ¿Puedo extender esta conclusión a otro grupo o a toda la población? |

Un estudio con alta validez interna (buena comparación) puede tener baja validez externa (muestra no representativa), y viceversa: son problemas distintos que se evalúan por separado.

## Relacionado
- [[01 - Como dar sentido a los datos]]
- [[variable de confusión]]
- [[diseño de experimentos]]
- [[validez externa]]
