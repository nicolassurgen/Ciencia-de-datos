---
titulo: Docker - Imagen
materia: Docker
tipo: apunte
tags:
  - docker
  - tecnologias
  - tema/imagenes
---

# Docker - Imagen

> [!definition] Imagen
> Un **archivo binario** que contiene todos los elementos necesarios para ejecutar un [[03 - Contenedor]]. Es la plantilla a partir de la cual se crean contenedores.

## Componentes de una imagen

| Componente | Descripción |
|---|---|
| **Aplicación** | El código propio o de terceros ya empaquetado |
| **Librerías del lenguaje** | Ej: numpy, pandas (Python), Spring Boot (Java) |
| **Librerías de SO** | Herramientas base como `curl`, `wget`, `cat`... |
| **Configuración** | Usuario, comandos de arranque, puertos expuestos |

## Ejemplo práctico (Java)

Para una app Java necesitaríamos una imagen con:
1. JDK o JRE instalado
2. La aplicación compilada + librerías (ej: Spring Boot)
3. Comando de ejecución: `java application.jar`

## Cómo se crean

- Principalmente a través de un [[04 - Dockerfile]] (método recomendado)
- También se puede hacer commit del estado de un contenedor en ejecución (no recomendado como práctica habitual)

> [!important] Principio fundamental
> Las imágenes deben ser **estáticas** y no depender del estado de ningún contenedor. Así se garantiza el mismo comportamiento desde el primer arranque, en cualquier entorno.

## Dónde se almacenan

Las imágenes se publican y descargan desde registros como [[05 - DockerHub]] u otros compatibles con OCI (GitHub Container Registry, Amazon ECR, Google Container Registry...).

```bash
docker pull nombre-imagen   # descargar
docker push nombre-imagen   # subir
```

## Ventaja principal

Una vez generada la imagen, desaparecen los conflictos de dependencias entre aplicaciones. Cada una corre en su propio contenedor aislado con sus propias versiones de librerías.
