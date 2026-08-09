---
titulo: GitHub - Issues y gestión de proyectos
materia: GitHub
tipo: apunte
tags:
  - github
  - tecnologias
  - tema/gestion
fuente: "GitHub Docs (docs.github.com)"
---

# GitHub - Issues y gestión de proyectos

## Issues: la unidad de seguimiento de trabajo

> [!definition] Issue
> Herramienta para "track ideas, feedback, tasks, or bugs" — "quick to create, flexible, and can be used in many ways", pensada para planificar, discutir y trackear trabajo de forma colaborativa. *Fuente: GitHub Docs, "About issues".*

Un issue admite: título, descripción en Markdown, comentarios, asignados, **sub-issues** (para partir un trabajo grande en partes más chicas) y **dependencias** (relaciones de bloqueo entre issues).

## Labels: categorizar issues y PRs

Todo repositorio nuevo trae **9 labels por defecto**:

| Label | Para qué se usa |
|---|---|
| `bug` | "Indicates an unexpected problem or unintended behavior" |
| `documentation` | "Indicates a need for improvements or additions to documentation" |
| `duplicate` | "Indicates similar issues, pull requests, or discussions" |
| `enhancement` | "Indicates new feature requests" |
| `good first issue` | "Indicates a good issue for first-time contributors" |
| `help wanted` | "Indicates that a maintainer wants help on an issue or pull request" |
| `invalid` | "Indicates that an issue, pull request, or discussion is no longer relevant" |
| `question` | "Indicates that an issue, pull request, or discussion needs more information" |
| `wontfix` | "Indicates that work won't continue on an issue, pull request, or discussion" |

*Fuente: GitHub Docs, "Managing labels".* Se pueden editar, borrar o crear labels propias.

## Milestones: agrupar issues bajo un objetivo

> [!definition] Milestone
> Sirve para "track progress on groups of issues or pull requests in a repository". Se le asocian issues/PRs similares, se pueden filtrar por milestone, y GitHub muestra cuántos quedan abiertos vs. cerrados para visualizar el avance. *Fuente: GitHub Docs, "Using labels and milestones to track work".*

Borrar un milestone no borra los issues/PRs asociados — solo los desasocia.

## Cerrar un issue automáticamente desde un Pull Request

GitHub reconoce ciertas palabras clave en la descripción de un PR (o en un mensaje de commit) para cerrar issues automáticamente al mergear:

```
close, closes, closed
fix, fixes, fixed
resolve, resolves, resolved
```

Sintaxis exacta:

```
Closes #10                          # mismo repositorio
Fixes octo-org/octo-repo#100        # repositorio distinto
```

> [!tip] También funcionan en mayúsculas y con dos puntos
> "The keywords can be followed by colons or in uppercase. For example: `Closes: #10`, `CLOSES #10`, or `CLOSES: #10`." *Fuente: GitHub Docs, "Linking a pull request to an issue".*

> [!warning] Solo funciona si el PR apunta a la rama por defecto
> "The special keywords in a pull request description are interpreted only when the pull request targets the repository's default branch. If the pull request targets any other branch, then these keywords are ignored, no links are created, and merging the PR has no effect on the issues." Si la keyword está en un **mensaje de commit** en vez de en la descripción del PR, el issue igual se cierra al mergear ese commit en la rama por defecto — pero el PR que lo contiene no queda listado como "linked pull request" del issue.

## Menciones y referencias

- `@usuario` o `@organizacion/equipo` — dispara una notificación: "This will trigger a notification and bring their attention to the conversation." Solo notifica a quien tenga acceso de lectura al repositorio (y, si es de una organización, sea miembro de ella).
- `#numero` (o `usuario/repo#numero` entre repositorios distintos) — se convierte automáticamente en un link corto al issue o PR correspondiente.

*Fuente: GitHub Docs, "Autolinked references and URLs" y "Basic writing and formatting syntax".*

## GitHub Projects: tableros de seguimiento

> [!definition] GitHub Projects
> "An adaptable table, board, and roadmap that integrates with your issues and pull requests on GitHub to help you plan and track your work effectively" — sin imponer un flujo de trabajo fijo. *Fuente: GitHub Docs, "About Projects".*

Ofrece tres vistas: **tabla** (estilo planilla, alta densidad de información), **tablero Kanban** (columnas por estado, útil para sprint planning y triage de bugs) y **roadmap tipo timeline** (para planificación de releases). Los cambios en issues/PRs se sincronizan automáticamente con el proyecto, y viceversa.

## Relacionado
- [[02 - Forks y Pull Requests]]
- [[01 - Introduccion y repositorios]]
- [[04 - GitHub Actions y CI-CD basico]]
