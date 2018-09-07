---
title: Desarrollo Orientado a Pruebas
category: workflow
---

# Desarrollo Orientado a Pruebas (Test Driven Development)

El desarrollo orientado a pruebas o como se le conoce en sus siglas en ingles **TDD** (Test Driven Development) es una metodologia de desarrollo que se basa en la repetición de un ciclo de desarrollo corto: primero el desarrollador escribe una prueba automatizada *(inicialmente falla)* que define un feature deseado, luego produce el código minimo para pasar esa prueba, y finalmente refactoriza el código a un estándar aceptable.

Generalmente se sigue la siguiente secuencia de pasos:
* Añadir una prueba
* Ejecutar todas las pruebas y ver si la nueva falla
* Escribir un código
* Ejecutar pruebas
* Refactorizar el código
* Repetir

![tdd](https://user-images.githubusercontent.com/214138/31112342-c2d994d8-a7d8-11e7-884b-7a5fb596dff0.png)

---
## Recursos
- [TDDExampleSwift](https://github.com/iOSLabUNAM/TDDExampleSwift) : Ejemplo de TDD con swift, e integracion con [travis CI](https://travis-ci.org)
- [XCode8 y Swift 3](https://medium.com/@Dougly/unit-tests-and-test-driven-development-xcode-8-and-swift-3-f6d43ecd4bd4)
