---
title: MVC
category: design patterns
layout: post
---
# Modelo Vista Controlador (MVC)

![mvc](https://user-images.githubusercontent.com/214138/31826728-78c93230-b57b-11e7-91b0-378d358cfb58.png)

El Modelo Vista Controlador es el mas comun de todos y ampliamente usado en backend frameworks como ruby on rails, django, swing, entre otros. Este patron separa la aplicacion en tres componentes principales:

- **Modelo(Model)** es la capa de abstraccion que connecta con nuestra `data source` ya sea una base de datos o una API. Y en general esta capa contiene nuestra logica de negocio.
- **Vista(View)** es la capa de abtracion que interactua con el usuario y contiene a los componentes visuales.
- **Controlador(Controller)** esta capa tiene la funcion de conectar la interaccion de las vistas con los modelos, y viceversa.

Dentro de MVC se busca que nuestro controladores tengan la menor cantidad de codigo(thin controller) y que la logica de este se encuentr en los modelos(fat models)
