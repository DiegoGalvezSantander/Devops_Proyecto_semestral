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
# Usamos la variante Alpine oficial de Amazon Corretto para máxima eficiencia en AWS
FROM amazoncorretto:17-alpine
WORKDIR /app

# SEGURIDAD: Creamos un usuario de sistema para no ejecutar como root usando la sintaxis de Alpine (IE9)
RUN addgroup -S despacho-group && adduser -S despacho-user -G despacho-group
USER despacho-user

# Copiamos el archivo JAR generado en la etapa anterior
COPY --from=build /app/target/*.jar app.jar

# Exponemos el puerto que usa tu API de Despacho
EXPOSE 8080

# Comando para iniciar el microservicio
ENTRYPOINT ["java", "-jar", "app.jar"]
