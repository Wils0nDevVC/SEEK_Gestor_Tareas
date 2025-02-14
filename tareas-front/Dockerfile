# Etapa 1: Construcción de Angular
FROM node:18 AS build-stage
WORKDIR /app

# Copiar package.json y package-lock.json antes para aprovechar la caché de Docker
COPY package*.json ./
RUN npm install

# Copiar el resto de los archivos y construir la aplicación
COPY . .
RUN npm run build --configuration=production  

# Etapa 2: Servir con Nginx
FROM nginx:1.21.0-alpine
COPY --from=build-stage /app/dist/tareas-app /usr/share/nginx/html  

# Copiar la configuración de Nginx correctamente
COPY nginx.conf /etc/nginx/nginx.conf
COPY conf.d/default.conf /etc/nginx/conf.d/default.conf  

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
