---
titulo: Docker - Contenedor
materia: Docker
tipo: apunte
tags:
  - docker
  - tecnologias
  - tema/contenedores
---

# Docker - Contenedor

> [!definition] Contenedor
> Una **instancia de una imagen**. Es un proceso que se ejecuta en un entorno aislado.

## Concepto clave

Un contenedor **no es una máquina virtual** ni un sistema operativo completo. Es un **proceso** que contiene:
- La aplicación
- Sus dependencias de librerías del lenguaje
- Sus dependencias de sistema operativo

> [!warning] Confusión habitual
> La confusión con las VMs viene porque incluye librerías de SO, pero no es lo mismo.

## Ciclo de vida

Un contenedor se ejecuta en torno a un **comando principal** (definido en el [[04 - Dockerfile]] con `CMD` o `ENTRYPOINT`):
- Cuando ese comando finaliza → el contenedor finaliza
- Puede ejecutar una tarea puntual y terminar
- O puede mantener un servicio siempre en ejecución

```
Posibles estados:
ejecutar → parar → reiniciar → eliminar
```

## Relación con la imagen

- Un contenedor es solo una **instancia** de la [[02 - Imagen]]
- Eliminar un contenedor **no elimina la imagen**
- Se pueden crear múltiples contenedores desde la misma imagen

## Guardar estado (commit)

Es posible guardar el estado de un contenedor en ejecución como una nueva imagen:
- Similar a una **snapshot** de una VM
- Permite persistir datos, archivos en RAM, estado de la aplicación
- Genera una imagen nueva con el estado actual

> [!warning] Buena práctica
> Evitar depender del estado. Las imágenes deben ser **estáticas y reproducibles** desde el primer arranque.

## Analogía

```
Imagen  →  Clase (plantilla)
Contenedor  →  Objeto (instancia)
```
