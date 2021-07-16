---
title: Deployar tu proyecto a Heroku
category: workflow
author: Galileo Garibaldi
layout: post

---

# Subiendo mi proyecto a Heroku

En éste pequeño artículo hablaremos de como deployar nuestro proyecto a la plataforma de Heroku. Para ello necesitaremos el código ya hecho, este puede ser el que tu desees, sin embargo aquí se usará el código en la parte de *Referencias*, el cuál está programado en Python

## 1.1- Jerarquía de archivos

Hasta ahorita, tenemos la siguiente estructura de archivos

![16](file:///Users/galigaribaldi/Documents/PPropios/Diplo2/wiki/assets/img/Heroku/16.png?lastModify=1626464952)

Para poder subir nuestro proyecto a heroku, necesitaremos los siguientes archivos:

1. Archivo de funcionamiento (código en Python):

   1. En este caso, el archivo de funcionamiento principal es nuestro archivo **app.py**

   2. Archivo de requerimientos (Archivo *.txt*):

      1. Este archivo es el que generamos en la sección 2, sin embargo puedes volver a generarlo o actualizarlo con el comando:

         ```shell
         pip3 freeze > requirements.txt.txt
         ```

   3. Archivo de configuración (*Procfile*): Archivo de configuración que usará heroku para saber quee *dyno* o que arhcivo debe correr como principal

      1. ```shell
         echo "web: gunicorn app:app" > Procfile
         ```

         Esto generará un archivo sin extensión de nombre **Procfile**, el cual debe de contener como única línea *web: gunicorn app:app*

      2. Entorno Virtual a usar (*carpeta generada con venv*): Este entorno es la carpeta de configuración que anteriormente ya hicimos.

      Una vez teniendo todos los archivos listos, nos dirigiremos a nuestra cuenta de Heroku y nos iremos al menú **Deploy**, es importante tener en cuenta unas cuantas cosas

      ![17](file:///Users/galigaribaldi/Documents/PPropios/Diplo2/wiki/assets/img/Heroku/17.png?lastModify=1626464952)

      

      

## 1.2 Instalando Heroku en nuestra computadora

Necesitaremos una instalación de Heroku CLI, el cual básicamente, es un cliente de heroku con el cual podremos deployar nuestro proyecto. Para ello, dejaré el enlace de instalación [Enlace Descarga - Instalación Heroku](https://devcenter.heroku.com/articles/heroku-cli).

## 1.3 Heroku Git (Con ningún repositorio creado)

En esta opción asumimos o decimos que no tenemos una cuenta de github con nuestro nombre o bien, decidimos que nuestro código no se alojará en Github, si este es el caso, Heroku nos proporcionará un reposotior externo cone l único fin de poder Deployar nuestro proyecto.

```shell
git init
```

```shell
heroku git:remote -a appdiplomado
```

```shell
git add .
```

```shell
git commit -am "make it better"
```

```shell
git push heroku master
```

## 1.4 Heroku Git - Github (Teniendo un repositorio Creado)

![18](file:///Users/galigaribaldi/Documents/PPropios/Diplo2/wiki/assets/img/Heroku/18.png?lastModify=1626464952)

La opcón mas recomendable es tener un repositorio en Github previamente cargado, lo que hará esta opción, será ligar una de nuestras ramas de Github (recomendablemente la master) a nuestro alojamiento en heroku, de manera tal, que si *commiteamos y pusheamos* a nuestro repo, este tambiñen se actualziará en nuestra app de heroku

En este caso nis iremos a el apartado *Github Connect to Github* y elegiremos el repsositorio y la rama que querramos

![19](file:///Users/galigaribaldi/Documents/PPropios/Diplo2/wiki/assets/img/Heroku/19.png?lastModify=1626464952)

Después elegiremos la rama a la cual estará asociado y por último daremos en **Enable Automatic Deploys**

**Opcion 1:** Lo último que haremos será commitear y pushear un cambio a nuestra app

```shell
git add .
```

```shell
git commit -m "Deploy to Heroku"
```

```shell
git push
```

**Opcion 2:** Podemos bajar y darle en *Deploy Manually* y procederá a hacer Deploy

## 1.5 Errores posibles durante el Deploy

Si lllega a ocurrir un error duramte el deploy, es importante checar lo siguiente:

1. Tener a la misma altura los archivos de *app.py*, *Procfile*(sin extension) y *requiriments.txt*

2. En caso de que el error nos salte que no puede encontrar una versión de Python, teclear los siguientes comandos

   1. ```shell
      heroku buildpacks:set heroku/python
      ```

      ```shell
      heroku buildpacks:set heroku/python --app appdiplomado
      ```

      ```shell
      git push heroku main
      ```

   2. O bien, irse a la interfaz gráfica en el menú de settings (Página web de Heroku) y configurar un python package

      ![20](file:///Users/galigaribaldi/Documents/PPropios/Diplo2/wiki/assets/img/Heroku/20.png?lastModify=1626464952)

      ![21](file:///Users/galigaribaldi/Documents/PPropios/Diplo2/wiki/assets/img/Heroku/21.png?lastModify=1626464952)

   3. Una vez hecho este cambio nos dirigiremos a las opciones Deploy y volveremos a deployar

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
- [Documentación Flask](