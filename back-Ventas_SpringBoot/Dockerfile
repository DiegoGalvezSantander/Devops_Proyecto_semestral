# ETAPA 1: Compilación (Build)

# Usamos Maven para transformar el código en un archivo ejecutable

FROM maven:3.8.5-openjdk-17 AS build

WORKDIR /app



# Copiamos los archivos de configuración y el código fuente

COPY pom.xml .

COPY src ./src



# Compilamos el proyecto generando el archivo JAR

RUN mvn clean package -DskipTests



# ETAPA 2: Ejecución (Run)

# Usamos una imagen liviana para que corra de forma eficiente en AWS

FROM openjdk:17-jdk-slim

WORKDIR /app



# SEGURIDAD: Creamos un usuario de sistema para evitar ejecutar como administrador (Root)

RUN addgroup --system ventas-group && adduser --system ventas-user --ingroup ventas-group

USER ventas-user



# Copiamos el archivo JAR desde la etapa de compilación

# Maven guarda el resultado en la carpeta 'target' que se ve en tu imagen

COPY --from=build /app/target/*.jar app.jar



# Exponemos el puerto del backend

EXPOSE 8080



# Comando para iniciar el microservicio de Ventas

ENTRYPOINT ["java", "-jar", "app.jar"]