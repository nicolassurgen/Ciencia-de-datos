---
titulo: Git - Repositorios remotos (clone, push, pull, fetch)
materia: Git
tipo: apunte
tags:
  - git
  - tecnologias
  - tema/remotos
fuente: "Pro Git Book, cap. 2 (git-scm.com/book); Git Reference Manual (git-scm.com/docs)"
---

# Git - Repositorios remotos (clone, push, pull, fetch)

## ¿Qué es un repositorio remoto?

> [!definition] Repositorio remoto
> "Remote repositories are versions of your project that are hosted on the Internet or network somewhere." No implica necesariamente otra máquina en la red — solo que está "en otro lugar" al que hay que conectarse para sincronizar. *Fuente: Pro Git Book, "Working with Remotes".*

## `git clone`: traer todo el historial

```bash
git clone https://github.com/usuario/proyecto.git
```

> [!important] Clone trae **todo** el historial, no solo el estado actual
> "Instead of getting just a working copy, Git receives a full copy of nearly all data that the server has. Every version of every file for the history of the project is pulled down by default when you run `git clone`." Es la manifestación directa de que Git es distribuido (ver [[01 - Introduccion y control de versiones]]). *Fuente: Pro Git Book, "Getting a Git Repository".*

Al clonar, Git automáticamente: crea el remoto llamado `origin` (por convención), crea ramas de **tracking remoto** para cada rama del repositorio original, y configura la rama local principal para hacer seguimiento (*tracking*) de su equivalente en `origin`. *Fuente: Git Reference, `git-clone`.*

## Gestionar remotos

```bash
git remote -v                          # listar remotos, con sus URLs
git remote add upstream <url>          # agregar otro remoto con nombre "upstream"
git remote show origin                 # inspeccionar el detalle de un remoto
```

## `git fetch` vs. `git pull`: la distinción que hay que tener clara

> [!important] `fetch` descarga; `pull` descarga **y mezcla**
> "The `git fetch` command only downloads the data to your local repository — it doesn't automatically merge it with any of your work or modify what you're currently working on. You have to merge it manually into your work when you're ready." *Fuente: Pro Git Book, "Working with Remotes".*
>
> `git pull`, en cambio: "First, `git pull` runs `git fetch` [...] Then it integrates that branch into the current branch" (por defecto con un merge; se puede configurar para que use rebase en su lugar con `git pull --rebase`). *Fuente: Git Reference, `git-pull`.*

En la práctica: `git fetch` es seguro para "mirar" qué cambió en el remoto sin tocar el propio trabajo; `git pull` combina ese fetch con una integración inmediata — cómoda, pero significa que el propio historial local puede cambiar (por un merge) en el mismo paso.

## `git push`: subir commits locales

```bash
git add archivo.py
git commit -m "Agrega función de limpieza"
git push origin main
```

La primera vez que se sube una rama nueva conviene fijar el tracking, para que después alcance con `git push`/`git pull` sin argumentos:

```bash
git push -u origin mi-rama
```

### Qué pasa si el remoto tiene commits que el local no tiene

```
$ git push
 ! [rejected]        main -> main (fetch first)
error: failed to push some refs
```

> [!warning] Git rechaza el push para no sobrescribir trabajo ajeno
> "This command works only if you cloned from a server to which you have write access and if nobody has pushed in the meantime. If you and someone else clone at the same time and they push upstream and then you push upstream, your push will rightly be rejected. You'll have to fetch their work first and incorporate it into yours before you'll be allowed to push." *Fuente: Pro Git Book, "Working with Remotes".*

La solución documentada:

```bash
git pull            # trae los cambios y los mezcla (crea un commit de merge si hace falta)
# resolver conflictos si aparecen
git push            # ahora sí, con el historial remoto ya incorporado
```

## Autenticación: HTTPS (con token) vs. SSH

Hay dos formas de conectarse con un remoto que requiere autenticación (como GitHub):

- **HTTPS**: funciona incluso detrás de firewalls o proxies restrictivos; se autentica con un **Personal Access Token (PAT)** en vez de contraseña — desde el 13 de agosto de 2021, GitHub dejó de aceptar contraseñas de cuenta para operaciones Git sobre HTTPS.
- **SSH**: requiere generar un par de claves (pública/privada) y registrar la clave pública en la cuenta remota; una vez configurado, no vuelve a pedir credenciales en cada operación. Algunos firewalls restrictivos pueden bloquear conexiones SSH.

Cualquiera de las dos es válida — HTTPS+token es más simple de arrancar; SSH es más cómodo para quien trabaja todos los días desde la misma máquina. Ver [[01 - Introduccion y repositorios]] de GitHub para el detalle de conectar un repo local con un remoto en GitHub específicamente.

## Relacionado
- [[01 - Introduccion y control de versiones]]
- [[02 - El flujo basico (working directory, staging area, repositorio)]]
- [[04 - Ramas y fusion (branching y merge)]]
- [[01 - Introduccion y repositorios]]
