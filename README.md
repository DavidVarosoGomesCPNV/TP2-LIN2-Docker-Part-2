# LIN2-TP2-Docker

#### Setup

##### Modification code app.py

`import os`

`client = MongoClient(db, 27017)`

##### Docker Compose 

```docker
#Final
# docker-compose up -d

version: '3'
networks:
  net:
    ipam:
      config:
      - subnet: 10.10.10.0/24
services:
  mongo:
    image: "mongo:3.2"
    container_name: mongo
    restart: unless-stopped
    networks:
      net:
        ipv4_address: 10.10.10.10
    ports:
      - 27017:27017
  app:
    image: auggus/tpdockerv2:v0.3
    container_name: tp2docker
    restart: unless-stopped
    environment:
      - DB=10.10.10.10
    ports:
      - 5000:5000
    depends_on:
      - "mongo"
    networks:
      net:
        ipv4_address: 10.10.10.11
```

##### Image

`docker image tag 3746 auggus/tpdockerv2:v0.3`

`docker push auggus/tpdockerv2:v0.2`

Link : https://hub.docker.com/repository/docker/auggus/tpdockerv2/general
