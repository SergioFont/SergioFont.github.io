---
typora-copy-images-to: ../assets/img
typora-root-url: ../
layout: post
categories:
conToc: true
title: Practica Jenkins Calculadora

---

# Instalación de Jenkins / Calculadora

Creamos y preparamos el directorio a enlazar con jenkins

```bash
mkdir $HOME/jenkins_home
sudo chown 1000 $HOME/jenkins_home
sudo chmod 777 $HOME/jenkins_home
docker run -d -p 49001:8080 -v $HOME/jenkins_home:/var/jenkins_home --name jenkins jenkins/jenkins:lts-jdk11
```

Entramos en el navegador con la url: http://localhost:49001/

Creamos el usuario y una nueva pipeline con el siguiente código

![image-20220215092714701](/assets/img/image-20220215092714701.png)

![image-20220215092855259](/assets/img/image-20220215092855259.png)

A continuación crearemos una nueva pipeline llamada calculator con el siguiente contenido:

![image-20220215093738893](/assets/img/image-20220215093738893.png)

Iremos a la página start.spring.io donde nos generará un proyecto Gradle personalizado.

Dentro del gradle.build modificamos la versión:

```bash
id 'org.springframework.boot' version '2.6.2'
```

Y compilamos con ./gradlew compileJava

![image-20220215094303048](/assets/img/image-20220215094303048.png)

Hecho esto procederemos a editar los ficheros que nos permitirán mostrar el calculo.

Dentro de src/main/java/com/victorponz/calculator editaremos tanto Calculator.java como CalculatorController.java, respectívamente.

```java
package com.SergioFont.calculator;
import org.springframework.stereotype.Service;

@Service
public class Calculator {
     int sum(int a, int b) {
          return a + b;
     }
}
```

```java
package com.SergioFont.calculator;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

@RestController
class CalculatorController {
     @Autowired
     private Calculator calculator;

     @RequestMapping("/sum")
     String sum(@RequestParam("a") Integer a, 
                @RequestParam("b") Integer b) {
          return String.valueOf(calculator.sum(a, b));
     }
}
```

Ejecutamos ./gradlew bootRun en la raíz de la carpeta principal.

![image-20220215095044374](/assets/img/image-20220215095044374.png)

Si vamos al navegador a la url http://localhost:8080/sum?a=1&b=2:

![image-20220215095151468](/assets/img/image-20220215095151468.png)

