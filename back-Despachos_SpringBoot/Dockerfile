# Etapa 1: Construcción (Build)
FROM maven:3.8.5-openjdk-17 AS build
WORKDIR /app

# Entramos a la carpeta interna donde está el pom.xml y el código
COPY Springboot-API-REST-DESPACHO/pom.xml .
COPY Springboot-API-REST-DESPACHO/src ./src

# Compilamos el proyecto
RUN mvn clean package -DskipTests

# Etapa 2: Ejecución (Runtime)
FROM amazoncorretto:17-alpine
WORKDIR /app

# Copiamos el .jar generado en la etapa anterior
COPY --from=build /app/target/*.jar app.jar
RUN addgroup -S despachos-group && adduser -S despachos-user -G despachos-group
USER despachos-user
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]
