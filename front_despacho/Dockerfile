# Etapa 1: Construcción
FROM node:20-slim AS build
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# Etapa 2: Servidor Nginx (IE5)
FROM nginx:alpine

# Configuramos permisos para que el usuario nginx pueda manejar los archivos
RUN touch /var/run/nginx.pid && \
    chown -R nginx:nginx /var/run/nginx.pid /var/cache/nginx /var/log/nginx /etc/nginx/conf.d

# Copiamos los archivos estáticos
COPY --from=build /app/dist /usr/share/nginx/html

# Aplicamos el principio de mínimo privilegio (IE1)
USER nginx

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
