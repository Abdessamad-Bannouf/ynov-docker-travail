# 🚀 Déploiement de l'Application avec Docker

Ce guide décrit comment configurer un environnement **Frontend** en Angular, **Backend** en Node.js, et **Base de données PostgreSQL** à l'aide de **Docker**.

---

## 📦 Prérequis

Assurez-vous que **Docker** est installé sur votre machine.

## 📂 Configuration du Docker

### 🗄️Création de volume pour l'application :

Lancer la commande :

    docker volume create myapp_data

### 🌐 Creation de network :

Lancer la commande :

    docker network create appnetwork

\

## 🖥️ Frontend

Aller dans le dossier Docker et faire la commande :
    
    docker build -t my-project-front ./frontend

Lancer la commande avec le network qu'on a créé :

    docker run -d -p 4300:80 --name=angular --network appnetwork my-project-front

Enfin aller sur l'url :

    http://localhost:4300/

\

## 🛠️ Backend

Aller dans le dossier Docker et faire la commande :

    docker build -t my-project-back ./backend

Lancer la commande avec le network qu'on a créé :

    docker run -d -p 4000:3000 NODE_ENV=production --name=node-api --network appnetwork my-project-back

Enfin aller sur l'url :

    http://localhost:4000/

\

### 🗃️ Base de données

Pour la connexion à la base de données avec les variables d'environnements et le volume qu'on a créé, lancer la commande :

    docker run --name=my-project-db -d -e POSTGRES_USER=postgres -e POSTGRES_PASSWORD=postgres -e POSTGRES_DB=mydb -p 5431:5432 -v myapp_data:/var/lib/postgresql/data postgres:13

Avant de pouvoir se connecter à la base de données, il faut exécuter le container

    docker exec -it my-project-db bash 

Et enfin se connecter sur la base de données

    psql -U postgres -d mydb
