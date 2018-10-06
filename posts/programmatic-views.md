---
title: Vistas Programaticas
category: ios
---

# Vistas Programaticas

Todos los elementos del utilizados en el interface builder, tanto en Storyboards y Xibs
corresponden a objetos del UIKit, por lo tanto pueden ser instanciables y extensibles desde codigo.

## Herencia

Se puede crear una clase heredada de clases de CocoaTouch, con la cual se pueden
sobre escribir los inicializadores
  - `init(frame: CGRect)` crea a partir de un CGRect
  - `init?(coder aDecoder: NSCoder)` crea apartir de un objecto NSCoder, generalmente este metodo es llamado cuando el Storyboard inicializa el objeto.
Ademas de ello se puede tener un inicializador de conveniencia con un `CGRect.zero`

```swift
  class MyView: UIView {
    convenience init() {
      self.init(frame: .zero)
    }

    override init(frame: CGRect) {
        super.init(frame: frame)
        setupAutoLayout()
    }

    required init?(coder aDecoder: NSCoder) {
        super.init(coder: aDecoder)
        setupAutoLayout()
    }

    func setupAutoLayout(){
      // here goes my code
    }
  }
```

## Setup UIView objects

Dado que todos los elementos del UIView heredan del mismo cuentan con attributos que nos
permiten customizar de la misma manera que lo hariamos en el interface builder.

```swift
  let iv = UIImageView(frame: .zero)
  iv.image = UIImage(named: "tacocat")!
  iv.contentMode = .scaleAspectFit
  iv.backgroundColor = .purple
```

## Constraint

Para crear constraints es necesario establecer `translatesAutoresizingMaskIntoConstraints` en `false` en cada uno de los objectos a agregar a la vista, ya que sin ello los constraint no aplicaran a ese objeto.

```swift
  iv.translatesAutoresizingMaskIntoConstraints = false
```

Una vez condigurado nuesto objecto, devemos agregarlo como Subview

```swift
  view.addSubview(imageView)
```

Esto seria el similar al agregar un objecto en el interface builder sin establecer un constraint.
Para crear un constraint por medio de codigo es necesario agregar el siguiente codigo

```swift
  let constraint = imageView.topAnchor.constraint(equalTo: self.topAnchor)
```

Sin embargo nuestro constraint no esta listo, ya que necestamos explicitamente decir que sea activado

```swift
  constraint.activate = true
```

En ejemplos en linea es mas comun encontrarlo asi

```swift
  imageView.topAnchor.constraint(equalTo: self.topAnchor).activate = true
```

Sin embargo al realizar constraints de esta manera se convierte repetitivo, para una estraegia DRY
se puede utilizar `NSLayoutConstraint` quien a travez del metodo activate, activa una lista de constraints.

```swift
  NSLayoutConstraint.activate([
      imageView.topAnchor.constraint(equalTo: self.topAnchor),
      imageView.leadingAnchor.constraint(equalTo: self.leadingAnchor),
      imageView.trailingAnchor.constraint(equalTo: self.trailingAnchor),
      imageView.bottomAnchor.constraint(equalTo: self.bottomAnchor)
      ])
```

Por lo tanto nuesto archivo final quedaria de la siguiente forma

```swift
//  CatView.swift
import UIKit

class CatView: UIView {
    private let imageView: UIImageView = {
        let iv = UIImageView(frame: .zero)
        iv.image = UIImage(named: "tacocat")!
        iv.contentMode = .scaleAspectFit
        iv.translatesAutoresizingMaskIntoConstraints = false
        return iv
    }()

    convenience init() {
        self.init(frame: .zero)
    }

    override init(frame: CGRect) {
        super.init(frame: frame)
        setupAutoLayout()
    }

    required init?(coder aDecoder: NSCoder) {
        super.init(coder: aDecoder)
        setupAutoLayout()
    }

    func setupAutoLayout() {
        backgroundColor = .red
        addSubview(imageView)
        NSLayoutConstraint.activate([
            imageView.topAnchor.constraint(equalTo: self.topAnchor),
            imageView.leadingAnchor.constraint(equalTo: self.leadingAnchor),
            imageView.trailingAnchor.constraint(equalTo: self.trailingAnchor),
            imageView.bottomAnchor.constraint(equalTo: self.bottomAnchor)
            ])
    }
}
```

## @IBInspectable / @IBDesignable

Desafortunadamente los elementos generados programaticamente tienden a ser tediosos
ya que para visualizarlos es necesario compilar y accesar a la vista correspondiente en el simulador.
Para eviar ello podemos hacer uso de `@IBDesignable` quien nos permite visualizar en el Storyboard


```swift
@IBDesignable
class CatView: UIView {
  ...
}
```

Una vez declarado un objeto como `IBDesignable` se puede asignar a un view en el interface
builder, y al hacer esto automaticamente compila y renderiza el objeto .
Desafortunadamente esto requiere una compilacion en cada cambio sobre el archivo para ser
visualizado y esto puede hacer muy lenta la renderizacion.

De igual manera se pueden acceder a attributos de la clase en el interface builder por medio
de `@IBInspectable`

```swift
@IBDesignable
class CatView: UIView {
  @IBInspectable var name: String?
  ...
}
```
