---
title: Librerias de terceros (3rd party libraries)
category: workflow
layout: post
---

Siempre es importante considerar que en muchas de las ocaciones en los que enfrentamos problemas a resolver alguien mas lo ha resuelto de una manera mas sencilla y optima. Y que muchas veces no necesitamos reinventar el hilo negro. Para ello existen diversar formas de inegrar librerias de terceros(3rd party libraries) a nuestro proyecto.

## Cocoapods
![cocoapods](https://user-images.githubusercontent.com/214138/31425761-36d45884-ae26-11e7-8d41-7420eaf6e456.png)

Es un manejador de paquetes **centralizado** escrito en ruby. Que a traves de un `Podfile` nos permite agregar diversos **pods** a un `workspace` donde se encuentra nuestro proyecto y el proyecto de Pods. Algunos dicen que cocapods es muy intrusivo, al tener la necesidad de crear un workspace por nosotros, sin embargo es gracias a esto que con un par de comandos podemos tener todo nuestro ambiente integrado.

### Instalacion

Para instalar desde cero se requiren dependencias de `hombrew` y `ruby`. Aqui puedes seguir los siguientes pasos

```shell
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)";
brew update;
brew upgrade;
brew install ruby;
gem install cocoapods --no-doc;
pod setup;
```

### Uso
Una vez instalado en tu ambiente local, se puede general el `Podfile` con el comando

```shell
pod init
```

Una vez creado el archivo podemos agregar las dependencias que creamos necesarias para nuestro proyecto. Y para instalamos solo ejecutamos

```shell
pod install
```

Este comando generara/actualizara el `xcworkspace` por lo que se recomienda abrir el proyecto una vez instalados los pods.

## Carthage
![carthage](https://user-images.githubusercontent.com/214138/31425812-70ca6466-ae26-11e7-8f90-57a7b11b3147.png)


A diferencia de cocoapods, Carthage es un sistema de paquetes **descentralizado** escrito en swift y mucho menos intrusivo, por lo que su instalacion es mas rapida y nos permite una mayor customizacion. La desventaja es que algunas 3rd party libraries solo usan cocoapods, aunque los proyectos con mas traccion tienden a incluir ambos.

### Instalacion

Para instalar carthage solo se requiere tener `homebrew`

```shell
brew install carthage
```

## Swift Package Manager

El manejador de paquetes de Swift es una herramienta para la gestión de la distribución de código Swift. Está integrado con el sistema Swift para automatizar el proceso de descargar, compilar y vincular las dependencias. El gestor de paquetes se incluye en Swift 3.0 y superiores.
