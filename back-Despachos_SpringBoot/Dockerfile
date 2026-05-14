# Etapa 1: Construcción (Build)
FROM maven:3.8.5-openjdk-17 AS build
WORKDIR /app
COPY pom.xml .
COPY src ./src
RUN mvn clean package -DskipTests

# Etapa 2: Ejecución (Runtime) - AQUÍ ESTÁ EL CAMBIO
FROM amazoncorretto:17-alpine
WORKDIR /app
# Copiamos el JAR generado en la etapa anterior
COPY --from=build /app/target/*.jar app.jar

EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]
