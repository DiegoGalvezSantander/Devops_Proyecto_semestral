# ETAPA 1: Compilación (Build)
FROM maven:3.8.5-openjdk-17 AS build
WORKDIR /app

COPY pom.xml .
COPY src ./src

RUN mvn clean package -DskipTests

# ETAPA 2: Ejecución (Run)
# Usamos la variante Alpine oficial de Amazon Corretto para máxima eficiencia en AWS
FROM amazoncorretto:17-alpine
WORKDIR /app

# SEGURIDAD: Creamos un usuario de sistema para no ejecutar como root usando la sintaxis de Alpine (IE9)
RUN addgroup -S ventas-group && adduser -S ventas-user -G ventas-group
USER ventas-user

# Copiamos el archivo JAR generado en la etapa anterior
COPY --from=build /app/target/*.jar app.jar

# Exponemos el puerto que usa tu API de Ventas
EXPOSE 8080

# Comando para iniciar el microservicio
ENTRYPOINT ["java", "-jar", "app.jar"]
