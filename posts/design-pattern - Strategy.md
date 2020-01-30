---
title: Patron Strategy 
category: design patterns
draft: true
---

# Patron de diseño Strategy

Este patrón de diseño se centra en la creencia de que un algoritmo puede atacar diferentes problemas o eventualidades adaptandose a cada caso.

Un ejemplo clásico de este tipo de diseño es que imagines que eres un D.T de Fútbol, tu equipo tendrá diferentes estrategias a la hora de atacar, defender, cuando van ganando o cuando van perdiendo. Esto es en si el patrón de estategia, hacer "cosas diferentes" o en el caso de la programación algoritmos diferentes para cada escenario.

la definicion formal es la siguiente:

> Este patrón define un conjunto de algoritmos, encapsula cada uno de ellos y los hace intercambiables. Permite que el algoritmo pueda variar independientemente de los clientes que lo utilicen.

Esto quiere decir que nuestros objetos deben estar preparados para afrontar diversos contextos sin cambiar las interacciones de estos con el cliente.

## Modelo

El modelo general del algoritmo es el siguiente:

&nbsp;

![Modelo](https://codigolinea.com/wp-content/uploads/2015/03/strategy-uml.png)

Un poco confuso al principio pero se entenderá mejor si lo simplificamos y explicamos con el siguiente ejemplo de modelo:

&nbsp;

![Model2](https://miro.medium.com/max/1608/1*4vdmSjQVWuBF7C2ZGelfYA.png)

&nbsp;

Imagina que tu programa va a controlar la estrategia del equipo de fútbol que mencionamos antes, entonces cada estrategia deberá ser una formación diferente representada en este caso por un algoritmo. Basándonos en las circunstancias del juego tu programa deberá elegir que algoritmo de la formación es el indicado para el momento del juego, y eso es el patrón estrategia a grandes rasgos, lo que buscamos es que un controlador o incluso el mismo usuario tome la decisión de que estrategia usar a veces sin siquiera notarlo.

El patrón Strategy (estrategia) es una alternativa a la herencia, si estás pensando usar la herencia para poder agregar nuevos comportamientos a tus objetos, sería conveniente usar este patrón

Si dentro de tu clase haces uso intensivo de las condicionales `if`, `else`, `switch case`, eso quiere decir que tu clase tiene asignado muchos comportamientos y/o responsabilidades, lo cual suele ser un indicador de la necesidad aplicar el patrón Strategy (estrategia), para poder encapsular estos comportamientos y delegarlos a otra clase u objeto.

> Redacción para IOSLab 