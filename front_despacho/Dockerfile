# ETAPA 1: Construcción (Build)
FROM node:18-alpine AS build
WORKDIR /app

# Copiamos archivos de dependencias y construimos el proyecto
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# ETAPA 2: Ejecución (Runtime)
# Usamos el servidor web Nginx optimizado sobre la distribución ultra ligera Alpine
FROM nginx:1.25.1-alpine
WORKDIR /usr/share/nginx/html

# Limpiamos el directorio por defecto de Nginx
RUN rm -rf ./*

# Copiamos los archivos estáticos generados por la etapa de construcción
COPY --from=build /app/dist .

# SEGURIDAD: Creamos un usuario no-root nativo en Alpine para mitigar riesgos en el host (IE9)
RUN addgroup -S front-group && adduser -S front-user -G front-group

# Aseguramos los permisos necesarios para que Nginx corra el contenido como no-root
RUN chown -R front-user:front-group /usr/share/nginx/html /var/cache/nginx /var/run /var/log/nginx

USER front-user

EXPOSE 80

# Iniciamos Nginx en primer plano
CMD ["nginx", "-g", "daemon off;"]
