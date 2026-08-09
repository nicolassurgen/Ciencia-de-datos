---
titulo: Git - El flujo básico (working directory, staging area, repositorio)
materia: Git
tipo: apunte
tags:
  - git
  - tecnologias
  - tema/flujo-basico
fuente: "Pro Git Book, cap. 2 (git-scm.com/book); Git Reference Manual (git-scm.com/docs)"
---

# Git - El flujo básico (working directory, staging area, repositorio)

## El problema: "guardar todo" no es lo mismo que "guardar lo que importa"

Cuando se modifican varios archivos a la vez, casi nunca conviene meter **todos** los cambios en un mismo commit — mezclar una corrección de un bug con un experimento a medio hacer hace que el historial sea difícil de leer y de revertir selectivamente. Git resuelve esto con un paso intermedio, explícito, entre "modificar un archivo" y "guardarlo permanentemente": el **staging area**.

## Los tres estados de un archivo

> [!definition] Modified, staged, committed
> "Git has three main states that your files can reside in: modified, staged, and committed. **Modified** means that you have changed the file but have not committed it to your database yet. **Staged** means that you have marked a modified file in its current version to go into your next commit snapshot. **Committed** means that the data is safely stored in your local database." *Fuente: Pro Git Book, "What is Git?".*

Esto se corresponde con las **tres áreas** de un proyecto Git:

| Área | Qué es |
|---|---|
| **Working tree** (working directory) | Los archivos tal como están en el disco, extraídos de la base de datos de Git para poder editarlos. |
| **Staging area** (también llamada *index*) | Un archivo interno (dentro de `.git/`) que registra qué va a entrar en el próximo commit. |
| **Git directory** (`.git/`) | Donde vive el historial completo — lo que se copia entero al clonar. |

> [!important] El flujo básico, en tres pasos
> "1. You modify files in your working tree. 2. You selectively stage just those changes you want to be part of your next commit [...] 3. You do a commit, which takes the files as they are in the staging area and stores that snapshot permanently to your Git directory." *Fuente: Pro Git Book, "What is Git?".*

## Una sesión real, paso a paso

```bash
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
nothing to commit, working tree clean
```

Se crea un archivo nuevo:

```bash
$ echo 'Mi Proyecto' > README
$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)

    README

nothing added to commit but untracked files present (use "git add" to track)
```

`git add` lo pasa al staging area:

```bash
$ git add README
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)

    new file:   README
```

`git commit` lo guarda permanentemente:

```bash
$ git commit -m "Story 182: fix benchmarks for speed"
[master 463dc4f] Story 182: fix benchmarks for speed
 2 files changed, 2 insertions(+)
 create mode 100644 README
```

La salida de `commit` resume qué pasó: en qué rama se commiteó (`master`), el hash del commit (`463dc4f`), y estadísticas de archivos/líneas modificadas. *Ejemplos citados de Pro Git Book, "Recording Changes to the Repository".*

> [!tip] `git add` fija el contenido en ese momento exacto
> "Git stages a file exactly as it is when you run the `git add` command." Si se edita el archivo **después** de haber hecho `git add`, hay que volver a correr `git add` para que ese cambio nuevo también quede en el staging area — de lo contrario, el commit va a incluir la versión anterior, no la última editada.

### `git status -s`: el formato corto

```bash
$ git status -s
 M README
MM Rakefile
A  lib/git.rb
M  lib/simplegit.rb
?? LICENSE.txt
```

> [!note] Cómo leer las dos columnas
> "New files that aren't tracked have a `??` next to them, new files that have been added to the staging area have an `A`, modified files have an `M`... There are two columns to the output — the left-hand column indicates the status of the staging area and the right-hand column indicates the status of the working tree." Por eso `Rakefile` con `MM` significa: modificado, agregado al staging, y modificado **otra vez** después de eso. *Fuente: Pro Git Book, "Recording Changes to the Repository".*

## `git diff` vs. `git diff --staged`

Esta es una de las distinciones que más confunde al empezar:

- **`git diff`** (sin argumentos): compara el **working tree** contra el **staging area**. Muestra los cambios que **todavía no** se agregaron con `git add`.
- **`git diff --staged`** (equivalente: `--cached`): compara el **staging area** contra el **último commit**. Muestra qué va a entrar exactamente en el próximo commit.

> [!warning] `git diff` no muestra "todo lo que cambió desde el último commit"
> "It's important to note that `git diff` by itself doesn't show all changes made since your last commit — only changes that are still unstaged. If you've staged all of your changes, `git diff` will give you no output." Si `git diff` no muestra nada pero sí se hicieron cambios, es porque ya están en el staging area — hay que usar `git diff --staged` para verlos. *Fuente: Pro Git Book, "Recording Changes to the Repository".*

## `.gitignore`: qué no versionar

No todo archivo de una carpeta de proyecto debería estar bajo control de versiones: archivos generados automáticamente, entornos virtuales, credenciales, cachés — versionarlos infla el repositorio y puede filtrar información sensible.

> [!definition] `.gitignore`
> "A gitignore file specifies intentionally untracked files that Git should ignore. Files already tracked by Git are not affected." *Fuente: Git Reference, `gitignore`.*

Sintaxis básica de patrones:

```gitignore
# Comentario (con # al inicio de línea)
hello.*          # matches hello.txt, hello.c, ...
/hello.*         # solo en la carpeta raíz
foo/             # ignora la carpeta foo y todo su contenido
*.pyc            # cualquier archivo compilado de Python
__pycache__/
.venv/
.env             # credenciales / variables de entorno

# Negación: excluir un caso puntual de una regla anterior
*.html
!foo.html        # foo.html SÍ se versiona, a pesar de la regla de arriba
```

`*` matchea cualquier cosa excepto `/`; `?` matchea un solo carácter; una barra al final (`foo/`) hace que el patrón matchee solo carpetas. *Sintaxis confirmada en Git Reference, `gitignore`.*

> [!important] `.gitignore` no afecta archivos que ya están versionados
> Si un archivo ya fue agregado con `git add`/`git commit` antes de escribir la regla en `.gitignore`, Git lo sigue siguiendo (*tracking*) igual — hay que sacarlo explícitamente del repositorio (`git rm --cached <archivo>`) para que la regla empiece a aplicar.

## Relacionado
- [[01 - Introduccion y control de versiones]]
- [[03 - Historial y deshacer cambios]]
- [[04 - Ramas y fusion (branching y merge)]]
