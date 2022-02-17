---
typora-copy-images-to: ../assets/img
typora-root-url: ../
layout: post
categories:
conToc: true
title: Jenkinsfile
---

# Creación Jenkinsfile



Creamos el fichero Jenkinsfile en la raíz del proyecto

```groovy
pipeline {
     agent any
     stages {
          stage("Compile") {
               steps {
                    sh "./gradlew compileJava"
               }
          }
          stage("Unit test") {
               steps {
                    sh "./gradlew test"
               }
          }
     }
}
```


Subimos la pipeline al github

```bash
git add .
git commit -m "Jenkinsfile"
git push
```



Cambiamos la secuencia pipeline a SCM

![image-20220217092700394](/assets/img/image-20220217092700394.png)

Dentro de build.gradle añadimos:

```bash
apply plugin: "jacoco"
```



Para generar un informe sobre la cobertura del código ejecutamos:

```bash
./gradlew test jacocoTestReport
```



Añadimos una etapa al archivo Jenkinsfile:

```bash
stage("Code coverage") {
     steps {
          sh "./gradlew jacocoTestReport"
          sh "./gradlew jacocoTestCoverageVerification"
     }
}
```



Publicamos el informe de cobertuar de código de Jenkins

```groovy
stage("Code coverage") {
     steps {
          sh "./gradlew jacocoTestReport"
          publishHTML (target: [
               reportDir: 'build/reports/jacoco/test/html',
               reportFiles: 'index.html',
               reportName: "JaCoCo Report"
          ])
          sh "./gradlew jacocoTestCoverageVerification"
     }
}
```



Añadimos el "Checkstyle" dentro de config/checkstyle/checkstyle.xml

```xml
<?xml version="1.0"?>
<!DOCTYPE module PUBLIC "-//Checkstyle//DTD Checkstyle Configuration 1.3//EN" "https://checkstyle.org/dtds/configuration_1_3.dtd">

<module name="Checker">
  <property name="charset" value="UTF-8" />

  <property name="severity" value="error" />

  <!-- Checks for whitespace                               -->
  <!-- See http://checkstyle.org/config_whitespace.html -->
  <module name="FileTabCharacter">
    <property name="eachLine" value="true" />
  </module>
</module>
```



Volvemos al build.gradle para añadir el checkstyle

```bash
apply plugin: 'checkstyle'
```



Añadimos una etapa de análisis estático

```groovy
stage("Static code analysis") {
     steps {
          sh "./gradlew checkstyleMain"
     }
}
```



Y publicamos el informe en jenkins

```groovy
stage("Static code analysis") {
     steps {
          sh "./gradlew checkstyleMain"
          publishHTML (target: [
             reportDir: 'build/reports/checkstyle/',
             reportFiles: 'main.html',
             reportName: "Checkstyle Report"
          ])
     }
}
```



Para que no dé errores eliminaremos los tabs que hayan en CalculatorApplication.java

```java
package com.victor.calculator;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class CalculatorApplication {

    public static void main(String[] args) {
        SpringApplication.run(CalculatorApplication.class, args);
    }

}
```

