# Utilisation d'une image Nginx allégée
FROM nginx:alpine

# Suppression de la configuration Nginx par défaut
RUN rm /etc/nginx/conf.d/default.conf

# Copie de notre configuration Nginx personnalisée
COPY nginx.conf /etc/nginx/conf.d/

# Copie des fichiers statiques du front-end vers le dossier public de Nginx
COPY index.html /usr/share/nginx/html/

# Exposition du port HTTP standard
EXPOSE 80

# Démarrage de Nginx en premier plan
CMD ["nginx", "-g", "daemon off;"]