---
titulo: Docker - Dockerfile
materia: Docker
tipo: apunte
tags:
  - docker
  - tecnologias
  - tema/dockerfile
fuente: "Docker Docs — Dockerfile reference (docs.docker.com/reference/dockerfile); Guía Docker Pabpereza"
---

# Docker - Dockerfile

> [!definition] Dockerfile
> Un **archivo de texto con instrucciones secuenciales** que le especifican a Docker cómo construir una [[02 - Imagen]].

## Concepto

Es infraestructura como código: define el proceso de construcción de una imagen de forma **reproducible y versionable**. Funciona como si fuera una serie de comandos ejecutados sobre un Linux limpio.

## Instrucciones principales

| Instrucción | Función |
|---|---|
| `FROM` | Define la **imagen base** (siempre es la primera instrucción) |
| `RUN` | Ejecuta un comando durante la construcción |
| `COPY` | Copia archivos desde el host hacia la imagen |
| `CMD` | Comando por defecto al iniciar el contenedor (sobreescribible) |
| `ENTRYPOINT` | Punto de entrada fijo del contenedor |
| `ENV` | Define variables de entorno |
| `EXPOSE` | Declara el puerto que expone la aplicación |

> [!note] `CMD` vs `ENTRYPOINT`
> Ambos definen el comando principal del [[03 - Contenedor]], pero `ENTRYPOINT` es más rígido. Ver detalles en capítulo dedicado.

## Ejemplo: servidor web Apache

```dockerfile
FROM ubuntu:22.04
RUN apt-get update && apt-get install -y apache2
COPY index.html /var/www/html/
CMD ["apache2ctl", "-D", "FOREGROUND"]
```

Paso a paso:
1. Parte de la imagen base `ubuntu:22.04`
2. Actualiza paquetes e instala Apache2
3. Copia el archivo `index.html` al directorio de Apache
4. Define el comando de arranque del servidor

## Flujo de trabajo

```
Dockerfile  →  docker build  →  Imagen  →  docker run  →  Contenedor
```

## Ventajas

- El proceso de construcción queda **documentado como código**
- Fácilmente **replicable** en cualquier entorno
- Permite **versionar** la definición de la imagen junto al código fuente
- Elimina el problema de "en mi máquina funciona"
