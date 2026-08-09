---
titulo: Git - Historial y deshacer cambios
materia: Git
tipo: apunte
tags:
  - git
  - tecnologias
  - tema/historial
fuente: "Pro Git Book, cap. 2 y cap. 7 (git-scm.com/book); Git Reference Manual (git-scm.com/docs)"
---

# Git - Historial y deshacer cambios

## Ver el historial: `git log` y `git show`

```bash
git log --oneline              # una línea por commit (hash corto + mensaje)
git log --graph --all          # dibuja el árbol de ramas en texto
git log -p                     # muestra el diff completo de cada commit
git log --stat                 # resumen de archivos y líneas +/- por commit, sin el diff completo
```

- `--oneline` es un atajo de `--pretty=oneline --abbrev-commit`.
- `--graph` "draw[s] a text-based graphical representation of the commit history on the left hand side of the output".
- `--all` muestra el historial de **todas** las ramas, no solo la actual.
- `-p`/`--patch` agrega el diff de cada commit; `--stat` agrega solo el resumen (nombres de archivo + líneas modificadas). *Fuente: Git Reference, `git-log`.*

`git show <commit>` muestra el mensaje y el diff completo de un commit puntual — el equivalente a un `git log -p` de un solo commit:

```bash
git show a1b2c3d
```

## Deshacer cambios: el árbol de decisión

Git separa "deshacer" en varias herramientas distintas según **qué** se quiere deshacer y **dónde** está el cambio. Mezclarlas es la fuente más común de confusión al empezar.

> [!important] Los tres comandos, según la documentación oficial
> "**git-revert** is about making a new commit that reverts the changes made by other commits. **git-restore** is about restoring files in the working tree from either the index or another commit. This command does not update your branch. **git-reset** is about updating your branch, moving the tip in order to add or remove commits from the branch." *Fuente: Git Reference, página `git`.*

### Descartar cambios sin commitear: `git restore`

```bash
git restore archivo.py             # descarta cambios en el working tree (vuelve a la última versión commiteada/staged)
git restore --staged archivo.py    # saca el archivo del staging area, sin tocar el working tree
```

> [!danger] `git restore <archivo>` es irreversible
> "Any local changes you made to that file are gone — Git just replaced that file with the last staged or committed version. Don't ever use this command unless you absolutely know that you don't want those unsaved local changes." *Fuente: Pro Git Book, "Undoing Things".*

`git restore` (Git 2.23+) es la versión moderna y más clara de dos usos que antes se hacían con comandos más confusos y sobrecargados: `git checkout -- <archivo>` (descartar cambios) y `git reset HEAD <archivo>` (sacar del staging). Ambos siguen funcionando, pero `restore` separa mejor la intención.

### Modificar el último commit: `git commit --amend`

```bash
git add archivo_olvidado.py
git commit --amend
```

> [!warning] `--amend` no "corrige", reemplaza
> "It's important to understand that when you're amending your last commit, you're not so much fixing it as replacing it entirely with a new, improved commit [...] Effectively, it's as if the previous commit never happened." Por eso: **solo** en commits que todavía no se subieron a un remoto compartido — amendear y forzar un push sobre un commit que otros ya descargaron les genera conflictos. *Fuente: Pro Git Book, "Undoing Things".*

### `git reset --soft / --mixed / --hard`: mover HEAD, con distinto alcance

`git reset` mueve el puntero de la rama actual a otro commit, y decide hasta dónde "arrastra" ese movimiento sobre el staging area y el working directory:

| Modo | HEAD (rama) | Staging area | Working directory | ¿Es seguro? |
|---|:---:|:---:|:---:|:---:|
| `--soft` | se mueve | **no se toca** | **no se toca** | Sí |
| `--mixed` (default) | se mueve | se actualiza para igualar el nuevo HEAD | **no se toca** | Sí |
| `--hard` | se mueve | se actualiza | se sobrescribe para igualar el nuevo HEAD | **No** |

> [!danger] `--hard` es de los pocos comandos de Git que destruye datos de verdad
> "It's important to note that this flag is the only way to make the `reset` command dangerous, and one of the very few cases where Git will actually destroy data. Any other invocation of `reset` can be pretty easily undone." Si el cambio perdido nunca se commiteó, `--hard` lo borra sin posibilidad de recuperarlo. *Fuente: Pro Git Book, "Reset Demystified".*

Ejemplo oficial de uso legítimo de `--soft`: unir los últimos 3 commits en uno solo, sin perder ningún cambio:

```bash
git reset --soft HEAD~3
git commit -m "Un único commit que resume los 3 anteriores"
```

Ejemplo de `reset` sobre un **archivo puntual** (equivalente a `git restore --staged`): al pasarle un path, `reset` no puede mover HEAD parcialmente, así que solo actúa como un "unstage":

```bash
git reset archivo.py    # atajo de: git reset --mixed HEAD archivo.py -> saca del staging, sin tocar el working directory
```

### `git revert`: deshacer un commit ya publicado, sin reescribir historial

```bash
git revert HEAD~3       # crea un commit NUEVO que revierte el efecto del commit indicado
```

> [!important] `revert` vs. `reset`: la diferencia que importa en equipo
> `reset` mueve la rama hacia atrás — **reescribe** el historial. `revert` deja el historial intacto y agrega un commit nuevo que deshace los cambios. La documentación aclara: "If you want to throw away all uncommitted changes in your working directory, you should see git-reset [...] If you want to extract specific files as they were in another commit, you should see git-restore." *Fuente: Git Reference, `git-revert`.*
>
> **Regla práctica**: en commits que son solo locales (nunca se subieron), `reset --hard`/`--amend` son seguros. En una rama **ya publicada** que otros pueden haber descargado, la única forma segura de deshacer es `revert` — porque no borra ni reescribe nada que otros ya tengan, solo agrega un commit nuevo. Reescribir historial compartido (con `reset --hard` + push forzado, o `rebase`) obliga a los demás a re-mergear su trabajo y ensucia el historial con commits duplicados.

## Relacionado
- [[02 - El flujo basico (working directory, staging area, repositorio)]]
- [[04 - Ramas y fusion (branching y merge)]]
- [[05 - Repositorios remotos (clone, push, pull, fetch)]]
