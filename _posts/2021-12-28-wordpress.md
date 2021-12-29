---
typora-copy-images-to: ../assets/img
typora-root-url: ../
layout: post
categories:
conToc: true
title: Practica Wordpress
---

# Práctica Wordpress



## Primeros pasos

Creamos la estrutura de directorios en la cuál instalaremos Wordpress. Una vez hecho crearemos dentro un archivo .yml con el siguiente contenido:

```yaml
version: '3.3'
   
services:
   db:
     image: mysql:5.7
     volumes:
       - db_data:/var/lib/mysql
     restart: always
     environment:
       MYSQL_ROOT_PASSWORD: somewordpress
       MYSQL_DATABASE: wordpress
       MYSQL_USER: wordpress
       MYSQL_PASSWORD: wordpress
   
   wordpress:
     depends_on:
       - db
     image: wordpress:latest
     ports:
       - "8000:80"
     restart: always
     environment:
       WORDPRESS_DB_HOST: db:3306
       WORDPRESS_DB_USER: wordpress
       WORDPRESS_DB_PASSWORD: wordpress
       WORDPRESS_DB_NAME: wordpress
volumes:
    db_data: {}

```
Debería de quedar tal que así:

![image-20211229102743898](/assets/img/image-20211229102743898.png)

Ejecutamos el comando docker compose para iniciar el .yml

```bash
docker-compose up -d
```

![image-20211229104122308](/assets/img/image-20211229104122308.png)



Si vamos al navegador y ponemos la dirección **http:localhost:8000** nos aparecerá la pantalla de instalación de Wordpress

![image-20211229104431080](/assets/img/image-20211229104431080.png)

