# Innovatech Chile - Proyecto de Despliegue Automatizado (EP2)

## Descripción del Proyecto
Este proyecto implementa una solución de microservicios contenedorizados para la empresa Innovatech Chile. Se compone de un Frontend (Vite/React) y dos Backends (Spring Boot), desplegados automáticamente en AWS mediante un pipeline de CI/CD.

## Tecnologías Aplicadas (Principios DevOps)
* **Contenedorización:** Docker y Docker Compose (Multi-stage builds y usuario no root).
* **Orquestación:** Docker Compose para la gestión de redes y volúmenes.
* **Automatización:** GitHub Actions para el ciclo de Build, Push y Deploy.
* **Infraestructura:** AWS EC2 (Instancia pública para Front e instancia privada para Back).
* **Persistencia:** Named Volumes para la continuidad operativa de los datos.

## Cómo ejecutar localmente
1. Clonar el repositorio.
2. Asegurarse de tener Docker Desktop instalado.
3. Ejecutar el comando en la raíz:
   ```bash
   docker-compose up -d --build
