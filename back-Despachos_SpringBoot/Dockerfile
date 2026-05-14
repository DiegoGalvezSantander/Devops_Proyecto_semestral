# Etapa 1: Construcción
FROM maven:3.8.5-openjdk-17 AS build
WORKDIR /app

# NOTA: Cambiamos la ruta para que busque dentro de la carpeta anidada
COPY Springboot-API-REST-DESPACHO/pom.xml .
COPY Springboot-API-REST-DESPACHO/src ./src

RUN mvn clean package -DskipTests

# Etapa 2: Ejecución
FROM amazoncorretto:17-alpine
WORKDIR /app
COPY --from=build /app/target/*.jar app.jar

EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]
