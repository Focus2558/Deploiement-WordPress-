# Documentation - Déploiement WordPress avec Docker (Test MSc Cybersécurité)

## 1. Objectif du projet
L'objectif de ce projet est de déployer un site WordPress complet en utilisant Docker et Docker Compose. Le déploiement est réalisé sur une machine virtuelle Linux (hébergée sur Microsoft Azure), avec une configuration permettant l'accès distant via le port 8080.

## 2. Environnement utilisé
- Machine virtuelle Ubuntu (Microsoft Azure)
- Docker installé via APT
- Docker Compose installé
- Accès SSH à distance
- Règle de pare-feu (NSG) configurée pour autoriser le trafic sur le port 8080

## 3. Structure du projet
Le dossier du projet `wordpress-docker` contient :

```
wordpress-docker/
├── docker-compose.yaml   # Fichier principal de configuration Docker
├── README.md             # Documentation du projet
```

Deux volumes Docker sont utilisés pour garantir la persistance des données :
- `db_data` : pour les fichiers de la base de données MariaDB
- `wp_data` : pour les fichiers WordPress

## 4. Fichier docker-compose.yaml
Le fichier de composition définit deux services :
- **mariadb** : le moteur de base de données utilisé par WordPress
- **wordpress** : l'application web avec Apache intégré

Port 8080 mappé vers le port 80 du conteneur WordPress, permettant un accès depuis l’extérieur.

## 5. Étapes de déploiement

### Étape 1 : Création du dossier de travail
```bash
mkdir wordpress-docker
cd wordpress-docker
```

### Étape 2 : Création du fichier docker-compose.yaml
Contient la définition des services `db` (mariadb) et `wordpress`. Les variables d’environnement sont utilisées pour initialiser la base de données.

### Étape 3 : Lancement des conteneurs
```bash
docker-compose up -d
```

### Étape 4 : Vérification du fonctionnement
Depuis SSH :
```bash
curl http://localhost:8080
```
Depuis navigateur (via IP publique Azure) :
```
http://<IP_PUBLIQUE>:8080
```

## 6. Résultat attendu
L'installation initiale de WordPress s'affiche dans le navigateur. Après configuration (langue, titre du site, compte admin), on accède à l’interface d’administration WordPress (`/wp-admin`).

## 7. Captures à insérer ici :
- docker ps (affichage des conteneurs actifs)
- docker logs wordpress (vérification d’erreurs Apache)
- curl http://localhost:8080 (depuis SSH)
- Affichage de l’installation WordPress dans navigateur
- Interface WordPress après connexion

## 8. Problèmes rencontrés et solutions
- **Port 80 déjà utilisé** → Changement du port publié à 8080
- **502 Bad Gateway avec Nginx** → Suppression de Nginx, utilisation d'Apache intégré
- **Connexion impossible depuis navigateur** → Ajout manuel d’une règle NSG dans Azure pour autoriser le port 8080

## 9. Conclusion
Ce projet m’a permis de :
- Prendre en main Docker et Docker Compose pour le déploiement d’applications web
- Travailler sur un environnement cloud distant (Azure)
- Résoudre des erreurs concrètes (réseau, ports, services)
- Documenter chaque étape de manière professionnelle

L’environnement est désormais opérationnel, et WordPress est accessible en ligne.

Auteur : Ruben Arnald Hombessa Massamouna
Test MSc Cybersécurité – Cybersup
