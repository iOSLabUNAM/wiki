---
title: Solid
category: design patterns
---
# S.O.L.I.D.

## Single Responsibility

Establece que cada módulo debe tener una responsabilidad única, lo cual significa que tiene que ser altamente cohesivo e implementar una logica fuertemente relacionada.

### Ejemplo

#### Malo
```swift
class PlaceOrder {
  let product: Product
  init(product: Product) {
    self.product = product
  }

  func run() {
    // 1. Lógica relacionada a verification
    //    de disponibilidad en inventario
    // 2. Lógica relacionada a procesamiento de pago
    // 3. Lógica relacionada a procesamiento de envio
  }
}
 ```

#### Bueno

```swift
class PlaceOrder {
  let product: Product
  init(product: Product) {
    self.product = product
  }

  func run() {
    StockAvailability(product: self.product).run()
    ProductPayment(product: self.product).run()
    ProductShipment(product: self.product).run()
  }
}
```

## Open Closed Principle

Establece que los modulos de software deben estar abiertos para extensión, pero cerrados para modificación; es decir, que un modulo de este tipo puede permitir que su comportamiento se amplíe sin modificar su implementación.

### Ejemplo

#### Malo

```swift
class Logger {
  init(loggingForm: String) {
    self.loggingForm = loggingForm
  }

  func log(message: String) {
    switch self.loggingForm {
      case "console":
        print(message)
      case "file":
        DiskStore().write("logs.txt", message: message)
    }
  }
}
```
#### Bueno

```swift
protocol Logger {
  func log(_ message: String)
}

class EventTracker {
  let logger: Logger
  init(logger: Logger) {
    self.logger = logger
  }

  func log(message: String) {
    self.logger.log(message)
  }
}

class ConsoleLogger: Logger {
  func log(_ message: String) {
    print(message)
  }
}

class FileLogger: Logger {
  func log(_ message: String) {
      DiskStore().write("logs.txt", message: message)
  }
}
```

## Liskov Subtitution Principle

Se define como una extensión del 'Open Closed Principle' que establece que las nuevas clases derivadas que extienden la clase base no deberían cambiar el comportamiento de la clase base (comportamiento de los métodos heredados). Siempre que una clase Y sea una subclase de la clase X, cualquier instancia que haga referencia a la clase X también debería poder hacer referencia a la clase Y (los tipos derivados deben ser completamente sustituibles por sus tipos base).

### Ejemplo

#### Malo

```swift
class Rectangle {
  let width: Int
  let height: Int
  init(width: Int, height: Int) {
    self.width = width
    self.height = height
  }

  mutating func setWidth(width: Int){
    self.width = width
  }

  mutating func setHeight(height: Int) {
    self.height = height  
  }
}

class Square: Rectangle {
  // Violación LSP: clase heredada sobrescribe comportamiento del padre

  override func setWidth(width: Int){
    super.setWidth(width: width)
    self.width = width
  }

  override func setHeight(height: Int) {
    super.setHeight(height: height)
    self.height = height
  }
}
```

## Interface Segregation Principle

Establece que ningún cliente debe ser obligado a depender de los métodos que no usa. El ISP divide las interfaces que son muy grandes en otras más pequeñas y más específicas para que los clientes solo tengan que conocer los métodos que les interesan. Estas interfaces reducidas también se denominan interfaces de rol. Este principio está destinado a mantener un sistema desacoplado y, por lo tanto, más fácil de refactorizar, cambiar y redistribuir.

### Ejemplo

#### Malo

```swift
protocol Car {
  func open()
  func startEngine()
  func changeEngine()
}

// ISP violation: La instancia Driver
// no hace uso de #changeEngine
class Drive {
  func takeARide(car: Car) {
    car.open()
    car.startEngine()
  }
}

// ISP violation: La instancia Mechanic
// no hace uso de #startEngine
class Mechanic {
  func repair(car: Car) {
    car.open()
    car.changeEngine()
  }
}
```

## Dependency Inversion Principle

Se refiere a una forma específica de desacoplar los módulos de software. Al seguir este principio, las relaciones de dependencia convencionales establecidas desde módulos de alto nivel de configuración de políticas a módulos de dependencia de bajo nivel se invierten, lo que hace que los módulos de alto nivel sean independientes de los detalles de implementación del módulo de bajo nivel. El principio establece:

  - *Los módulos de alto nivel no deben depender de módulos de bajo nivel. Ambos deben depender de las abstracciones.*
  - Las abstracciones no deben depender de los detalles. Los detalles deben depender de las abstracciones.


### Ejemplo

#### Malo

```swift
class EventTracker {
  let logger: ConsoleLogger
  init() {
    // Una instancia de bajo nivel ConsoleLogger
    // es directemente creade dentro de una de alto nivel.
    // La clase EventTracker aumenta el acoplamiento
    self.logger = ConsoleLogger.new
  }

  func log(message: String) {
    self.logger.log(message)
  }
}
```

#### Bueno

```swift
protocol Logger {
  func log(_ message: String)
}

class EventTracker {
  let logger: Logger
  init(logger: Logger = ConsoleLogger()) {
    self.logger = logger
  }

  // Por medio de injección de dependencias en el
  // Open Closed Principle
  func log(message: String) {
    self.logger.log(message)
  }
}
```
