---
title: Solid
category: annex
---
# S.O.L.I.D.

## Single Responsibility

Este practica nos dicta que cada componente de desarrollo deve tener una sola responsabilidad. Esto nos ayuda a mantener nuestra aplicacion modular y escalable. Digamos que tenemos un controller que nos muestra un panel de control y para renderizarlo necesita realizar 20 requests a la base de datos y una API. Bajo este principio se buscaria que dicho controllador solo tuviera los request minimos para su funcionamiento inical y el resto separarlo en controladores aparte y los componentes de UI hacen los requests asyncronamente a estos.

## Open Closed Principle

## Liskov Subtitution Principle

## Interface Segregation Principle

## Dependency Inversion Principle
