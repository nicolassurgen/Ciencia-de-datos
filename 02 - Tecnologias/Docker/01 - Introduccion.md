---
titulo: Introducción a Docker
materia: Docker
tipo: apunte
tags:
  - docker
  - tecnologias
  - tema/introduccion
fuente: "Docker Docs — Docker overview (docs.docker.com/get-started/docker-overview); Guía Docker Pabpereza"
---

# Introducción a Docker

Un mismo proyecto suele fallar con el clásico "en mi máquina funciona": distintas versiones de librerías, de sistema operativo, o dependencias instaladas manualmente que nadie documentó. Ejecutar la aplicación junto con **todo su entorno**, empaquetado y reproducible, elimina esa fuente de errores — ese es el problema que resuelven los contenedores.

## ¿Qué es un contenedor?

> [!definition] Contenedor
> Unidad de software que encapsula una aplicación y **todas sus dependencias** en un entorno aislado.

Características clave:
- Tiene su propio sistema de archivos, bibliotecas y configuraciones
- Comparte el **kernel del SO** subyacente (no lo duplica)
- Portable, escalable y eficiente en recursos
 
## Docker
- Lanzado en **2013** por Docker, Inc.
- No inventó los contenedores — existía LXC (Linux Containers) antes
- Los popularizó con una forma simple de crear, distribuir y ejecutar software

## Contenedores vs. Máquinas Virtuales

**VMs**
- Emulan hardware completo + SO propio
- Corren sobre un **hipervisor**
- Mayor aislamiento, mayor consumo de recursos

**Contenedores**
- Comparten el kernel del SO anfitrión
- Más ligeros y rápidos que las VMs
- Sin sobrecarga de SO completo

## Estándar OCI
- **Open Container Initiative** — creado en 2015
- Define specs comunes para imágenes y runtimes de contenedores
- Fundadores: Docker, CoreOS, Google, Red Hat, VMware
- Garantiza portabilidad e interoperabilidad entre plataformas

## Casos de uso
- Desarrollo y pruebas de aplicaciones
- Microservicios
- CI/CD (Continuous Integration / Continuous Deployment)
- Despliegue en la nube
- Aislamiento, escalabilidad y alta disponibilidad
- Desarrollo multiplataforma

❌ No aplica para: apps móviles nativas, interfaces gráficas nativas (Windows/Mac)

Conceptos claves de Docker:
- [[02 - Imagen]]
- [[03 - Contenedor]]
- [[04 - Dockerfile]]
- [[05 - DockerHub]]


## Recursos
* [Guia Docker Pabpereza](https://pabpereza.dev/docs/cursos/docker/conceptos_basicos_de_docker_imagenes_contenedores_y_dockerfiles)


