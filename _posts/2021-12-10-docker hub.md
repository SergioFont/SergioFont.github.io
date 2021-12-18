---
typora-copy-images-to: ../assets/img
typora-root-url: ../
layout: post
categories:
conToc: true
title: Practica Docker Hub
---

# Práctica Docker Hub



## Subir la imagen



Iniciamos sesión en dockerhub desde la consola de comandos

```bash
docker login
```
![image-20211218101704563](/assets/img/image-20211218101704563.png)



Preparamos la imagen para que sea aceptada en el registro público

```bash
docker tag chapter2 sergiofont/chapter2:latest
```
![image-20211218101733145](/assets/img/image-20211218101733145.png)



Y subimos las imagenes a Docker Hub con la orden:

```bash
docker push sergiofont/chapter2:latest
```
![image-20211218101801172](/assets/img/image-20211218101801172.png)



Nos vamos a Docker Hub, donde dentro de repositorios, encontraremos nuestra imagen ya subida

![1KYXJ7XRfF0GJBSB4yxJV4n92Y3ZEs87P](/assets/img/1KYXJ7XRfF0GJBSB4yxJV4n92Y3ZEs87P)
