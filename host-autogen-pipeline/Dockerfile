# Étape 1 : Utiliser une image de base Node.js pour construire le projet (frontend + backend)
FROM node:18 AS build

# Définir le répertoire de travail
WORKDIR /app

# Mise à jour des paquets et installation de rsync, Python, pip et venv
RUN apt-get update && apt-get install -y \
    rsync \
    python3 \
    python3-pip \
    python3-venv \
    && rm -rf /var/lib/apt/lists/*

# Créer un environnement virtuel pour Python
RUN python3 -m venv /venv

# Activer l'environnement virtuel
ENV PATH="/venv/bin:$PATH"

# Copier tout le projet dans le conteneur
COPY team.json .

# Installer les dépendances Python dans l'environnement virtuel
RUN pip install --upgrade pip
RUN pip install -U autogenstudio

# Exposer les ports nécessaires
EXPOSE 8084

# Commande pour démarrer le backend et le serveur frontend
CMD ["autogenstudio", "serve","--team","/app/team.json", "--port", "8084", "--host", "0.0.0.0"]