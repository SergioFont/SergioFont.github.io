---
typora-copy-images-to: ../assets/img
typora-root-url: ../
layout: post
categories:
conToc: true
title: Imagen Privada
---

# Imagen privada

Creamos una imagen privada y la subimos las imagen a DockerHub

Iniciamos minikube

```bash
minikube start
```


Creamos el secreto en base al siguiente comando

```bash
kubectl create secret docker-registry sergiofont --docker-server=https://index.docker.io/v1/ --docker-username=sergiofont --docker-password=hola --docker-email=alufon090@ieselcaminas.org
```



Si hubiesemos creado algun secreto anteriormente utilizar el siguiente comando para borrarlo

```bash
kubectl delete secret sergiofont
```



Aplicamos el comando anterior con:

```bash
kubectl apply -f .
```



Para ver todos los pods que se han iniciado:

```bash
kubectl get all
```



Para borrar los pods:

```bash
kubectl delete -f .
```



Seleccionaremos un pod para mandarlo al puerto 8080:80

```bash
kubectl port-forward pod/deployment-b7c4f57b-t5qwj 8080:80
```



Para montar una imagen usaremos 

```dockerfile
docker build .
```



Con docker build -t le especificaremos la imagen que queremos seleccionar

```bash
docker build -t sergiofont/chapter2:latest
```



Y para aplicar los cambios en base al image.yaml utilizaremos: 

```bash
kubectl apply -f ./images.yaml
```

