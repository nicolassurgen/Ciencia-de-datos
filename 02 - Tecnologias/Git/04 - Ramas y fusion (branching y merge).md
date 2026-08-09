---
titulo: Git - Ramas y fusión (branching y merge)
materia: Git
tipo: apunte
tags:
  - git
  - tecnologias
  - tema/ramas
fuente: "Pro Git Book, cap. 3 (git-scm.com/book); Git Reference Manual (git-scm.com/docs)"
---

# Git - Ramas y fusión (branching y merge)

## ¿Qué problema resuelve?

Probar una idea nueva, o trabajar en una funcionalidad que va a tardar varios commits en estar lista, sin arriesgar el código que ya funciona — eso es lo que resuelven las ramas: una línea de desarrollo independiente y paralela al resto.

## Una rama es solo un puntero

> [!definition] Rama
> "A branch in Git is simply a lightweight movable pointer to one of these commits." *Fuente: Pro Git Book, "Branches in a Nutshell".*

Esta es la idea más importante de todo el capítulo, porque explica por qué ramificar en Git es rápido y prácticamente gratis:

> [!important] Por qué crear una rama es instantáneo
> "Because a branch in Git is actually a simple file that contains the 40 character SHA-1 checksum of the commit it points to, branches are cheap to create and destroy. [...] This is in sharp contrast to the way most older VCS tools branch, which involves copying all of the project's files into a second directory." Por eso "Git encourages workflows that branch and merge often, even multiple times in a day." *Fuente: Pro Git Book, "Branches in a Nutshell".*

`HEAD` es otro puntero — no al commit directamente, sino a la **rama** en la que se está parado:

> [!note] `HEAD`
> "It keeps a special pointer called HEAD. [...] In Git, this is a pointer to the local branch you're currently on." Cuando se hace un commit nuevo, es la rama a la que apunta HEAD la que se mueve hacia adelante — HEAD "sigue" a la rama activa.

## Crear y cambiar de rama

```bash
git branch nueva-funcionalidad     # crea la rama (no cambia a ella)
git switch nueva-funcionalidad     # cambia a esa rama (comando moderno, dedicado a esto)
git switch -c otra-rama            # crear y cambiar en un solo paso

git branch -d nueva-funcionalidad  # borrar una rama ya fusionada
```

`git checkout` es el comando histórico y más "sobrecargado" (además de cambiar de rama, sirve para restaurar archivos, crear ramas con `-b`, etc.); `git switch` es la versión más nueva pensada exclusivamente para cambiar de rama, más clara de leer.

## Fusionar ramas: `git merge`

Hay dos formas en que Git puede fusionar una rama, según cómo divergió el historial.

### Fast-forward: cuando no hubo trabajo divergente

Si la rama activa no recibió ningún commit propio mientras la otra rama avanzaba, fusionar es trivial: Git simplemente **mueve el puntero hacia adelante**, sin crear ningún commit nuevo.

```bash
$ git checkout master
$ git merge hotfix
Updating f42c576..3a0874c
Fast-forward
 index.html | 2 ++
 1 file changed, 2 insertions(+)
```

> [!definition] Fast-forward
> "Because the commit pointed to by the branch you merged in was directly ahead of the commit you're on, Git simply moves the pointer forward [...] there is no divergent work to merge together — this is called a 'fast-forward.'" *Fuente: Pro Git Book, "Basic Branching and Merging".*

### Three-way merge: cuando ambas ramas avanzaron

Si mientras se trabajaba en una rama, la rama base **también** recibió commits nuevos, ya no hay un camino directo entre ambas — Git tiene que combinar el trabajo de las dos.

```bash
$ git checkout master
$ git merge iss53
Merge made by the 'recursive' strategy.
index.html |    1 +
1 file changed, 1 insertion(+)
```

> [!definition] Three-way merge
> "Because the commit on the branch you're on isn't a direct ancestor of the branch you're merging in, Git has to do some work. [...] Git does a simple three-way merge, using the two snapshots pointed to by the branch tips and the common ancestor of the two. [...] Git creates a new snapshot [...] and automatically creates a new commit that points to it. This is referred to as a merge commit, and is special in that it has more than one parent." *Fuente: Pro Git Book, "Basic Branching and Merging".*

## Conflictos de merge

Un conflicto ocurre cuando ambas ramas modificaron **las mismas líneas** del mismo archivo, y Git no puede decidir solo cuál versión conservar. Marca el tramo en conflicto directamente en el archivo:

```
<<<<<<< yours:sample.txt
Conflict resolution is hard;
let's go shopping.
=======
Git makes conflict resolution easy.
>>>>>>> theirs:sample.txt
```

> [!important] Cómo resolverlo
> "After seeing a conflict, you can [...] resolve the conflicts. Git will mark the conflicts in the working tree. Edit the files into shape and `git add` them to the index. Use `git commit` [...] to seal the deal." *Fuente: Git Reference, `git-merge`.* En la práctica: editar el archivo eliminando los marcadores y dejando el contenido final deseado → `git add <archivo>` → `git commit`.

## Una alternativa a merge: `git rebase` (mención)

`git rebase` integra los cambios de una rama en otra reescribiendo commits (en vez de crear un commit de merge con dos padres, "reubica" los commits de una rama sobre la punta de la otra, generando un historial lineal). No se desarrolla en profundidad acá, pero la advertencia oficial es importante:

> [!danger] La regla de oro del rebase
> "Do not rebase commits that exist outside your repository and that people may have based work on." Si se ignora: "your collaborators will have to re-merge their work and things will get messy." Regla práctica del propio libro: "rebase local changes before pushing to clean up your work, but never rebase anything that you've pushed somewhere." *Fuente: Pro Git Book, "Rebasing".*

## Relacionado
- [[01 - Introduccion y control de versiones]]
- [[03 - Historial y deshacer cambios]]
- [[05 - Repositorios remotos (clone, push, pull, fetch)]]
- [[02 - Forks y Pull Requests]]
