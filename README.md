# KUBERNETES PARTIE II - PROJET - DEVOPS - Orchestration - Jidel Louison

# Jidel 5SRC

# Objectif


### Ce projet à pour objectif de déployer et orchestrer trois applications conteneurisées dans un

### cluster Kubernetes Minikube pour l’entreprise fictive IC GROUP :

## Étapes de déploiement

### 1. Préparation de l'environnement

### Dans un premier temps, j'ai préparé l'environnement en installant les outils nécessaire pour le

### bon fonctionnement du projet

### Outils essentiels et commandes d'installation

**Outil Commande d’installation**

**curl** sudo apt install curl -y`

**Git** sudo apt install git - y

**Docker** sudo^ apt^ install^ - y^ docker.io``sudo systemctl enable docker``sudo systemctl start
docker``sudo usermod - aG docker $USER

**kubectl** curl - LO "https://dl.k 8 s.io/release/$(curl - Ls
https://dl.k 8 s.io/release/stable.txt)/bin/linux/amd 64 /kubectl"``sudo install - o r
root - m 0755 kubectl /usr/local/bin/kubectl

### Un site vitrine Flask personnalisable via des variables d'environnement

### L’ERP Odoo 13 connecté à une base PostgreSQL

### pgAdmin pour l'administration graphique de la base de données


**Outil Commande d’installation**

**Minikube** curl - LO
https://storage.googleapis.com/minikube/releases/latest/minikube_latest_amd 64 .deb
dpkg - i minikube_latest_amd 64 .deb

### Vérification après installation

**Outil Commande**

**Minikube** minikube version

**kubectl** kubectl version - -client

**Docker** docker - -version

**Git** git - -version

### Lancement de Minikube

### Puis pour lancer minikube j'ai utilisé la commande :

### **2. Clonage du repository GitHub**

### J’ai récupéré le projet en faisant un fork du repo : https://github.com/OlivierKouokam/mini-

### projet-5esgi et je me suis placé dans le répertoire Kubernetes :

```
minikube start
```
```
git clone https://github.com/Vaksalan/mini-projet- 5 esgi.git
```

### **3. Conteneurisation de l'application web**

### 3.1 - Pour la conteneurisation, j'ai en premier lieu créé un Dockerfile :

```
FROM python: 3. 6 - alpine
WORKDIR /opt
ENV ODOO_URL=http://odoo.local PGADMIN_URL=http://pgadmin.local
COPY..
RUN pip install flask== 1. 1. 2
EXPOSE 8080
ENTRYPOINT ["python", "app.py"]
```
### 3.2 - Puis, j'ai exécuté les commandes suivante pour build l'image

```
cd mini-projet- 5 esgi/kubernetes
```
```
docker build - t ic-webapp: 1. 0.
docker run - d -p 8080 : 8080 \
```
- eODOO_URL=https://www.odoo.com \
- ePGADMIN_URL=https://www.pgadmin.org \
- -name test-ic-webapp ic-webapp


### 3.3 - Et enfin, j'ai push l'image sur DockerHub à l'aide des commandes suivantes :

```
docker login
docker tag ic-webapp: 1. 0 vsritharan/ic-webapp: 1. 0
docker push vaksalan 25 /ic-webapp: 1. 0
```

### https://hub.docker.com/repository/docker/vaksalan25/ic-webapp/general

### **4. Déploiement des ressources Kubernetes**

### Voici les fichiers que j’ai utilisés pour construire cette infrastructure

**Fichier Rôle**

```
namespace.yaml Création du namespace icgroup
odoo.yaml Déploiement et NodePort Odoo
pgadmin-configmap.yaml Injection de servers.json dans pgAdmin
pgadmin.yaml Déploiement de pgAdmin
postgresql.yaml Déploiement et service PostgreSQL
webapp-config.yaml Variables d’environnement de la webapp
webapp.yaml Déploiement de l’application Flask
```
### Vous pouvez retrouvez le contenu des fichiers .yaml sur : https://github.com/Vaksalan/mini-

### projet-5esgi/tree/main/kubernetes

### 4.1 - Ensuite, j’ai appliqué tous les fichiers YAML avec kubectl apply - f :


### 4.2 - Sécurisation des informations

### Pour sécuriser les informations sensibles de mon projet Kubernetes, j’ai utilisé un fichier

### secret.yaml qui me permet de stocker de manière masquée les identifiants et mots de

### passe nécessaires au fonctionnement d’Odoo, PostgreSQL et PGAdmin. Ce fichier contient

### des données encodées en base64, comme le mot de passe administrateur d’Odoo ou encore

### les identifiants de connexion à PGAdmin.

### secret.yaml :

```
apiVersion: v 1
kind: Secret
metadata:
name: app-secrets
namespace: icgroup
type: Opaque
data:
pgadmin-email: dnNyaXRoYXJhbkBteWdlcy 5 mcg== # vsritharan@myges.fr
pgadmin-password: YWRtaW 4 xMjM= # admin 123
postgres-password: b 2 Rvbw== # mypostgres
odoo-password: b 2 Rvbw== # odoo
```
### Pour l'appliquer dans Kubernetes j'ai effectué les étapes ci-dessous :

### 1. Application du secret avec kubectl

```
kubectl apply - f secret.yaml
```
### 2. Vérifier que le secret est bien créé :

```
kubectl get secrets - n icgroup
```

### **5. Vérification du déploiement**

### Pour m’assurer que tous les pods et services sont en place, j’ai utilisé :

## Accès aux applications

### 3. Affichage du contenu encodé

```
kubectl get secret app-secrets - n icgroup - o yaml
```
```
kubectl get all - n icgroup
```

### Après avoir récupéré l’IP du cluster avec minikube ip, j’ai pu accéder aux services :

**Application URL**

Webapp [http://](http://) 192. 168. 58. 2 : 30080

Odoo [http://](http://) 192. 168. 58. 2 : 30069

pgAdmin [http:/](http:/) 192. 168. 58. 2 : 30050

### **6. Test d'accès aux services**

### Webapp Flask :

### Le site vitrine Flask est fonctionnel et affiche dynamiquement les liens vers Odoo et pgAdmin

### Odoo:

### Odoo est connecté à PostgreSQL et permet de créer des bases


### PgAdmin:

### pgAdmin est préconfiguré grâce au fichier servers.json. Pour accéder à l’interface de

### pgAdmin, j’ai utilisé les identifiants définis dans le fichier secret.yaml`, qui

### contient l’email et le mot de passe encodés et injectés dans le déploiement.


## **7. Conclusion**

### Ce projet m’a permis de :

### Apprendre à orchestrer plusieurs conteneurs dans un environnement Kubernetes

### Utiliser les objets Secret, ConfigMap, NodePort, PVC, etc.

### Comprendre comment connecter plusieurs services entre eux dans un cluster
