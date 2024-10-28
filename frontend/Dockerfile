# Étape de build
FROM node:18-alpine AS build-front
WORKDIR /app

# Copie des fichiers nécessaires
COPY package*.json ./

# Installation des dépendances
RUN npm install

# Copie du code et build
COPY .. .
RUN npm run build

# Étape finale - image légère avec Nginx pour servir les fichiers statiques
FROM nginx:alpine
#COPY --from=build-front /app/build /usr/share/nginx/html
COPY --from=build-front /app/dist/my-project /usr/share/nginx/html

# Variables d'environnement pour l'API backend
ENV API_URL=http://localhost:3000

# Expose le port de l'application
EXPOSE 80
