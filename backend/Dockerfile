# Étape de build
FROM node:18-alpine AS build-back
WORKDIR /app

# Copie des fichiers nécessaires pour installer les dépendances
COPY package*.json ./

# Installation des dépendances
RUN npm install --only=production

# Copie du code de l'application
COPY . .

# Étape finale - image plus légère
FROM node:18-alpine
WORKDIR /app

# Arguments et variables d'environnement
ARG NODE_ENV=production
ENV NODE_ENV=${NODE_ENV}

# Copie les fichiers de l'étape de build
COPY --from=build-back /app /app

# Expose le port de l'application
EXPOSE 3000

# Commande pour démarrer l'application
CMD ["node", "index.js"]
