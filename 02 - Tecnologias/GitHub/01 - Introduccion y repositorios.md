---
titulo: GitHub - Introducción y repositorios
materia: GitHub
tipo: apunte
tags:
  - github
  - tecnologias
  - tema/introduccion
fuente: "GitHub Docs (docs.github.com); GitHub Changelog (github.blog/changelog)"
---

# GitHub - Introducción y repositorios

## GitHub no es lo mismo que Git

Es una confusión frecuente al empezar. **Git** es el sistema de control de versiones (ver [[01 - Introduccion y control de versiones]] de Git) — una herramienta de línea de comandos que funciona sin conexión a internet. **GitHub** es una plataforma que aloja repositorios Git en la nube y agrega una capa de colaboración encima: interfaz web, Pull Requests, Issues, Projects, Actions.

> [!important] GitHub está construido sobre Git
> La documentación oficial identifica a Git explícitamente como "the version control software" sobre la que GitHub se construye. Para tareas simples desde la interfaz web, GitHub incluso permite trabajar "without [needing] to know how to code, use the command line, or install Git" — pero por debajo, todo repositorio de GitHub **es** un repositorio Git. *Fuente: GitHub Docs, "Hello World".*

GitHub no es la única plataforma de este tipo — existen alternativas como GitLab o Bitbucket, que también usan Git como motor de versionado.

## Repositorio

> [!definition] Repositorio
> "A folder that contains related items, such as files, images, videos, or even other folders." Organiza los materiales de un proyecto, típicamente con un `README` que lo describe. *Fuente: GitHub Docs, "Hello World".*

## Crear un repositorio en GitHub

Desde la interfaz web: ícono **+** → **New repository** → nombre → descripción (opcional) → elegir visibilidad (**Public**/**Private**) → opción de agregar un `README.md` inicial automáticamente. *Fuente: GitHub Docs, "Quickstart for repositories".*

> [!tip] El README tiene tratamiento especial
> GitHub **renderiza automáticamente** el `README.md` en la página principal del repositorio — está escrito en Markdown, "an easy-to-read, easy-to-write language for formatting plain text". Es, en la práctica, la carta de presentación de cualquier proyecto.

## Conectar un repositorio local con GitHub

Si el proyecto ya existe localmente (por ejemplo, con `git init` ya hecho — ver [[01 - Introduccion y control de versiones]] de Git), conectar con un repo vacío recién creado en GitHub usa estos comandos, citados literalmente de la documentación oficial:

```bash
git remote add origin REMOTE-URL
git remote -v                    # verificar que quedó bien
git push -u origin main
```

*Fuente: GitHub Docs, "Adding locally hosted code to GitHub".*

Si en cambio el repositorio ya existe en GitHub y se quiere una copia local, `git clone <url>` es la vía estándar (trae todo el historial — ver [[05 - Repositorios remotos (clone, push, pull, fetch)]] de Git).

## Autenticación: HTTPS con token, o SSH

> [!warning] GitHub ya no acepta contraseña simple para Git sobre HTTPS
> Desde el **13 de agosto de 2021** (09:00 PST), GitHub eliminó la autenticación por contraseña de cuenta para operaciones Git sobre HTTPS, exigiendo en su lugar un **Personal Access Token (PAT)**, OAuth, una clave SSH, o un token de instalación de GitHub App. *Fuente: GitHub Changelog, "Git password authentication is shutting down" (2021-08-12).*

Las dos formas de conectarse a un repositorio de GitHub:

- **HTTPS**: funciona detrás de casi cualquier firewall/proxy. Se autentica con un **Personal Access Token** en vez de contraseña — existen dos tipos: **clásicos** (prefijo `ghp_`) y **fine-grained** (prefijo `github_pat_`, con permisos más acotados y recomendados por GitHub cuando sea posible).
- **SSH**: requiere generar un par de claves y registrar la pública en la cuenta de GitHub; algunos firewalls restrictivos pueden bloquear este protocolo.

*Fuente: GitHub Docs, "About authentication to GitHub".*

> [!note] Dato relacionado, no confundir
> Desde marzo de 2023, GitHub además exige habilitar autenticación de dos factores (2FA) a todo usuario que contribuye código en GitHub.com — es un requisito de seguridad de cuenta, distinto (aunque relacionado) de la autenticación Git vía token/SSH.

## Público vs. privado

Al crear un repositorio hay que elegir su visibilidad: **público** (cualquiera puede verlo, típico de proyectos open source) o **privado** (acceso restringido a quien se invite explícitamente como colaborador).

## Relacionado
- [[01 - Introduccion y control de versiones]]
- [[05 - Repositorios remotos (clone, push, pull, fetch)]]
- [[02 - Forks y Pull Requests]]
