---
title: Particularidades del lenguaje Swift
category: swift
layout: post
---

# Particularidades del lenguaje swift

Swift, como cualquier lenguaje de programación tiene características que lo
hacen único, conocer dichas características es vital para generar código limpio,
eficiente y optimizado en este lenguaje. 

Por lo anterior, este post NO tiene como finalidad introducir al lector en los
fundamentos del lenguaje swift, sino que en lugar de eso buscar enlistar las
particularidades del lenguaje para saber que **herramientas tenemos disponibles
a la hora de programar**.


## Optional binding

_Optional binding_ permite encontrar su una _variable opcional_ contiene algún
valor, de ser así, este se pone disponiblem mediante una *constante* o variable
*temporal*

La técnica de optional binding se puede usar en `if`'s y en `while`'s

````swift
if let actualNumber = Int(possibleNumber) {
  print("Se pudo hacer el parseo")
  print("Ahora puedo usar el valor como actualNumber: \(actualNumber)")
} else {
  print("No se pudo realizar el parseo")
}
````

Se pueden poner varios _Optional binding_, cada uno separado por *comas*. Cada
coma se puede traducir a un "and"

Este snipet se vuelve inecesariamenent díficil de leer

````swift
if let firstNumber = Int("4") {
  if let secondNumber = Int("42") {
    if firstNumber < secondNumber && secondNumber < 100 {
      print("\(firstNumber) < \(secondNumber) < 100")
    }
  }
}
````

Una mejor forma de escribir lo anterior, sería de la siguiente forma:

````swift
if let firstNumber = Int("4"), let secondNumber = Int("42"), 
  firstNumber < secondNumber && secondNumber < 100 {
  print("\(firstNumber) < \(secondNumber) < 100")
}
````


## Nil-Coalescing Operator (`a ?? b`)

No existen una traducción adecuada pero, este operador hace lo siguiente:

_Desenvuelve_ un optional si es que contiene un valor, en caso contrario regresa
el valor por defecto (`b`).

El operador _nil-coalescing_ es un abreviación del código que se muestra a
continuación

````swift
a != nil ? a! : b
````

*Ejemplo*

````swift
let defaultColor = "red"
var userColor: String? //<1>

//Uso del operador
var layoutColor = userColor ?? defaultColor // <2>
````

* `<1>` Se declara como opcional y como no se le asigna un valor, por defecto se
inicializa con `nil`

* `<2>` La variable se inicializa con el color "red"


<!--## Rangos-->

<!--Swift permite crear los rangos que se muestran a continuación.-->

<!--* Rangos con _intervalo cerrado_-->
<!--* Rangos con _intervalo abierto_-->
<!--* Rangos de 1 solo lado (`names[2...]`)-->
<!--* Rangos "infinitos" (`range = [0...]`)-->

<!--## Strings (Cadenas)-->

<!--La característica más destacable es que _Swift_ utiliza *interpolación* de una-->
<!--manera muy sencilla.-->

## Arreglos

````swift
// Reemplazando 3 elementos del arreglo con solo 2: "Bananas" y "Apples"
shoppingList[4...6] = ["Bananas", "Apples"]
````

## Diccionarios

````swift
// Inicializando un diccionario
var namesOfIntegers = [Int: String]()
// Una forma de vaciar el diccionario
var namesOfIntegers2 = [:]
// Agregando un valor al diccionario
namesOfIntegers[16] = "sixteen"
````

## Switch

La sentencia `switch` es una de las sentencias más versátiles de Swift. `case`
puede recibir 

* Rangos, 
* Tuplas
* E inclusive puedes hacer _value binding_

Notar que la palabra `break` no es necesaria en comparación con otros lenguajes
como C.

*Ejemplo de switch con tuplas*

````swift
let somePoint = (1, 1)
switch somePoint {
case (0, 0):
  print("\(somePoint) is at the origin")
case (_, 0):
  print("\(somePoint) is on the x-axis")
case (0, _):
  print("\(somePoint) is on the y-axis")
case (-2...2, -2...2):
  print("\(somePoint) is inside the box")
default:
  print("\(somePoint) is outside of the box")
}
// Prints "(1, 1) is inside the box"
````

## Guard (Salida anticipada)

Una sentencia `guard` es _muy_ similiar a un `if`. Sin embargo, se enlistan
algunas particularidades:

* La sentencia `guard` *siempre* se acompaña de la clausula `else`
* La sentencia `guard`, al igual que el `if`, requiere de una _condición
booleana_ para trabajar.

### Caso práctico

Para desenvolver opcionales.

Tenemos una función y en caso de que algún opcional tenga el valor `nil` podemos
terminar la función y regresar el control.

````swift
func greet(person: [String: String]) {
  guard let name = person["name"] else {
    return
  }

  print("Hello \(name)!")

    guard let location = person["location"] else {
      print("I hope the weather is nice near you.")
        return
    }

  print("I hope the weather is nice in \(location).")
}

greet(person: ["name": "John"])
// Prints "Hello John!"
// Prints "I hope the weather is nice near you."
greet(person: ["name": "Jane", "location": "Cupertino"])
// Prints "Hello Jane!"
// Prints "I hope the weather is nice in Cupertino."
````

## Funciones

En Swift, la sintaxis por defecto para crear funciones es la siguiente

````swift
func saludador(nombre:String, edad:Int) -> String {
  return "Hola soy \(nombre) y tengo \(edad) años"
}
````

Y para llamar a la función se hace siempre de la siguiente forma

````swift
saludo = saludador(nombre:"Rodrigo", edad:12)
````

### Etiquetas de argumentos y nombres de parámetros

* La etiqueta de argumento se utiliza cuando la función se manda a llamar.
* El nombre del parámetro se utiliza en la implementación de la función.

````swift
func greet(person: String, from hometown: String) -> String {
  return "Hello \(person)!  Glad you could visit from \(hometown)."
}
print(greet(person: "Bill", from: "Cupertino"))
// Prints "Hello Bill!  Glad you could visit from Cupertino."
````

### Omitiendo etiquetas de argumentos

````swift
func someFunction(_ firstParameterName: Int, secondParameterName: Int) {
    // In the function body, firstParameterName and secondParameterName
    // refer to the argument values for the first and second parameters.
}
someFunction(1, secondParameterName: 2)
````

### Parámetros de entrada y salida (In-out parameters)

Los parámetros pasados a las funciones son *constantes*, es decir, no podemos
modificar su valor.

Para poder modificar el parámetro que se le envía al usuario se utiliza la
clausula `inout`.


````swift
func swapTwoInts(_ a: inout Int, _ b: inout Int) {
    let temporaryA = a
    a = b
    b = temporaryA
}

var someInt = 3
var anotherInt = 107
swapTwoInts(&someInt, &anotherInt) //<1>
print("someInt is now \(someInt), and anotherInt is now \(anotherInt)")
// Prints "someInt is now 107, and anotherInt is now 3"
````
* `<1>` Observar que se requiere del _ampersand_ para indicar que el parámetro se
puede modificar.

En este caso, como parámetros no se pueden pasar _constantes_ o _literales_ ya
que no se pueden modificar su valor y por lo tanto habría un error.

### Function Type

Así como los enteros y los String son tipos de dato, existe también el tipo
"function".

Su utiliza es para poder asignar una función a una variable.


````swift
func addTwoInts(_ a: Int, _ b: Int) -> Int {
    return a + b
}

var mathFunction: (Int, Int) -> Int = addTwoInts //<1>

print("Result: \(mathFunction(2, 3))")
// Prints "Result: 5"
````
* `<1>` Ahora `mathFunction` tiene las mismas características que `addTwoInts`

### Function Types como tipos de parámetro

Esta característica de swift nos permite pasar una función como parámetro de
otra función como se muestra en el siguiente ejemplo:


````swift
func printMathResult(
    _ mathOperator: (Int, Int) -> Int, 
    _ a: Int, 
    _ b: Int
  ) {
  print("Result: \(mathOperator(a, b))")
}

///Pasamos como parametro la función definida anteriormente
print(MathResult(addTwoInts, 3, 5))
// Prints "Result: 8"
````

### Otras características de la funciones en swift

* Se pueden regresar una función de una función. Simplemente despues de `->` se
escribe la firma de función que queremos regresar.
* Se pueden crear funciones anidadas.

## Closures

Las closures *atrapan* y guardan referencias de cualquier constante y variable
del contexto en donde fueron definidas.

*Ejemplo de ordenamiento*


````swift
let nombres = ["Chris", "Alex", "Ewa", "Barry", "Daniella"]

// Primera forma de ordenamiento utilizando un closure
reversedNames = names.sorted(by: { (s1: String, s2: String) -> Bool in
  return s1 > s2
})

// Gracias a la inferencia de tipo se puede escribir de la sig. forma
reversedNames = names.sorted(by: { s1, s2 in return s1 > s2 } )

// Para una sola expresión se puede omitir la clausula return
reversedNames = names.sorted(by: { s1, s2 in s1 > s2 } )
````

### Nombre abreviados de argumentos

Los nombres de los parámetros se pueden omitir poniendo: `$0,$1,$2, ...`


````swift
reversedNames = names.sorted(by:{$0 > $1})
````

### Trailing closures


````swift
// Example of sorted 
reversedNames = names.sorted() { $0 > $1 }

// SI la  closure es el único parámetro de la función entonce se puede escrbir
// de la siguiente forma

reversedNames = names.sorted { $0 > $1 }

let strings = numbers.map { (number) -> String in
  // Cuerpo del closure
}
````

Otros ejemplos


````swift
// Una closure se escribe en su forma normal y la siguiente como trailing
// closure
func loadPicture(from server: Server, 
completion: (Picture) -> Void, onFailure: () -> Void) { 
  if let picture = download("photo.jpg", from: server) { 
    completion(picture)
  } else {
    onFailure()
  }
}

// 2 closure en su forma "trailing"
// La firma de la funcion 
// loadPicture(from:completion:onFailure:)
loadPicture(from: someServer) { picture in
  someView.currentPicture = picture
} onFailure: {
  print("Couldn't download the next picture.")
}
````

### Escapando Closures
Considerar la siguiente _closure_


````swift
var completionHandlers = [() -> Void]()
func someFunctionWithEscapingClosure(completionHandler: @escaping () -> Void) {
  completionHandlers.append(completionHandler)
}
````

*Explicación*

* `@escaping` es para indicar que la función se escapa
* Una closure se espaca cuando una pasa como argumento de una función pero se
invoca hasta que la función regresa.
* `someFunctionWithEscapingClosure(_:)` toma una closure como argumento y la
agregar a un arrego que es declarado fuera de la función.
* La función regresa después de iniciar la operación, pero no se llama a la
_closure_ hasta que se completa la operación.


### Auto closure

*Primer ejemplo: Lazy evaluation*

````swift
var customersInLine = ["Chris", "Alex", "Ewa", "Barry", "Daniella"]
print(customersInLine.count)
// Prints "5"

let customerProvider = { customersInLine.remove(at: 0) }
print(customersInLine.count)
// Prints "5"

print("Now serving \(customerProvider())!")
// Prints "Now serving Chris!"
print(customersInLine.count)
// Prints "4"
````

Otro ejemplo con el atributo `@autoclosure`



````swift
// customersInLine is ["Ewa", "Barry", "Daniella"]
func serve(customer customerProvider: @autoclosure () -> String) {
  print("Now serving \(customerProvider())!")
}
serve(customer: customersInLine.remove(at: 0))
// Prints "Now serving Ewa!"
````

.Explicación
* Con `@autoclosure` el argmento de la función se convierte en automático a una
closure.
* El objetivo es el mismo, retrasar la evaluación de cierta parte de código.

Los atributos `@autoclosure` y `@escaping` se pueden combinar.


## Enumerations

Cada llave de la enumeración no esta asociado a un entero sino más bien lo que
pasa es que al crear una enumeración se crea un nuevo tipo de dato.


````swift
enum CompassPoint {
    case north
    case south
    case east
    case west
}

var directionToHead = CompassPoint.west

directionToHead = .east //<1>
````
* `<1>` Se entiende que directionToHead es de tipo CompassPoint por lo que se
  puede usar la sintaxis `.east` para cambiar su valor

### Enumeraciones con valores asociados

Se explica mediante el siguiente ejemplo:


````swift
enum Barcode {
    case upc(Int, Int, Int, Int)
    case qrCode(String)
}

var productBarcode = Barcode.upc(8, 85909, 51226, 3)
````

### Raw values

Similar al ejemplo de _Valores asociados_, `swift` tiene la capacidad de asociar
valores a los casos al momento de crear la enumeración


````swift
enum ASCIIControlCharacter: Character { //<1>
  case tab = "\t"
  case lineFeed = "\n"
  case carriageReturn = "\r"
}
````
* `<1>` : Character` define el tipo de dato de cada uno de los casos de la
enumeración


### Enumeraciones recursivas

Son útiles para cuando en la enumeración necesitamos utilizar el propio nombre
de la enumeración en alguno de los casos. Ejemplo:


````swift
// Se puede definir de esta forma (con la palabra indirect en cada caso)
enum ArithmeticExpression {
  case number(Int)
  indirect case addition(ArithmeticExpression, ArithmeticExpression)
  indirect case multiplication(ArithmeticExpression, ArithmeticExpression)
}

// Ó con indirect al inicio de la enumeración
indirect enum ArithmeticExpression {
  case number(Int)
  case addition(ArithmeticExpression, ArithmeticExpression)
  case multiplication(ArithmeticExpression, ArithmeticExpression)
}
````

*Ejemplo* de uso de la enumeración descrita en la parte de arriba

````swift
// Ejemplo de uso
let five = ArithmeticExpression.number(5)
let four = ArithmeticExpression.number(4)
let sum = ArithmeticExpression.addition(five, four)
let product = ArithmeticExpression.multiplication(sum,
  ArithmeticExpression.number(2)) 

func evaluate(_ expression: ArithmeticExpression) -> Int {
    switch expression {
    case let .number(value):
        return value
    case let .addition(left, right):
        return evaluate(left) + evaluate(right)
    case let .multiplication(left, right):
        return evaluate(left) * evaluate(right)
    }
}

print(evaluate(product))
// Prints "18"
````
