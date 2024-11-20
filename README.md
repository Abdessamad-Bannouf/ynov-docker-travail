# 🚀 Déploiement de l'Application avec Docker

Ce guide décrit comment configurer un environnement **Frontend** en Angular, **Backend** en Node.js, et **Base de données PostgreSQL** à l'aide de **Docker**.

---

## 📦 Prérequis

Assurez-vous que **Docker** est installé sur votre machine.

## 📂 Configuration du dossier db pour la database

- Créer un dossier "db" dans le répertoire docker. 


- Créer ensuite un fichier .env et rajouter les lignes suivantes : \
DB_USER=postgres \
POSTGRES_USER=${DB_USER}

### 🔑 Passons ensuite à la partie password

- Créer un fichier db_password.txt et mettre uniquement le password de postgres en brut


- Créer un fichier pgadmin_db_password.txt et mettre uniquement le password de pgadmin en brut

## ✨ Génération du secret pour les passwords

Exécuter les commandes : 

    docker swarm init
    docker secret create db_password ./db/db_password.txt
    docker secret create pgadmin_db_password ./db/pgadmin_db_password.txt

## 🐳⚙️ Docker compose

Lancer les commandes : 

    docker compose build
    docker compose up -d

\

## 🖥️ Frontend

Aller sur l'url :

    http://localhost:4300/

\

## 🛠️ Backend

Aller sur l'url :

    http://localhost:4000/

\

## 🗃️ Base de données

Aller sur l'url :

    http://localhost:8888

Mettre comme login : 

    abdessamad.bannouf@laposte.net

PS: vous pouvez changer de mail en changeant la valeur de PGADMIN_DEFAULT_EMAIL dans le docker compose

Mettre le password correspondant.

### Création de la database au sein de pgadmin

Tout d'abord lancer les commandes : 

    docker container ps
    récupérer l'id du container project-db
    docker inspect <id_du_container> | grep IPAddress

- Récupérer la valeur IPAddress


- Ensuite sur l'interface pgadmin cliquer sur Add New Server


- Dans l'onglet général mettre un nom pour le serveur


- Après cliquer sur l'onglet connection puis dans Host name mettre la valeur de l'IPAddress


- Dans le champ port mettre : 5432


- Dans le champ username mettre : postgres


- Dans le champ password mettre le password correspondant


## 🐳👀 Docker Watch

Lancer la commande :

    docker compose watch

En modifiant ce qui se trouve dans le fichier backend, vous pourrez voir les modifications sur le terminal en temps réel.