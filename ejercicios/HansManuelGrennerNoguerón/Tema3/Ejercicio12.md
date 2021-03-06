**Crear una imagen con las herramientas necesarias para el proyecto de la asignatura sobre un sistema operativo de tu elección.**

Al desarrollarse la aplicación usando Ubuntu partimos de dicho sistema operativo. Creamos el Dockerfile asociado a la aplicación.

```
FROM ubuntu
MAINTAINER Hans Manuel Grenner Noguerón <juanmagnc@gmail.com>

#Instalar Python con todas las dependencias y git

RUN apt-get update
RUN apt-get -y install python python-setuptools build-essential python-dev git git-core
RUN easy_install pip

# Instalamos MongoDB

RUN \
  apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10 && \
  echo 'deb http://downloads-distro.mongodb.org/repo/ubuntu-upstart dist 10gen' > /etc/apt/sources.list.d/mongodb.list && \
  apt-get update && \
  apt-get install -y mongodb-org && \
  rm -rf /var/lib/apt/lists/*

# Clonamos el repositorio

RUN git clone https://github.com/enpi/ProjectCC.git

# Instalamos las dependencias del proyecto

RUN easy_install web.py
RUN easy_install mako
RUN easy_install pymongo
RUN easy_install feedparser
RUN easy_install tweepy
```

Dado que se encuentra conectado el repositorio de Github del proyecto con Docker podemos obtener y desplegar la imagen anterior mediante:

```
docker pull enpi/projectcc
docker run -t -i enpi/projectcc
```

