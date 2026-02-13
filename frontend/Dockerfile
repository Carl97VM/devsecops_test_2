#FROM node:20-alpine

#WORKDIR /app

#COPY package*.json ./
#RUN npm install

#COPY . .
#RUN npm run build

#EXPOSE 4173
#CMD ["npm", "run", "preview", "--", "--host"]

# Etapa de Build
FROM node:20-alpine AS build
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build

# Etapa de Producción (Serve)
FROM nginx:alpine

# Copiar archivos compilados
COPY --from=build /app/dist /usr/share/nginx/html

# Configuración de seguridad para Nginx no-root [cite: 45, 50]
RUN touch /var/run/nginx.pid && \
    chown -R nginx:nginx /var/run/nginx.pid /var/cache/nginx /var/log/nginx /etc/nginx/conf.d

# Activar usuario nginx
USER nginx

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]