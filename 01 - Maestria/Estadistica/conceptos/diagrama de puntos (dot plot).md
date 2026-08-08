---
titulo: Diagrama de puntos (dot plot)
materia: Estadística
tipo: concepto
tags:
  - estadistica
  - maestria
  - concepto
  - tema/variabilidad
fecha: 2026-08-08
---

# Diagrama de puntos (dot plot)

Con pocos datos, agrupar en intervalos (como hace un [[histograma]]) puede ser contraproducente: agrupar 8 o 10 valores en clases pierde casi toda la información individual que hay para mostrar. Hace falta un gráfico que muestre cada dato **sin agrupar y sin perderlo**, pero que siga comunicando la forma de la distribución de un vistazo — eso es lo que resuelve el diagrama de puntos.

> [!definition] Diagrama de puntos (dot plot)
> Gráfico para una variable **cuantitativa** que representa **cada dato individual** como un punto sobre una recta numérica. Cuando varios datos comparten (o casi comparten) el mismo valor, los puntos se apilan uno encima del otro en esa posición, formando columnas cuya altura muestra cuántas veces se repite (o casi se repite) ese valor.

## Cómo leerlo

```
Diámetro (mm):
       •
       •   •
   •   •   •
   •   •   •   •
---+---+---+---+---+---
  98  99  100 101 102
```

Cada columna de puntos apilados funciona como una barra de [[histograma]] informal, pero sin haber definido intervalos de clase: la posición horizontal de cada punto **es** el valor real del dato, no una clase que lo agrupa con otros.

## Cuándo usarlo

Es la herramienta natural para conjuntos de datos **chicos** (unas pocas decenas de observaciones como mucho): con muchos datos, los puntos se amontonan y el gráfico deja de ser legible, momento en el que conviene pasar a un [[histograma]] (que agrupa) o a un [[diagrama de tallo y hoja]] (que conserva el detalle agrupando por dígitos). Es habitual, por ejemplo, para comparar dos muestras chicas una al lado de la otra sobre el mismo eje — dos columnas de puntos permiten ver a simple vista si difieren en centro, en dispersión, o en ambos.

> [!tip] Puente con la clase
> El caso de los diámetros de piezas de la Máquina 1 y la Máquina 2 en [[02 - El estudio de la variabilidad|la clase 2]] se presentó justamente como un dot plot: dos columnas de puntos, una por máquina, comparadas sobre el mismo eje de diámetro — la forma más directa de ver a ojo si una máquina produce piezas más dispersas o más centradas que la otra, antes incluso de calcular ninguna medida de resumen.

## Relación con otros gráficos

| Gráfico | Agrupa los datos | Conserva el valor exacto |
|---|:---:|:---:|
| Diagrama de puntos | No | Sí |
| [[diagrama de tallo y hoja]] | Parcialmente (por dígito) | Sí |
| [[histograma]] | Sí (intervalos de clase) | No |

> [!note] En código
> `sns.stripplot(data=df, x="grupo", y="valor")` o `sns.swarmplot(...)` en Seaborn (ver [[04 - Relaciones entre variables (scatterplot, lineplot)]]) son las versiones modernas del dot plot, con un algoritmo que separa los puntos horizontalmente para que no se superpongan al apilarse. `plt.plot(x, np.zeros_like(x), 'o')` en Matplotlib da la versión más literal y de bajo nivel.

## Relacionado
- [[02 - El estudio de la variabilidad]]
- [[histograma]]
- [[diagrama de tallo y hoja]]
- [[distribución de frecuencias]]
- [[04 - Relaciones entre variables (scatterplot, lineplot)]]
