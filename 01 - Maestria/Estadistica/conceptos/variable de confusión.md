---
titulo: Variable de confusión
materia: Estadística
tipo: concepto
tags:
  - estadistica
  - maestria
  - concepto
  - tema/introduccion
fecha: 2026-08-03
---

# Variable de confusión

> [!definition] Variable de confusión (confounding variable)
> Un factor **distinto** del que se quiere estudiar, que **varía a la par** de él y que también podría explicar el efecto observado. Cuando existe, no se puede separar el efecto del factor de interés del efecto de la variable de confusión: están **"confundidos"**.

## Ejemplo de la clase

Una empresa fabrica el mismo producto en dos plantas de **localidades distintas**. Usa materia prima del proveedor **A en una planta** y del **B en la otra**, y compara la calidad resultante.

¿Puede concluir que un proveedor es mejor que el otro? **No limpiamente**: la localidad, la maquinaria, el personal y otros factores propios de cada planta están **confundidos** con el proveedor. Si la calidad difiere, podría deberse a la planta, no a la materia prima.

![[Variable de confusion.png]]

## Cómo se evita

- **Aleatorización**: asignar los tratamientos (p. ej. el proveedor) al azar entre las unidades, para que la variable sospechosa (la planta) se reparta parejo entre condiciones.
- **Bloqueo / [[estratificación]]**: comparar dentro de cada nivel de la variable sospechosa (p. ej. comparar A vs. B **dentro de cada planta**) y no entre plantas.
- **Diseño experimental controlado**: ver [[diseño de experimentos]].

## Por qué importa

Una variable de confusión no detectada es la causa más común de perder [[validez interna]]: la comparación "se ve" concluyente pero no lo es, porque el factor de interés viaja pegado a otra explicación posible.

> [!note] En código
> `sns.lmplot()` en Seaborn (ver [[07 - Regresion y relaciones estadisticas]]) dibuja una recta de regresión prolija entre dos variables — pero **no** protege de esto: una relación aparente puede deberse a una variable de confusión que ni siquiera está en el gráfico. Comparar dentro de cada estrato con `hue=`/`col=` ([[08 - Grids y comparaciones multiples]]) es la forma visual de chequearlo.

> [!info] A futuro: controlarla en un modelo
> La forma numérica (no solo visual) de manejar esto es agregar la variable sospechosa **como predictora adicional** en un modelo de regresión múltiple: `smf.ols('calidad ~ proveedor + planta', data=df)` estima el efecto de `proveedor` *ya teniendo en cuenta* `planta`, en vez de mezclar ambos efectos. Ver [[02 - Regresion lineal (OLS y WLS)]] de statsmodels — la fórmula matricial exacta que resuelve `.ols()` está desarrollada en [[02 - Matrices]] de Matemática.
>
> Caso real citado en la bibliografía: al predecir el precio de venta de casas a partir solo de los metros cuadrados, **omitir el código postal** (una variable de confusión enorme en el mercado inmobiliario: la ubicación afecta tanto el tamaño típico de la casa como su precio) produce coeficientes contraintuitivos y difíciles de interpretar. Agregar el código postal al modelo es exactamente el mecanismo de "controlar" descripto arriba. *Fuente: [[Practical Statistics for Data Scientists]] (Bruce & Bruce), cap. 4.*

## Relacionado
- [[causalidad vs asociación]]
- [[01 - Como dar sentido a los datos]]
- [[validez interna]]
- [[diseño de experimentos]]
- [[estratificación]]
- [[07 - Regresion y relaciones estadisticas]]
- [[02 - Regresion lineal (OLS y WLS)]]
