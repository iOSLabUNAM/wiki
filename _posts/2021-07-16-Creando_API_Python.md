---
title: Creando API con Python y Flask
category: workflow
author: Galileo Garibaldi
layout: post

---

## Heroku

En este pequeño artículo - Tutorial, veremos como crear una API en Python. **Importante: Ésto lo haremos con el lenguaje de programación *Python V3.8***

## 1.- Configurando Python

Ya que tenemos nuestra cuenta creada, crearemos un entorno virtual de python con las siguientes líneas de comando

```bash
pip3 install venv
python3 -m venv entorno
source entorno/bin/activate
pip install --upgrade pip
```

De esta forma conseguiremos estar en un pequeño entorno virtual, el cual es como una burbuja dentro de python, el cual nos permite configurar la máquina virtual de python. Para mayores referencias, consultar el siguiente [enlace](https://docs.python.org/es/3/tutorial/venv.html)

Una vez teniendo configurado nuestro entorno virtual, proccederemos a instalar las librerías necesarias, éstas se describen a continuación

1. Flask: Framework de mini Aplicaciones Web

   1. ```bash
      pip3 install flask
      ```

2. Gunicorn: Librería de interacción con Heroku

   1. ```bash
      pip3 install gunicorn
      ```

3. Psycopg2: Librería interna para el manejo de *Postgres*

   1. ```bash
      pip3 install psycopg2
      pip3 install psycopg2-binary
      ```

4. Pandas: Librería para el manejo de datos

   1. ```
      pip3 install pandas
      ```

5. Requirements.txt: Esta no es una librería, si no un archivo de configuración que creareamos con los siguientes comandos:

   1. ```bash
      pip3 freeze > requirements.txt
      ```

      Este Archivo nos servirá para la configuración en heroku, este contiene las librerías y configruaciones que hemos hecho hasta ahora. **Importante: Cada vez que se instale una nueva librería, éste archivo deberá actualizarse, escribiendo el comando anteriormente mencionado**

## 3.- Empezamos a codificar

### 3.1 Primeros pasos

Una vez que tenemos todo listo, es hora de empezar a codificar. 

Lo primero que haremos será crear nuestra aplicación de forma sencilla y correrla en el navegador

```python
from flask import Flask
##Importamos la librería Flask
app = Flask(__name__)
##Creamos nuestra app

##Creamos nuestro primer decorador, lo que nos permite crear la ruta principal "/"
@app.route("/")
def hello():
    ##Le decimos a nuestra función que retorne "Hola mundo"
    return "Hola mundo"

if __name__ == "__main__":
    app.run(debug=True,port=5003)
```

¡De esta forma ya tenemos nuestra primera aplicación corriendo desde flask! Puedes checarlo tu mismo llendo a este enlace: http://127.0.0.1:5003, el cual es tu localhost

<img src="../assets/img/Heroku/2.png" alt="2" style="zoom:67%;" />

Sin embargo esto es aún muy poco útil, por lo que procederemos a poner un poco de sabor a las cosas

### 3.2 Configurando Templates

Hasta ahorita sólo tenemos algunos pocos archivos, **Nota: El archivo se debe llamar *requirements.txt***

<img src="../assets/img/Heroku/3.png" alt="3" style="zoom:90%;" />

Para este ejemplo implementaremos el modelo Vista - Controlador, por lo que crearemos 3 directorios mas

- Controllers: En este Directorio irá toda la configuración hacía la Base de datos **(Controlador)**

- static: En este directorio irá toda la configuración de archivos estáticos, tales como *css*, *js* o bien imágenes, se recomienda tener la siguiente jerarquía **(Vista)**

  - css
  - img
  - js

  **Vista de las carpetas dentro de static**

- templates: En este directorio se encuentran todos los archivos de tipo *.html* y plantillas **(Vista)**

**Vista de los archivos**

![4](../assets/img/Heroku/4.png)

Para este caso crearemos un archivo llamado **layout.html** dentro de la carpeta *templates*, el cual contendrá el contenido del siguiente [enlace](https://github.com/galigaribaldi/Python_Web/blob/heroku-proof/templates/layout.html).

Una vez teniendo nuestro **layout.html**, lo que haremos será crear una vista principal para nuestra api, esto lo lograremos poniendo un archivo dentro de nuestra carpeta **templates** llamado *index.html*.

```html
{% extends "layout.html" %} {% block content %}
<br><br><br><br><br><br>
<h1> Inicio </h1>
<br><br><br><br><br> 
{% endblock %}
```

**NOTA:** Quizás te estés preguntando por que este archivo luce tan raro, esto se debe a que se usó el archivo *layout.html*, como plantilla para poder heredarlo en el archivo *index.html*, este nos permite escribir menos código.

Una vez teniendo estas configuraciones del lado del front, empezaremos a configurar el archivo en el controlador, es decir el archivo *app.py*

```python
from flask import Flask
##Importamos la librería Flask
from flask import request, render_template, url_for

app = Flask(__name__)
##Creamos nuestra app

##Creamos nuestro primer decorador, lo que nos permite crear la ruta principal "/"
@app.route("/")
def hello():
    ##Le decimos a nuestra función que retorne el template index.html
    return render_template("index.html")
  
###Segunda ruta API
@app.route("/api")
def api():
    return "API"
if __name__ == "__main__":
    app.run(debug=True,port=5003)
```

### 3.3 Configurando nuestra ruta de API

Para este ejemplo usaremos una API de películas, está API tendrá la siguiente estructura:

1. ID Película: Tipo de dato numérico, *int-integer*
2. Nombre Película: Tipo de dato Cadena, *str, character varying*
3. Nombre del director: Tipo de dato Cadena de texto, *str, character varying*
4. Actores principales: Tipo de dato Cadena de texto, *str, character varying*
5. Año de lanzamiento: Tipo de dato Cadena de texto, *str, character varying*
6. Trama: Tipo de dato Cadena de texto, *str, character varying*
7. Imagen de portada: Tipo de dato Cadena de texto, *str, character varying*

En python tenemos un tipo de dato que se asemeja al *JSON*, el cual son los diccionarios, su estructura es básicamente *llave-valor*

```python
### De esta forma crearemos un diccionario con 1 solo dato
dicccionario = {
        "ID": 1,
        "Nombre_Pelicula": "Amelie",
        "Nombre_director":"Jean-Pierre Jeunet",
        "Actores_principales":"Audrey Tautou, Mathieu Kassovitz",
        "anio_lanzamiento":"2001",
        "trama":"""Amelie no es una chica como las demás.
                Ha visto a su pez de colores deslizarse hacia las alcantarillas municipales, 
                a su madre morir en la plaza de Notre-Dame y a su padre dedicar todo su afecto a un gnomo de jardín. 
                De repente, a sus veintidós años, descubre su objetivo en la vida: arreglar la vida de los demás. 
                A partir de entonces, inventa toda clase de estrategias para intervenir, sin que se den cuenta,
                en la existencia de varias personas de su entorno."""
    }
```

Configuraremos nuestro archivo de *app.py*, para que pueda mandar este diccionario como un archivo Json, ésto lo haremos con la librería *jsonify*.

```python
from flask import Flask
##Importamos la librería Flask
from flask import request, render_template, url_for
from flask import jsonify
app = Flask(__name__)
##Creamos nuestra app

##Creamos nuestro primer decorador, lo que nos permite crear la ruta principal "/"
@app.route("/")
def hello():
    ##Le decimos a nuestra función que retorne "Hola mundo"
    return render_template("index.html")

@app.route("/api")
def api():
    dicccionario = {
        "ID": 1,
        "Nombre_Pelicula": "Amelie",
        "Nombre_director":"Jean-Pierre Jeunet",
        "Actores_principales":"Audrey Tautou, Mathieu Kassovitz",
        "anio_lanzamiento":"2001",
        "trama":"""Amelie no es una chica como las demás.
                Ha visto a su pez de colores deslizarse hacia las alcantarillas municipales, 
                a su madre morir en la plaza de Notre-Dame y a su padre dedicar todo su afecto a un gnomo de jardín. 
                De repente, a sus veintidós años, descubre su objetivo en la vida: arreglar la vida de los demás. 
                A partir de entonces, inventa toda clase de estrategias para intervenir, sin que se den cuenta,
                en la existencia de varias personas de su entorno."""
    }
    return jsonify(dicccionario)
if __name__ == "__main__":
    app.run(debug=True,port=5003)
```

Si nos vamos a la ruta http://127.0.0.1:5003/api, podremos visualizar nuestro resultado

<img src="../assets/img/Heroku/6.png" alt="6" style="zoom:80%;" />

### 3.4 Configurando nuestra BD en Postgres Heroku

Para este punto nos iremos a la pantalla principal de heroku y daremos en **New** y en **Create a New App**

![7](../assets/img/Heroku/7.png)

Pondremos de nombre *appdiplomado* y elegiremos como region USA.

<img src="../assets/img/Heroku/8.png" alt="8" style="zoom:80%;" />

Esto nos mandará a la pantalla principal de Heroku y nos dará la opción de elegir un deployamiento (subir nuestro código a la nube), pero para este punto sólo elegiremos el menú de **Resources** y después **Find More add-ons**

![9](../assets/img/Heroku/9.png)

Esto nos mandará a otra pantalla y bajaremos un poco hasta encontrar **Heroku Postgres** y después **Install Heroku Postgres**

![10](../assets/img/Heroku/10.png)

Finalmente nos aparacerá un menú donde elegiremos la app donde la pondremos y elegiremos el nombre de nuestra app, en este caso **appdiplomado** y elegir el plan **HobbyDev**, este nos dará un plan gratis con la capacidad de almacenar 10,000 registros, finalmente, damos en **Submit Order Form**

![11](../assets/img/Heroku/11.png)

<img src="../assets/img/Heroku/12.png" alt="12" style="zoom:67%;" />

Nos aparecerá la pantalla principal y daremos click en heroku postgress

<img src="../assets/img/Heroku/13.png" alt="13" style="zoom:80%;" />

Esto nos saltará al menú de la base, aquí nos iremos al menú **settings** y aquí tomaremos las claves de nuestra base y daremos click en **View Credentials**

<img src="../assets/img/Heroku/14.png" alt="14" style="zoom:80%;" />

De aquí tomaremos los siguientes datos

- Host
- Database
- User
- Port
- Password

**Importante:** Estas credenciales en el plan *hobby dev*, no son permamemtes, por lo que es importante revisar constantemente que estas sean válidas.

### 3.5 Configurando el acceso a nuestra base en Python

Ahora nos concentraremos en conectar la base de datos con nuestro código de python, esto lo haremos con ayuda del módulo *psycopg2*

Nos iremos a la carpeta *Controllers* y aquí crearemos un archivo llamado *modelsCreation.py* y otro llamado *modelsOperation.py*, para el primer archivo llamado *modelsCreation.py*, en el crearemos las tablas necesarias para crear nuestra API.

**En el siguiente código de modelsCreation.py, en el crearemos 3 funciones principales:**

- Creación de la base: Nombre de la función *creacion_base*
  - Entrada: NULL, no recibe argumento
  - Proceso: Crear la tabla **pelicula**, en la base datos
  - Salida: Null, hay argumentos de salida
- Inserción de registros:
  - Entrada: Tupla con el registro a insertar
  - Proceso: Inserción de datos en la BD
  - Salida: NULL
- Eliminar Tablas:
  - Entrada: Null
  - Proceso: Borrar tablas
  - Salida: Null

```python
# -*- coding: utf-8 -*-
import psycopg2
###################     Credenciales de la base       #####################
host = 'Host'
database = 'NombreDelaBase'
user = 'Usuario'
password = 'Password'
def creacion_base():
    conexion = psycopg2.connect(host=host, database=database, user=user, password=password)
    cursor = conexion.cursor()
    cursor.execute("""CREATE TABLE pelicula(
	                    movie_id serial PRIMARY KEY,
                    	movie_name character varying(100),
                    	director_name character varying(100),
                        principals_actors character varying(200),
                        movie_year character varying(100),
                        trama_movie character varying(400)
                    );
                   """)
    conexion.commit()
    cursor.close()
    conexion.close()
    
def insercion_datos(tupla):
    conexion = psycopg2.connect(host=host, database=database, user=user, password=password)
    cursor = conexion.cursor()
    cursor.execute("""INSERT INTO pelicula(movie_name,director_name, principals_actors,movie_year,trama_movie)
                   VALUES """+str((tupla)))
    conexion.commit()
    cursor.close()
    conexion.close()
    
def eliminar_Tablas():
    conexion = psycopg2.connect(host=host, database=database, user=user, password=password)
    cursor = conexion.cursor()
    cursor.execute("""DROP TABLE pelicula;
                   """)
    conexion.commit()
    cursor.close()
    conexion.close()
```

**Para el archivo modelsOperation.py, crearemos una función que traiga todos los registros, en este caso usaremos, la ayuda de módulo pandas para convertirlo en JSON**

```python
# -*- coding: utf-8 -*-
import psycopg2
import pandas as pd
###################     Credenciales de la base       #####################
host = 'host'
database = 'db'
user = 'user'
password = 'contraseña'

def consulta():
    query = "SELECT * FROM pelicula;"
    datos = pd.read_sql(query, con=psycopg2.connect(host=host, database=database, user=user, password=password))
    datos = datos.to_json()
    return datos
```



### 3.6 Configurando las rutas de nuestra API

En este punto está casi todo listo, agregaremos un par de rutas, las cuales harán posible la consulta hacía la API y la creación y/o eliminación de dicha tabla:

- Creación **(/api/CreacionTabla)**: En esta ruta importaremos la función *creacion_base()*, esta se hará posible poniendo las siguientes líneas de código:

  - ```python
    ###Importacion de la base
    import Controllers.modelsCreation as crear
    ### Crear base
    crear.creacion_base()
    ```

- Eliminar **(/api/EliminarTabla)**: Eliminar todas las tablas, **Importante: Esto eliminará todos los registros**

  - ```python
    ##Eliminar tablas
    crear.eliminar_Tablas()
    ```

- Insertar **(/api/Insert/register/<movie_name>/<director_name>/<principals_actors>/<movie_year>/<trama_movie>)**: En esta ruta tenemos que pasarle los siguientes parámetros:

  - Nombre de la película - **movie_name**: Este tipo de dato es *String*

  - Director Principal - **director_name**: Este tipo de dato es *String*

  - Actor principal - **principals_actors**: Este tipo de dato es *String*

  - Año de la película - **movie_year**: Este tipo de dato es *String*

  - Trama de la película - **trama_movie**: Este tipo de dato es *String*

    - En esta sección, se necesita pasarle por medio de la URL los parámetros, y después leerlos con ayuda de la librería *request*

    - Por último, se redirigirá a la ruta *api*, la cual se define a continuación

    - ```python
      @app.route("/api/Insert/register/<movie_name>/<director_name>/<principals_actors>/<movie_year>/<trama_movie>")
      def inserts(movie_name,director_name, principals_actors,movie_year,trama_movie):
          ###Leer datos
          movie_name = request.args.get('movie_name',movie_name)
          director_name = request.args.get('director_name',director_name)
          principals_actors = request.args.get('principals_actors',principals_actors)
          movie_year = request.args.get('movie_year',movie_year)
          trama_movie = request.args.get('trama_movie',trama_movie)
          ####CConvertir datos a tuplas
          tupla = (movie_name,director_name, principals_actors,movie_year,trama_movie)
          ###Meter datos
          crear.insercion_datos(tupla,)
          return redirect(url_for('api'))  
      ```

- Ver **(/api)**: En esta ruta se hará una consulta a la BD y se retornará un JSON

  - ```python
    @app.route("/api")
    def api():
        dicccionario = operaciones.consulta()
        return dicccionario
    ```

A cotinuación se presenta todo el código

```python
from flask import Flask
##Importamos la librería Flask
from flask import request, render_template, url_for,redirect
from flask import jsonify
##
import Controllers.modelsCreation as crear
##
import Controllers.modelsOperations as operaciones
app = Flask(__name__)
##Creamos nuestra app

##Creamos nuestro primer decorador, lo que nos permite crear la ruta principal "/"
@app.route("/")
def hello():
    ##Le decimos a nuestra función que retorne "Hola mundo"
    return render_template("index.html")

@app.route("/api")
def api():
    dicccionario = operaciones.consulta()
    return dicccionario

@app.route("/api/CreacionTabla")
def creacion():
    crear.creacion_base()
    return "Tablas Creadas Listo!"

@app.route("/api/EliminarTablas")
def eliminar():
    crear.eliminar_Tablas()
    return "Tablas Eliminadas"

##/api/Insert/register/Amelie/Jean_Pierre_Jeunet/Audrey_Totou/2001/El_fabuloso_destino_de_Amelie
##/api/Insert/register/Requiem_for_a_dream/Darren_Afronosky/Jared_Leto/2001/_
##/api/Insert/register/It/Darren_Afronosky/Jared_Leto/2001/_
@app.route("/api/Insert/register/<movie_name>/<director_name>/<principals_actors>/<movie_year>/<trama_movie>")
def inserts(movie_name,director_name, principals_actors,movie_year,trama_movie):
    ###Leer datos
    movie_name = request.args.get('movie_name',movie_name)
    director_name = request.args.get('director_name',director_name)
    principals_actors = request.args.get('principals_actors',principals_actors)
    movie_year = request.args.get('movie_year',movie_year)
    trama_movie = request.args.get('trama_movie',trama_movie)
    ####CConvertir datos a tuplas
    tupla = (movie_name,director_name, principals_actors,movie_year,trama_movie)
    ###Meter datos
    crear.insercion_datos(tupla,)
    return redirect(url_for('api'))  
if __name__ == "__main__":
    app.run(debug=True,port=5003)
```

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