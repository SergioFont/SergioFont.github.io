---
typora-copy-images-to: ../assets/img/
typora-root-url: ../
layout: post
categories: 
conToc: true
title: OWASP MASVS
---

# OWASP MASVS

## Estándar de Verificación de Seguridad de Aplicaciones Móviles



### V1: Requisitos de Arquitectura, Diseño y Modelado de Amenazas

1.4 MSTG-ARCH-4: Se identificó claramente la información considerada sensible en el contexto de la aplicación móvil

1.7 MSTG-ARCH-7: Todos los controles de seguridad poseen una implementados centralizada.



### V2: Requerimientos de Almacenamiento de datos y Privacidad

2.1 MSTG-STORAGE-1: Las funcionalidades de almacenamiento de credenciales del sistema deben de ser utilizadas para almacenar información sensible, tal como información personal, credenciales de usuario o claves criptográficas.

2.2 MSTG-STORAGE-2: No se debe almacenar información sensible fuera del contenedor de la aplicación o del
almacenamiento de credenciales del sistema.



### V3: Requerimientos de Criptografía

3.1 MSTG-CRYPTO-1: La aplicación no depende únicamente de criptografía simétrica cuyas claves se encuentran directamente en el código fuente de la misma.

3.2 MSTG-CRYPTO-2: La aplicación utiliza implementaciones de criptografía probadas.



### V4: Requerimientos de Autenticación y Manejo de Sesiones

4.5 MSTG-AUTH-5: Existe una política de contraseñas y es aplicada en el servidor.

4.6 MSTG-AUTH-6: El servidor implementa mecanismos, cuando credenciales de autenticación son ingresadas una cantidad excesiva de veces



### V5: Requerimientos de Comunicación a través de la red

5.4 MSTG-NETWORK-4: La aplicación utiliza su propio almacén de certificados o realiza pinning del certificado o la clave pública del servidor. Bajo ningún concepto establecerá conexiones con servidores que ofrecen otros certificados o claves, incluso si están firmados por una CA de confianza.

5.6 MSTG-NETWORK-6: La aplicación sólo depende de bibliotecas de conectividad y seguridad actualizadas.



### V6: Requerimientos de Interacción con la Plataforma

6.1 MSTG-PLATFORM-1: La aplicación requiere la cantidad de permisos mínimamente necesaria.

6.5 MSTG-PLATFORM-5: JavaScript se encuentra deshabilitado en los WebViews salvo que sea necesario.



### V7: Requerimientos de Calidad de Código y Configuración del Compilador

7.1 MSTG-CODE-1: La aplicación es firmada y provista con un certificado válido, cuya clave privada está debidamente protegida.

7.7 MSTG-CODE-7: Los controles de seguridad deniegan el acceso por defecto



### V8: Requerimientos de Resistencia ante la Ingeniería Inversa

8.1 MSTG-RESILIENCE-1: La aplicación detecta y responde a la presencia de un dispositivo rooteado, ya sea alertando al usuario o finalizando la ejecución de la aplicación.

8.3 MSTG-RESILIENCE-3: La aplicación detecta y responde a cualquier modificación de ejecutables y datos críticos de la propia aplicación.
