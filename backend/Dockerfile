# EXPLICATION DU MULTI-STAGE BUILD

# L'utilisation du multi-stage build est pertinente pour deux raisons :

# 1. Sécurité : L'image finale ne contient pas les outils de build ni le code source des tests, réduisant ainsi considérablement la surface d'attaque.

# 2. Taille d'image : On abandonne les "devDependencies" qui sont très lourdes, pour ne conserver que les dépendances strictes de production dans une image Alpine ultra-légère, ce qui accélère les déploiements.

# STAGE 1 : BUILD ET TESTS
FROM node:20 AS builder
WORKDIR /app
# Copie des fichiers de configuration des dépendances
COPY package*.json ./
# Installation de toutes les dépendances
RUN npm install
# Copie du code source
COPY . .
# Exécution des tests unitaires
RUN npm run test

# STAGE 2 : PRODUCTION
# Utilisation de la version Alpine pour minimiser la taille
FROM node:20-alpine
WORKDIR /app
# Copie uniquement des dépendances de production depuis le builder
COPY package*.json ./
RUN npm install --only=production
# Copie uniquement le code source nécessaire à l'exécution de l'API depuis le builder
COPY --from=builder /app/server.js ./

# Exposition du port de l'API
EXPOSE 3000

# Commande de démarrage
CMD ["node", "server.js"]