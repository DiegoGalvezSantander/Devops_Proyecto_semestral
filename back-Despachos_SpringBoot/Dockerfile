# ETAPA 1: Compilación (Build)

# Usamos una imagen de Maven para construir el archivo JAR

FROM maven:3.8.5-openjdk-17 AS build

WORKDIR /app



# Copiamos el archivo pom.xml y el código fuente para compilar

COPY pom.xml .

COPY src ./src



# Ejecutamos la compilación saltando los tests para ahorrar tiempo

RUN mvn clean package -DskipTests



# ETAPA 2: Ejecución (Run)

# Usamos una imagen ligera de Java para que el contenedor sea eficiente en AWS

FROM openjdk:17-jdk-slim

WORKDIR /app



# SEGURIDAD: Creamos un usuario de sistema para no ejecutar como root (Punto clave de la pauta)

RUN addgroup --system despacho-group && adduser --system despacho-user --ingroup despacho-group

USER despacho-user



# Copiamos el archivo JAR generado en la etapa anterior

# Nota: Spring Boot por defecto genera el archivo en la carpeta 'target'

COPY --from=build /app/target/*.jar app.jar



# Exponemos el puerto que usa tu API de Despacho (comúnmente 8080 o el que definas)

EXPOSE 8080



# Comando para iniciar el microservicio

ENTRYPOINT ["java", "-jar", "app.jar"]