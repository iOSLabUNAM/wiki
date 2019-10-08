---
title: Solid
category: annex
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
    // 1. Logic related to verification of stock availability
    // 2. Logic related to payment process
    // 3. Logic related to shipment process
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

Establece que "los modulos de software deben estar abiertos para extensión, pero cerradas para modificación"; es decir, que una entidad de este tipo puede permitir que su comportamiento se amplíe sin modificar su comportamiento.

## Liskov Subtitution Principle

Indica que, en un programa de computadora, si S es un subtipo de T, entonces los objetos de tipo T pueden reemplazarse con objetos de tipo S (es decir, un objeto de tipo T puede sustituirse por cualquier objeto) de un subtipo S) sin alterar ninguna de las propiedades deseables del programa (corrección, tarea realizada, etc.).

## Interface Segregation Principle

Establece que ningún cliente debe ser obligado a depender de los métodos que no usa. El ISP divide las interfaces que son muy grandes en otras más pequeñas y más específicas para que los clientes solo tengan que conocer los métodos que les interesan. Estas interfaces reducidas también se denominan interfaces de rol. Este principio está destinado a mantener un sistema desacoplado y, por lo tanto, más fácil de refactorizar, cambiar y redistribuir.

## Dependency Inversion Principle

Se refiere a una forma específica de desacoplar los módulos de software. Al seguir este principio, las relaciones de dependencia convencionales establecidas desde módulos de alto nivel de configuración de políticas a módulos de dependencia de bajo nivel se invierten, lo que hace que los módulos de alto nivel sean independientes de los detalles de implementación del módulo de bajo nivel. El principio establece:

  - Los módulos de alto nivel no deben depender de módulos de bajo nivel. Ambos deben depender de las abstracciones.
  - Las abstracciones no deben depender de los detalles. Los detalles deben depender de las abstracciones.
