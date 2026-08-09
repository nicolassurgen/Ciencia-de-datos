---
titulo: GitHub - GitHub Actions y CI/CD básico
materia: GitHub
tipo: apunte
tags:
  - github
  - tecnologias
  - tema/ci-cd
fuente: "GitHub Docs (docs.github.com)"
---

# GitHub - GitHub Actions y CI/CD básico

## ¿Qué problema resuelve?

Correr los tests manualmente cada vez, en la propia máquina, antes de mergear un cambio, es fácil de olvidar — y distinto de una persona a otra según qué versión de Python o de las dependencias tenga instalada localmente. La **integración continua** (CI) automatiza esa verificación: cada vez que se sube código, una máquina neutral (no la de nadie en particular) corre los tests desde cero, sobre un entorno limpio y reproducible.

> [!definition] CI/CD
> "GitHub Actions is a continuous integration and continuous delivery (CI/CD) platform that allows you to automate your build, test, and deployment pipeline." *Fuente: GitHub Docs, "Understanding GitHub Actions".*

## Vocabulario de GitHub Actions

| Término | Definición oficial |
|---|---|
| **Workflow** | "A configurable automated process that will run one or more jobs." Vive en un archivo YAML. |
| **Event** | "A specific activity in a repository that triggers a workflow run" (un push, abrir un PR, crear un issue). |
| **Job** | "A set of steps in a workflow that is executed on the same runner." |
| **Step** | "Either a shell script that will be executed, or an action that will be run." |
| **Action** | "A pre-defined, reusable set of jobs or code that performs specific tasks within a workflow" (código reutilizable, propio o de la comunidad). |
| **Runner** | "A server that runs your workflows when they're triggered" — hospedado por GitHub (Ubuntu/Windows/macOS) o *self-hosted*. |

*Fuente: GitHub Docs, "Understanding GitHub Actions".*

## Dónde viven los workflows

> [!important] Ubicación exacta
> "Workflows are defined in the `.github/workflows` directory in a repository." Un repositorio puede tener varios archivos de workflow, cada uno con su propio propósito. *Fuente: GitHub Docs, "About workflows".*

## Un workflow mínimo (ejemplo oficial de quickstart)

```yaml
# .github/workflows/github-actions-demo.yml
name: GitHub Actions Demo
run-name: ${{ github.actor }} is testing out GitHub Actions 🚀
on: [push]
jobs:
  Explore-GitHub-Actions:
    runs-on: ubuntu-latest
    steps:
      - run: echo "🎉 The job was automatically triggered by a ${{ github.event_name }} event."
      - name: Check out repository code
        uses: actions/checkout@v6
      - run: echo "🖥️ The workflow is now ready to test your code on the runner."
      - name: List files in the repository
        run: |
          ls ${{ github.workspace }}
```

*Fuente: GitHub Docs, "Quickstart for GitHub Actions".*

### Leyendo el archivo

- `on: [push]` — el **evento** que dispara el workflow: cualquier `push` al repositorio.
- `jobs.Explore-GitHub-Actions` — el **job** (se le puede poner cualquier nombre).
- `runs-on: ubuntu-latest` — el **runner**: una máquina virtual Ubuntu hospedada por GitHub.
- `steps` — la secuencia de pasos del job. Cada uno es o un `run:` (un comando de shell) o un `uses:` (una **action** reutilizable, como `actions/checkout`, que descarga el código del repositorio al runner).

## Ejemplo real: correr tests de Python con pytest

```yaml
name: Python package

on: [push]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v6
      - name: Set up Python
        uses: actions/setup-python@v5
        with:
          python-version: '3.x'
      - name: Install dependencies
        run: |
          python -m pip install --upgrade pip
          pip install -r requirements.txt
      - name: Test with pytest
        run: |
          pip install pytest
          pytest
```

*Fuente: GitHub Docs, "Building and testing Python".* Este workflow corre en cada `push`: descarga el código (`actions/checkout`), instala la versión de Python indicada (`actions/setup-python`), instala las dependencias del proyecto, y corre la suite de tests con `pytest` — todo en una máquina limpia, igual para cualquiera que lo dispare.

## Triggers: `push` y `pull_request`, con filtros

```yaml
on:
  push:
    branches:
      - main
      - 'releases/**'

on:
  pull_request:
    branches:
      - main
```

> [!tip] Filtrar por rama, incluir y excluir
> `branches` acepta patrones (`releases/**`) y se puede combinar con `!` para excluir un caso puntual dentro de una regla más amplia: `branches: ['releases/**', '!releases/**-alpha']`. También existe `branches-ignore` como alternativa (mutuamente excluyente con `branches` dentro del mismo evento). *Fuente: GitHub Docs, "Triggering a workflow".*

> [!note] Correr un workflow solo en Pull Requests hacia una rama específica
> Es el patrón más común para CI: correr los tests en cada PR antes de aprobar el merge (ver [[02 - Forks y Pull Requests]]), no solo en cada push directo — así ningún cambio llega a `main` sin haber pasado la verificación automática.

## Relacionado
- [[02 - Forks y Pull Requests]]
- [[03 - Issues y gestion de proyectos]]
- [[01 - Introduccion y repositorios]]
