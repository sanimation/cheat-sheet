# Docker CheatSheet

## IMAGES

### Rechercher Images Dans Le Repo Docker Public

```
$ docker search image_name:stable
```

### Charger Image Debian:Stable depuis Le Repo Docker Public

```
$ docker pull image_name:stable
```

### Lister les images

```
$ docker images
$ docker images -a
```
-a, --all            Show all images (default hides intermediate images)

### Supprimer une image

```
$ docker rmi image_id_or_image_name
```

### Supprimer toutes les images

```
$ docker rmi $(docker images -a -q)
```
-q, --quiet          Only show numeric IDs

Enregistrer les modif dans l'image

```
$ docker commit image_name Modif_name
```

## CONTAINER

### Lister tous les conteneurs

```
$ docker ps -a
$ docker ps -l 
```

--all , -a		Show all containers (default shows just running)
--latest , -l		Show the latest created container (includes all states

### Lister les conteneurs actifs

```
$ docker ps
```

### Stopper un conteneur efficlloud-00

```
$ docker stop efficlloud-00
```

### Mettre en pause un conteneur efficlloud-00

```
$ docker pause efficlloud-00
```

### Supprimer un conteneur efficloud-00

```
$ docker rm efficloud-01
```

### Supprimer tous les conteneurs

```
$ docker rm $(docker ps -a -q)
```

### Détail sur un conteneur

```
$ docker inspect "container_id"
```

### Lancer un container de nom efficloud-01 depuis l'image efficloud_template en mode interactif avec renvoi de port 22

```
$ docker run -i --name efficloud-01 -p 2221:22 -t efficloud_template /bin/bash
```

### Lancer un container de nom efficloud-02 depuis l'image efficloud_template en mode daemon avec renvoi de port 22

```
$ docker run -d --name efficloud-02 -p 2222:22 efficloud_template
```

### Lancer un container de nom efficloud-03 depuis l'image efficloud_template en mode daemon avec ....

```
$ docker run -d -P --name efficloud-03 efficloud_template
```

### Savoir sur quel port du host est redirigé le port 22 du Container efficloud-03

```
$ docker port efficloud-03 22
```

### Lancer un container de nom efficloud-04 depuis l'image efficloud_template en mode interactif avec renvoi de port 22 et mount vol

```
$ docker run -i --name efficloud-04 -p 2224:22 -v /DockerData:/datapps -t efficloud_template /bin/bash
```

### Monter dossier /export de host dans dossier /datapps du container

```
$ docker run -d -p 2222:22 -v /export:/datapps container_id
```

### Voir la sortie d'un container executer en mode Detached

```
$ docker logs [Container iD]
$ docker logs -f [Container iD]
$ docker logs container_name | tail
```

```
$ docker -diff container
```

### S'attacher à un container

```
$ docker attach efficloud-01
$ docker attach debian-01 —sig-proxy=false 75
```

### Se détacher du container
Ctrl-p + Ctrl-q

### Se connecter en SSH au container efficloud-04

```
$ ssh -p 2224 root@localhost
```

### Lancer une commande sur un container actif

```
$ docker exec -d container_name touch /tmp/myfile
$ docker exec -it container_name /bin/bash
```

## DOCKERFILE

### Création de son Dockerfile pour une image que l'on nommera efficloud-template

```
$ mkdir -p /var/lib/docker/image/efficloud-template
$ cd /var/lib/docker/image/efficloud-template

$ touch Dockerfile

$ ls

$ sudo nano dockerfile
```

```
MAINTAINER : nom et mail de mainteneur du conteneur
FROM : image de base (ubuntu, debian)
VOLUME : Point de montage
RUN : commande à exécuter pour installer le conteneur.
ENTRYPOINT : commande qui s’exécute au démarrage du conteneur (une seule sera exécutée).
CMD : commande qui s’exécute au démarrage du conteneur.
ADD : Copier un fichier du répertoire courant dans le filesystem du conteneur.
USER : utilisateur qui exécute les commandes dans le conteneur.
EXPOSE : Port(s) à exposer à l’exterieur.
DIFF:
```

### Construire son Image 

```
$ docker build -t efficloud_template -f dockerfile . (Le Point est important à la fin)
```

## Docker attach

By ID

```
$ sudo docker attach <container-id>
```

or by Name

```
$ sudo docker attach <container-name>
```

```
$ root@<container-id>:/# 
```

UPDATE: (docker >= 1.3) If we use attach we can use only one instance of shell. So if we want open new terminal with new instance of container's shell, we just need run the following:

By ID

```
$ sudo docker exec -it <container-id> /bin/bash
```

or by Name

```
$ sudo docker exec -i -t <container-name> /bin/bash
```

```
$ root@<container-id>:/#
```

# Docker Compose CheatSheet

## Deploying changes
When you make changes to your app code, you’ll need to rebuild your image and recreate your app’s containers. To redeploy a service called web, you would use:

`$ docker-compose build web`

`$ docker-compose up --no-deps -d web`

This will first rebuild the image for web and then stop, destroy, and recreate just the web service. The --no-deps flag prevents Compose from also recreating any services which web depends on.

# Connect to Docker MySQL container from localhost?

## Using docker-compose up

Since you published port 3306 on your docker host, from that host itself you would connect to `127.0.0.1:3306`.

## Using docker-compose run

In that case the port mapping section of the docker-compose.yml file is ignored. To have the port mapping section considered, you have to add the --service-ports option:

```
docker-compose run --service-ports db
```

## Additional note

Beware that by default, the mysql client tries to connect using a unix socket when you tell it to connect to localhost. So do use 127.0.0.1 and not localhost:

```
$ mysql -h 127.0.0.1 -P 3306 -u root
```

Welcome to the MySQL monitor. Commands end with ; or \g. Your MySQL connection id is 1 Server version: 5.6.26 MySQL Community Server (GPL)

Copyright (c) 2000, 2015, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its affiliates. Other names may be trademarks of their respective owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql>


```
$ mysql -h localhost -P 3306 -u root
```

ERROR 2002 (HY000): Can't connect to local MySQL server through socket '/var/run/mysqld/mysqld.sock' (2)

# Install Docker Ubuntu 1604

```
$ sudo apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
$ echo "deb https://apt.dockerproject.org/repo ubuntu-xenial main" | sudo tee /etc/apt/sources.list.d/docker.list
$ sudo apt-get install linux-image-extra-$(uname -r) linux-image-extra-virtual
$ sudo apt-get update
$ sudo apt-get install docker-engine
$ sudo service docker start
$ sudo usermod -aG docker $USER
$ members docker

$ sudo nano /etc/default/grub
	GRUB_CMDLINE_LINUX="cgroup_enable=memory swapaccount=1"
$ sudo update-grub
$ reboot
```

# Start Docker on Boot

```
$ sudo systemctl enable docker
$ docker info
```

# Upgrade Docker

```
$ sudo apt-get upgrade docker-engine
```

# Uninstall Docker

```
$ sudo apt-get purge docker-engine
$ sudo apt-get autoremove --purge docker-engine (suppression Docker + dépendances)
$ rm -rf /var/lib/docker (Suppression  images, containers et volumes)
```

# Fichier de Configuration de Docker

```
$ cd /var/lib/docker
$ vim /etc/default/docker.io
```

# Install Docker CentOS-7

# Update CentOS

```
$ sudo yum update
```

# Create file /etc/yum.repos.d/docker.repo

```
$ sudo tee /etc/yum.repos.d/docker.repo <<-'EOF'
[dockerrepo]
name=Docker Repository
baseurl=https://yum.dockerproject.org/repo/main/centos/7/
enabled=1
gpgcheck=1
gpgkey=https://yum.dockerproject.org/gpg
EOF
```

# Update CentOS

```
$ sudo yum update
```

# Install Docker

```
$ sudo yum install docker-engine
```


# Enable Docker service 

```
$ sudo systemctl enable docker.service
```

# Start Docker

```
$ sudo systemctl start docker
```

# Check docker

```
$ sudo docker search nginx
```

# Add user localadmin to docker group

```
$ sudo usermod -aG docker localadmin
```

# Start Docker on Boot

```
$ sudo systemctl enable docker
```



