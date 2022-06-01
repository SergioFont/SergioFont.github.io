---
typora-copy-images-to: ../assets/img
typora-root-url: ../
layout: post
categories:
conToc: true
title: Seguridad en Docker
---

# Seguridad en Docker

Para esta práctica haremos uso de Trivy3, cuya funcionalidad es la de escanear vulnerabilidades



Si realizamos un primer escaneo con trivy nos mostrará un panel con todas las vulnerabilidades enontradas. Nosotros lo haremos sobre la app log4shell

```bash
trivy config .
```

![image-20220601095106097](/assets/img/image-20220601095106097.png)



A continuación probaremos con una imagen de Wordpress antigua.

```bash
syft log4shell -o cyclonedx-xml > Syft-BOM
```

![image-20220601095416507](/assets/img/image-20220601095416507.png)



La escaneamos con Grype

```bash
grype sbom:Syft-BOM
```

![image-20220601095445920](/assets/img/image-20220601095445920.png)



Y si vamos al Dependency track, después de crear el respectivo proyecto podremos comprobar la vulnerabilidades que nos detecta

![image-20220601095616234](/assets/img/image-20220601095616234.png)




