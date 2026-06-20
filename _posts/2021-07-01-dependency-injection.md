---
title: Inyeccion de depencendias
category: workflow
layout: post
----

# Inyeccion de dependencias 


Cuando se habla de calidad de codigo un punto importante (entre otros) es la testeabilidad modular del codigo, que hace parte de los principios de SOLID.


Para hablar de inyeccion de dependencias y su manenjo se tiene el siguente ejemplo practico que puede ser replacado en un playground:

```swift
func isRandomGreater(than value: Int) -> Bool {
    Int.random(in: 0...10) > value
}
```

Esta funcion simplemente retorna un boleano representando si cierto numero (aleatorio entre 0 y 10) es mayor al valor pasado como paramentro ```value```. Para ver claramente su funcionamiento, modifiquemos la funcion para imprimir el resultado cada que se llame la funcion:

```swift
@discardableResult
func isRandomGreater(than value: Int) -> Bool {
    if Int.random(in: 0...10) > value {
        print("true")
        return true
    } else {
        print("false")
        return false
    }
}
```

Cada vez que se llame la funcion ```isRandomGreater```, la consola imprimirá valores ```true``` o ```false``` aleatoriamente basado en el valor interno generado, por ejemplo:

```swift
isRandomGreater(than: 5)
```

Probablilisticamente, ```isRandomGreater``` imprimirá ```true``` aproximadamente la mitad de las veces que se ejecute. Si se ejecuta un loop con 10 elementos consecutivos:

```swift
(1...10).forEach { value in
    isRandomGreater(than: value)
}

```

En consola se imprimiria:

``` swift
false
true
false
true
false
true
true
false
true
false

```

Este output será diferente cada vez que se ejecute el codigo.

## Problematica 

La implementacion de ```isRandomGreater``` no es controlable debido a que depende de un valor random que se genera intermanente en el scope de la funcion. Esto es un problema cuando se habla de unit tests, donde la base es la habilidad de tener control total sobre el environment en el que se prueba la funcinalidad de cierta implementación, podiendo asi comprobar su correcta respuesta bajo condiciones muy especificas.

La solucion a este issue es el correcto manejo de dependencias, en este caso es claro que la dependencia de la funcion ```isRandomGreater``` es el generador aleatorio de numeros ```Int.random(in: 1...10)```, y es el elemento que debe ser controlado por inyeccion.

Existen multiples formas de inyectar dependencias, aqui se muestran 2:

## Closures

La inyeccion de dependencias evitará visualizar ```isRandomGreater``` como una caja negra que solo responde bajo una implementacion definida. En cambio, introducimos la propiedad ```randomizer``` como un closure que no toma parametros y retorna un ```Int```. Esta nueva propiedad puede ser asignada por default con el random generator original:

```swift
@discardableResult
func isRandomGreater(
    than value: Int,
    randomizer: () -> Int = { Int.random(in: 1...10) }
) -> Bool {
    if randomizer() > value {
        print("true")
        return true
    } else {
        print("false")
        return false
    }
}
```

el codigo anterior no modificaria las implementaciones que puedieran estar usando este proceso en un ambiente de produccion pues su llamado permanece igual:

```swift
(1...10).forEach { value in
    isRandomGreater(than: value)
}

```

pero provee la habilidad de forzar la salida deseada para comprobar su correcto funcionamiento en un unit test, sobreescribiendo la implementación de ```Int.random(in: 1...10)``` en el closure:

```swift
(1...10).forEach { value in
    isRandomGreater(than: value) { 11 }
}

```

logrando el control de la dependencia sabiendo asi que siempre que este codigo se ejecute, la respuesta será la misma:

```swift
true
true
true
true
true
true
true
true
true
true

```

## Protocols

Cuando se habla de escalabilidad, el closure injection prodria ser no suficiente, por lo que un metodo más socorrido es el de interface injection, que consiste en crear un protocolo que describa la dependencia a controlar. En este caso conservamos el nombre ```Randomizer``` pero esta vez como un protocolo que contiene la funcion ```random()```:


```swift
protocol Randomizer {
    func random() -> Int
}
```

al igual que en el metodo de closures, al trabajar con protocolos es posible asignar un default behavior extendiendo el protocolo:

```swift
extension Randomizer {
    func random() -> Int {
        Int.random(in: 1...10)
    }
}
```
Este protocolo permite desacoplar de funcionalidad para que multiples objetos la utlicen. Para este ejemplo se utlizaran dos implementaciones diferentes, una ```live``` que se utilizara en el codigo de produccion con el comportamiento default definido en la extension de ```Randomizer```. y una version ```mock``` que se utlizará en para controlar la dependencia en unit tests. Para la version live basta con crear una estructura que conforme ```Randomizer```:

```swift
struct LiveRandomizer: Randomizer {}
```

Ninguna otra modificacion es requerida pues ```Randomizer``` implementa un comportamiendo default para la funcion ```random()```, logrando de igual manera que las implementaciones de ```isRandomGreater``` no requieran modificacion:


```swift
@discardableResult
func isRandomGreater(
    than value: Int,
    randomizer: Randomizer = LiveRandomizer()
) -> Bool {
    if randomizer.random() > value {
        print("true")
        return true
    } else {
        print("false")
        return false
    }
}
```

Para la version ```mock``` se requiere una nueva estructura que conforme ```Randomizer``` usando una implementación diferente para la funcion ```random()``` haciendo que retorne siempre un valor asigado desde el ```init``` de la estuctura:

```swift
struct MockRandomizer: Randomizer {
    let output: Int

    init(output: Int) {
        self.output = output
    }
    
    func random() -> Int {
        output
    }
}
```

Esta estructura puede ahora ser llamada en unit tests que usen ```isRandomGreater``` de la siguiente manera:

```swift
(1...10).forEach { value in
    let mockRandomizer = MockRandomizer(output: 11)
    isRandomGreater(than: value, randomizer: mockRandomizer)
}
```

obteniendo la salida controlada:

```swift
true
true
true
true
true
true
true
true
true
true
```

### Summary
El control de dependencias es un must cuando se habla de codigo modular testeable (unit tests) sobre todo en casos donde esta dependencias mofician su comportamiento basado en muchos factores externos (otros buenos ejemplos de pedendencias pueden ser: ```ÙRLSession```, ```UserDefaults```, ```Date()```, etc). Aunque habrá casos donde la interconexion de modulos deba testearse con funcionalidad real de las dependencias (integration tests), usar inyeccion de de dependencias es una buena practica que ayuda a la organizacion y legibilidad de codigo en grandes equipos/proyectos.