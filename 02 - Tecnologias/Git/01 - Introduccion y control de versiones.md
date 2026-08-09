---
titulo: Git - Introducción y control de versiones
materia: Git
tipo: apunte
tags:
  - git
  - tecnologias
  - tema/introduccion
fuente: "Pro Git Book, cap. 1 (git-scm.com/book); Git Reference Manual (git-scm.com/docs)"
---

# Git - Introducción y control de versiones

## ¿Qué problema resuelve?

Trabajar en un proyecto sin ningún sistema de control implica guardar copias manuales ("informe_final_v2_definitivo.py") cada vez que se quiere preservar un estado, sin poder saber con certeza qué cambió entre una versión y otra, ni volver atrás de forma confiable si algo se rompe. Un **sistema de control de versiones (VCS)** resuelve exactamente eso.

> [!definition] Sistema de control de versiones (VCS)
> "A system that records changes to a file or set of files over time so that you can recall specific versions later." Permite volver atrás a versiones anteriores (de un archivo o del proyecto entero), comparar cambios a lo largo del tiempo, ver quién modificó algo por última vez y cuándo se introdujo un problema, y recuperarse si algo se rompe o se pierden archivos. *Fuente: Pro Git Book, cap. 1.1.*

## Centralizado vs. distribuido: por qué Git es distribuido

Antes de Git, los VCS más usados eran **centralizados** (CVS, Subversion, Perforce): un único servidor guarda todo el historial versionado, y cada persona descarga (*checkout*) solo el estado actual de los archivos.

> [!warning] El problema del sistema centralizado
> "The most obvious downside is the single point of failure that the centralized server represents. If that server goes down for an hour, then during that hour nobody can collaborate at all [...] If the hard disk the central database is on becomes corrupted, and proper backups haven't been kept, you lose absolutely everything." *Fuente: Pro Git Book, cap. 1.1.*

Git es un VCS **distribuido (DVCS)**: cada persona que clona el repositorio no descarga solo el estado actual, sino una copia completa de **todo** el historial.

> [!important] Cada clon es un respaldo completo
> "Clients don't just check out the latest snapshot of the files; rather, they fully mirror the repository, including its full history. [...] Every clone is really a full backup of all the data." Si el servidor central se cae, cualquier clon local alcanza para restaurarlo por completo. *Fuente: Pro Git Book, cap. 1.1.*

Esto también habilita algo que un sistema centralizado no permite con la misma naturalidad: trabajar con **varios repositorios remotos a la vez** y flujos de colaboración más flexibles (por ejemplo, el modelo de fork que usa GitHub — ver [[01 - Introduccion y repositorios]] de GitHub).

## El modelo mental: snapshots, no diffs

> [!definition] La diferencia central con otros VCS
> La mayoría de los sistemas de control de versiones anteriores a Git piensan sus datos como una lista de cambios por archivo — un modelo llamado *delta-based version control*: guardan un archivo base y una serie de diferencias (parches) acumuladas sobre ese archivo. **Git piensa sus datos como una serie de fotografías (snapshots)** de todo el proyecto: cada vez que se hace un commit, Git guarda cómo se ven **todos** los archivos en ese momento, no solo qué cambió. *Fuente: Pro Git Book, cap. 1.3, "Snapshots, Not Differences".*

Esto no significa que Git duplique cada archivo en cada commit, aunque no haya cambiado:

> [!tip] La optimización que hace esto viable
> "To be efficient, if files have not changed, Git doesn't store the file again, just a link to the previous identical file it has already stored." Cada commit es, entonces, un snapshot del árbol completo del proyecto — pero los archivos sin cambios son solo un puntero al contenido ya guardado, no una copia nueva. *Fuente: Pro Git Book, cap. 1.3.*

Este modelo es la razón por la que el Pro Git Book describe a Git más como "a mini filesystem with some incredibly powerful tools built on top of it" que como un VCS tradicional — casi todas las particularidades de Git (lo liviano de las ramas, la velocidad, la forma de resolver conflictos) se derivan de este modelo de snapshots.

## Configuración inicial (obligatoria antes del primer commit)

Cada commit en Git queda firmado con un nombre y un email. Configurarlos es lo primero que hay que hacer al instalar Git:

```bash
git config --global user.name "Nicolás"
git config --global user.email "nicolas@ejemplo.com"

# Verificar la configuración
git config --list
```

`--global` aplica la configuración a **todos** los repositorios del usuario en esa máquina; se puede sobreescribir por proyecto corriendo el mismo comando sin `--global` estando dentro de ese repo. Hay tres niveles de configuración, y el más específico gana: `--local` (solo ese repo) > `--global` (todos los repos del usuario) > `--system` (toda la máquina). *Fuente: Pro Git Book, "First-Time Git Setup".*

> [!note] Nombre de la rama por defecto
> Desde Git 2.28, se puede elegir el nombre de la rama inicial (históricamente `master`; hoy la convención más común es `main`) con `git config --global init.defaultBranch main`.

## `git init`: crear un repositorio

```bash
git init
```

> [!definition] Qué hace exactamente
> "This command creates an empty Git repository — basically a `.git` directory with subdirectories for `objects`, `refs/heads`, `refs/tags`, and template files. An initial branch without any commits will be created." *Fuente: Git Reference, `git-init`.*

Esa carpeta oculta `.git/` es, literalmente, todo el repositorio: contiene el historial completo, la configuración y los objetos versionados. Borrarla equivale a borrar el historial de Git del proyecto (los archivos de trabajo quedan intactos, pero dejan de estar versionados).

## Relacionado
- [[02 - El flujo basico (working directory, staging area, repositorio)]]
- [[04 - Ramas y fusion (branching y merge)]]
- [[05 - Repositorios remotos (clone, push, pull, fetch)]]
- [[01 - Introduccion y repositorios]]
