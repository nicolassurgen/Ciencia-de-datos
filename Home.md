---
titulo: Home
tipo: home
tags:
  - home
---

# 🏠 Home

Punto de entrada al vault. Desde acá se llega a las cuatro áreas y se puede ver, con [[#📊 Resumen|Dataview]], el estado general de las notas sin tener que navegar carpeta por carpeta.

## 📚 Áreas

**Maestría**
- 📐 **Matemática**
	- [[01 - Vectores]] · [[02 - Matrices]] · [[03 - Transformaciones lineales]]
	- [[01 - Funciones]] · [[02 - Derivadas]] · [[03 - Optimizacion]]
- 📊 **Estadística**
	- [[01 - Como dar sentido a los datos]]
	- [[02 - El estudio de la variabilidad]]
- 🐍 **Algoritmos**
	- [[01 - Introduccion a la programacion]]

**Tecnologías**
- 🐳 **Docker**
	- [[01 - Introduccion]] · [[02 - Imagen]] · [[03 - Contenedor]] · [[04 - Dockerfile]] · [[05 - DockerHub]]
- 🔀 **Git**
	- [[01 - Introduccion y control de versiones]] (índice del recorrido completo)
- 🐙 **GitHub**
	- [[01 - Introduccion y repositorios]] (índice del recorrido completo)
- 📈 **Matplotlib**
	- [[01 - Introduccion y primer grafico]] (índice del recorrido completo)
- 🔢 **NumPy**
	- [[01 - Introduccion y arrays]] (índice del recorrido completo)
- 🐼 **Pandas**
	- [[01 - Introduccion a Series y DataFrame]] (índice del recorrido completo)
- 🎨 **Seaborn**
	- [[01 - Introduccion a Seaborn]] (índice del recorrido completo)
- 🧪 **SciPy**
	- [[01 - Introduccion a SciPy.stats]] (índice del recorrido completo)
- 📉 **statsmodels**
	- [[01 - Introduccion a statsmodels]] (índice del recorrido completo)

---

## 📊 Resumen

Cantidad de notas por materia y tipo:

```dataview
TABLE WITHOUT ID
	materia AS "Materia",
	length(filter(rows, (r) => r.tipo = "apunte")) AS "Apuntes",
	length(filter(rows, (r) => r.tipo = "concepto")) AS "Conceptos",
	length(rows) AS "Total"
FROM ""
WHERE materia
GROUP BY materia
SORT materia ASC
```

## 📖 Apuntes de clase

```dataview
TABLE materia AS "Materia", clase AS "Clase", fecha AS "Fecha"
FROM ""
WHERE tipo = "apunte"
SORT materia ASC, fecha ASC
```

## 🧩 Conceptos por materia

```dataview
LIST rows.file.link
FROM ""
WHERE tipo = "concepto"
GROUP BY materia
SORT materia ASC
```

## 🕳️ Notas sin materia asignada

Notas que no tienen frontmatter con `materia` (candidatas a revisar o estandarizar):

```dataview
LIST
FROM ""
WHERE !materia AND file.name != "Home"
```
