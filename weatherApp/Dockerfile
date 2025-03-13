# Etapa 1: Construir la aplicación de React
FROM node:18 AS build

# Instalar dependencias necesarias para crypto
RUN apt-get update && apt-get install -y libssl-dev

# Definir el directorio de trabajo
WORKDIR /app

# Copiar los archivos package.json y package-lock.json
COPY package*.json ./

# Instalar dependencias de npm
RUN npm install

# Copiar el resto de los archivos del proyecto
COPY . .

# Ejecutar la construcción de la app con Vite
RUN npm run build

# Etapa 2: Configurar el servidor para servir los archivos estáticos
FROM nginx:alpine

# Copiar los archivos de la construcción al directorio de Nginx
COPY --from=build /app/dist /usr/share/nginx/html

# Exponer el puerto donde Nginx estará escuchando
EXPOSE 80

# Comando para ejecutar Nginx
CMD ["nginx", "-g", "daemon off;"]
