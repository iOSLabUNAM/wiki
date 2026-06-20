---
title: Introducción a Heroku
category: workflow
author: Galileo Garibaldi
layout: post
---

## Heroku

En éste pequeño artículo hablaremos sobre la plataforma en la nube llamada Heroku.

### ¿Qué es Heroku?

Heroku es una plataforma de servicio de computación en la nube, ésta te permitirá, *en pocos pasos*, alojar tu código y permitir *deplyarlo* (desplegarlo en un servidor).

Heroku hacce énfasis en que necesitarás pocos pasos, ya que no es necesario configurar todos los pasos de un servidor a gran escala.

### ¿Cómo funciona Heroku?

Heroku funciona través de *Dynos*, estos *Dynos*, no son mas que pequeños contenedores, los cuales permiten a tu aplicación - Servicio, poder desplegarse ccon facilidad, seguridad y bajo la configuración que tu le digas. Todos estos *Dynos*, están basados en un UNIX y mas exáctamente en un sistema de tipo Debian

De manera análoga, Heroku, provee de una interfaz de mantenimiento en su página web, lo que hace posible que la administración del mismo sea manejable de mejor manera.

### ¿Que puedo hacer en Heroku

Heroku nos ofrece varios servicios que nos pueden ayudar en nuestra aplicación, a continuación se describen algunos de ellos:

- Heroku app
- Heroku Postgress
- Redis To go
- Redis Enterprise Cloud
- Apache Kafka
- SFTP to go
- MSSQL
- Buketeer
- JawsDB MySQL

Cada una de éstas tecnologías son configurables desde la interfaz web de heroku, o bien desde línea de comandos en la terminal

### Crear cuenta en Heroku

Lo primero que necesitaremos será crear una cuenta en la plataforma de [Heroku](https://www.heroku.com), en ella te pedirá llenar algunos datos de información personal. 

**NOTA: Si es tu primera vez trabajando con heorku te recomiendo poner en el campo *Company Name* la palabra *UNAM* y en *Role* el campo *Student* o bien *Hobbyst***

Para éste caso se pondrá *python* como lenguaje de programación principal **Aunque esto no significca que sólo construiremos aplicaciones en éste lenguaje, es sólo un parámetro para Heroku**

<img src="../assets/img/Heroku/1.png" alt="1" style="zoom:80%;" />

Posterior a esto, te pedirá confirmar tu correo electrónicco.

**NOTA: Heroku te pedirá ingresar una tarjeta de pago, esta puede ser de Débito o crédito, pero no se te hará ningún pago o coste, puedes estar tranquilo de que no se te cobrará al menos que así lo desees.**

### Referencias

#### Código de Github

El código se ha hecho parte por parte y se encuentra en el siguiente enlace, si gustas puedes mejorarlo. ¡Eres bienvenido!

https://github.com/galigaribaldi/Python_Web/tree/Deploy-Heroku

#### Liga de Heroku

El código se encuentra corriendo en el siguiente enlace: https://appdiplomado.herokuapp.com

#### Referencias Externas

- [Entornos Virtuales](https://docs.python.org/es/3/tutorial/venv.html)
- [Agregar Utilidades a Heroku](https://devcenter.heroku.com/categories/add-ons)
- [Documentación Oficial de Heroku](https://devcenter.heroku.com/categories/reference)
- [Documentación Flask](https://flask.palletsprojects.com/en/2.0.x/)
