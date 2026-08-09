---
titulo: GitHub - Forks y Pull Requests
materia: GitHub
tipo: apunte
tags:
  - github
  - tecnologias
  - tema/colaboracion
fuente: "GitHub Docs (docs.github.com)"
---

# GitHub - Forks y Pull Requests

## ¿Qué problema resuelve?

Contribuir a un proyecto ajeno (una librería open source, por ejemplo) plantea un problema: nadie le da permiso de escritura directo sobre su repositorio a cualquier desconocido de internet. GitHub resuelve esto con dos piezas que trabajan juntas: el **fork** (una copia propia del repositorio, donde sí se puede escribir) y el **Pull Request** (la propuesta formal de traer esos cambios de vuelta al original).

## Fork: una copia conectada al original

> [!definition] Fork
> "Forks are repositories that start as copies of another repository, called the upstream repository. A fork has its own settings and permissions but stays connected to the upstream repository." *Fuente: GitHub Docs, "About forks".*

> [!important] Fork ≠ Branch
> La propia documentación lo aclara explícitamente: "a branch is part of one repository. A fork is a separate repository with its own settings and collaboration space." Una rama vive dentro del mismo repositorio; un fork es un repositorio **completo e independiente**, con sus propios issues, PRs, Actions — que además mantiene la referencia a su repositorio de origen (*upstream*).

> [!tip] Fork vs. Clone
> `git clone` siempre baja una copia local a la computadora, sin importar el nivel de permisos que se tenga. **Forkear** es el paso adicional — crear una copia propia en GitHub.com — que solo hace falta cuando **no** se tiene permiso de escritura directo sobre el repositorio original, para tener un espacio propio desde el cual abrir un Pull Request.

## El flujo de contribución, paso a paso

1. **Fork** del repositorio (botón "Fork" en la interfaz web de GitHub).
2. **Clonar el fork** a la computadora:
   ```bash
   git clone https://github.com/TU-USUARIO/proyecto.git
   ```
3. **Configurar el remoto `upstream`**, apuntando al repositorio original (para poder sincronizar después):
   ```bash
   git remote add upstream https://github.com/DUEÑO-ORIGINAL/proyecto.git
   git remote -v
   ```
4. **Crear una rama** para el cambio propuesto (ver [[04 - Ramas y fusion (branching y merge)]] de Git):
   ```bash
   git switch -c mi-mejora
   ```
5. Hacer los cambios, `git commit`, `git push` a **la propia rama del fork**.
6. **Abrir el Pull Request**, desde la rama del fork hacia el repositorio original: "If you want to contribute back to the upstream repository, you can submit a pull request to ask the original author to pull your fork into their repository." *Fuente: GitHub Docs, "Fork a repo".*

## Pull Request: la unidad de colaboración de GitHub

> [!definition] Pull Request (PR)
> "Pull requests are proposals to merge code changes into a project" — GitHub lo describe como su "key collaboration feature, letting you discuss and review changes before merging them." *Fuente: GitHub Docs, "About pull requests".*

Un PR se organiza en pestañas: **Conversation** (descripción y comentarios), **Commits**, **Checks** (tests/builds automáticos — ver [[04 - GitHub Actions y CI-CD basico]]), y **Files changed** (el diff completo para revisar).

> [!note] Draft Pull Requests
> "Draft pull requests cannot be merged, and code owners are not automatically requested to review them. Drafts are useful when you want to share work-in-progress without formally requesting reviews." Útiles para mostrar avance sin pedir todavía una revisión formal.

## Code review

Quien revisa un PR puede dejar tres tipos de review:

| Tipo | Qué significa |
|---|---|
| **Comment** | Feedback general, sin aprobar ni pedir cambios explícitamente |
| **Approve** | "Signals that the changes are ready to merge" |
| **Request changes** | "Flags feedback that the author should address before merging" |

Los comentarios pueden dejarse línea por línea sobre el diff, y quedan registrados en el timeline del PR. *Fuente: GitHub Docs, "About pull request reviews".*

## Las tres formas de mergear un PR

| Opción | Qué le pasa al historial |
|---|---|
| **Merge commit** | Se agregan **todos** los commits de la rama del PR a la rama base, más un commit de merge que marca el punto de integración — "your team values complete history". |
| **Squash and merge** | Todos los commits del PR se aplastan en **uno solo** sobre la rama base — "a pull request represents one logical change", ideal si hubo muchos commits intermedios de tipo WIP. |
| **Rebase and merge** | Cada commit del PR se agrega **individualmente** sobre la rama base, sin commit de merge — historial lineal, "your team wants a linear history". |

*Definiciones citadas de GitHub Docs, "About pull request merges".*

## Mantener el fork actualizado

Con el tiempo, el repositorio original avanza y el fork queda desactualizado. Vía terminal (una vez configurado el remoto `upstream` del paso 3):

```bash
git fetch upstream
git switch main
git merge upstream/main
git push origin main    # el merge local no actualiza el fork en GitHub.com por sí solo
```

> [!warning] El merge local no alcanza
> "Syncing your fork only updates your local copy of the repository. To update your fork on GitHub.com, you must push your changes." Si aparecen conflictos al sincronizar, GitHub sugiere resolverlos mediante un Pull Request. *Fuente: GitHub Docs, "Syncing a fork".*

## Relacionado
- [[01 - Introduccion y repositorios]]
- [[04 - Ramas y fusion (branching y merge)]]
- [[05 - Repositorios remotos (clone, push, pull, fetch)]]
- [[03 - Issues y gestion de proyectos]]
