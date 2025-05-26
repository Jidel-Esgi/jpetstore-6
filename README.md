# KUBERNETES PARTIE II - CC - REVERSE ENGINEERING - Voting App

# Objectif


### Le but de ce projet était de déployer l'application open-source Example Voting App sur un

### cluster Kubernetes local via Minikube. J'ai ensuite vérifié que le système de vote fonctionne

### correctement et que les résultats apparaissent en temps réel.

## Architecture de l'application

### Voici le schéma que j’ai réalisé pour illustrer les flux entre les composants, pour mieux

### comprendre le fonctionnement, j'ai analysé les rôles de chaque composant de l'application

### Voici ce que chaque service fait :

## Étapes de déploiement

### Comprendre le fonctionnement d’une application multi-conteneurs

### Tester la communication entre les différents services

### Documenter chaque étape avec des captures d’écran

### Proposer un schéma d’architecture pour mieux visualiser les interactions

### Une application web en Python (vote) permet de choisir une option

### Le service Redis récupère les votes temporairement

### Un worker .NET lit Redis et enregistre les votes dans PostgreSQL

### Enfin, l'interface result (Node.js) affiche en direct les résultats


### 1. Préparation de l'environnement

### Dans un premier temps, j'ai préparé l'environnement en installant les outils nécessaire pour le

### bon fonctionnement du projet

### Outils essentiels et commandes d'installation

#### Outil Commande d’installation

#### curl sudo apt install curl -y`

#### Git sudo apt install git - y

#### Docker sudo apt install - y docker.io``sudo systemctl enable docker``sudo systemctl start

```
docker``sudo usermod - aG docker $USER
```
#### kubectl curl - LO "https://dl.k^8 s.io/release/$(curl- Ls

```
https://dl.k 8 s.io/release/stable.txt)/bin/linux/amd 64 /kubectl"``sudo install - o r
root - m 0755 kubectl /usr/local/bin/kubectl
```
#### Minikube curl - LO

```
https://storage.googleapis.com/minikube/releases/latest/minikube_latest_amd 64 .deb
dpkg - i minikube_latest_amd 64 .deb
```
### Vérification après installation


#### Outil Commande

#### Minikube minikube version

#### kubectl kubectl version - -client

#### Docker docker - -version

#### Git git - -version

### 1. Lancer Minikube

### J’ai commencé par démarrer Minikube avec la commande suivante :

### 2. Cloner le projet Voting App

### Ensuite, j’ai forké le dépôt contenant les fichiers de déploiement YAML et je l'ai cloné sur ma

### machine :

#### minikube start

#### git clone https://github.com/Vaksalan/example-voting-app

#### cd example-voting-app/k 8 s-specifications


### 3. Appliquer les manifests Kubernetes

### J’ai déployé l’ensemble des services avec cette commande :

### 4. Vérifier les objets déployés

### Pour m’assurer que tout fonctionne bien, j’ai vérifié les pods et services :

#### kubectl create - f.

#### kubectl get all


### 5. Récupérer l’adresse IP du cluster Minikube

### J’ai utilisé cette commande pour connaître l’adresse IP de Minikube :

### 6. Accéder aux interfaces vote/result

### En utilisant l’IP récupérée précédemment et les NodePort associés aux services, j’ai pu

### accéder aux interfaces suivantes :

#### minikube ip

#### kubectl get svc

### vote : http://192.168.58.2:31000 

### result : http://192.168.58.2:31001


## Résultats obtenus
