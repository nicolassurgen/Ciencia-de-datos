---
titulo: Docker - Docker Hub
materia: Docker
tipo: apunte
tags:
  - docker
  - tecnologias
  - tema/dockerhub
---

# Docker - Docker Hub

> [!definition] Docker Hub
> El **repositorio público de imágenes de contenedor** más popular. Es a las imágenes Docker lo que GitHub es al código fuente.

## ¿Qué es?

Un registro donde se pueden:
- **Descargar** imágenes ya creadas por la comunidad o por empresas
- **Publicar** imágenes propias para compartirlas
- **Versionar y etiquetar** imágenes (similar a tags en git)

## Comandos básicos

```bash
docker pull nombre-imagen          # descargar imagen
docker pull nombre-imagen:tag      # versión específica
docker push usuario/nombre-imagen  # subir imagen propia
```

## Alternativas (estándar OCI)

Docker Hub no es el único registro. Cualquier registro compatible con OCI funciona con Docker:

| Registro                  | Proveedor          |
| ------------------------- | ------------------ |
| Docker Hub                | Docker Inc.        |
| GitHub Container Registry | GitHub / Microsoft |
| GitLab Container Registry | GitLab             |
| Amazon ECR                | AWS                |
| Google Container Registry | Google Cloud       |
| Azure Container Registry  | Microsoft Azure    |

> [!note]
> La portabilidad entre registros es posible gracias al estándar OCI (Open Container Initiative).

## Tipos de imágenes en Docker Hub

- **Imágenes oficiales**: mantenidas por Docker o por el proyecto original (ej: `nginx`, `postgres`, `python`)
- **Imágenes de comunidad**: publicadas por usuarios (`usuario/nombre-imagen`)
- **Imágenes verificadas**: de publishers de confianza

## Analogía con git

```
git clone  ≈  docker pull
git push   ≈  docker push
git tag    ≈  docker tag
branch     ≈  etiquetas / tags de imagen
```

