# Prise de Connaissance avec Jenkins

```bash
docker run --rm -v "${PWD}:/app/rest-service" -w /app/rest-service  maven:3.9.5-amazoncorretto-17 mvn compile
```


```bash
docker exec -it -u root awesome_golick bash
```

```bash
apt update -y
apt install maven
```

# Exécuter les jobs dans un conteneur

```bash
docker network create jenkins
```

```bash
docker run --name jenkins-docker --rm --detach   --privileged --network jenkins --network-alias docker   --env DOCKER_TLS_CERTDIR=/certs   --volume jenkins-docker-certs:/certs/client   --volume jenkins-data:/var/jenkins_home    docker:dind --storage-driver overlay2
```

```Dockerfile
FROM jenkins/jenkins:latest
USER root
RUN apt-get update && apt-get install -y lsb-release ca-certificates curl &&     install -m 0755 -d /etc/apt/keyrings &&     curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc &&     chmod a+r /etc/apt/keyrings/docker.asc &&     echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc]     https://download.docker.com/linux/debian $(. /etc/os-release && echo \"$VERSION_CODENAME\") stable"     | tee /etc/apt/sources.list.d/docker.list > /dev/null &&     apt-get update && apt-get install -y docker-ce-cli &&     apt-get clean && rm -rf /var/lib/apt/lists/*
USER jenkins
RUN jenkins-plugin-cli --plugins "docker-workflow json-path-api"
```

```bash
docker build -t myjenkins-docker:latest .
```

```bash
docker run --name jenkins --restart=on-failure --detach   --network jenkins --env DOCKER_HOST=tcp://docker:2376   --env DOCKER_CERT_PATH=/certs/client --env DOCKER_TLS_VERIFY=1   --publish 8080:8080 --volume jenkins-data:/var/jenkins_home   --volume jenkins-docker-certs:/certs/client:ro   myjenkins-docker:latest
```

```bash
docker compose up -d --build
```


# Brancher un nouvel agent SSH

Etapes

1. Trouver une image pour créer un node agent
1. Ajouter un service docker compose pour représenter tous ces agents
1. Installer l'extension ssh-slaves depuis le Dockerfile
1. Configurer depuis le node principal la connexion vers ces nouveaux node agent
1. Forcer l'exécution des jobs sur ces nouveaux node agent

Pour générer une paire de clés privé/publique

```bash
ssh-keygen
```