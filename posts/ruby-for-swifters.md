---
title: Ruby para Swifteros
category: backend
---

# Ruby para Swifteros

Al igual que swift ruby es un lenguaje orientado objetos robusto y con un amplio ecosistema en el desarrollo web.
En esta guia encontraras los paradigmas y diferencias entre swift y ruby.

## Principales Diferencias

- **Paradigma**: Ruby es un lenguaje totalmente orientado a objetos, al contrario de swift
donde tenemos structuras y enums que no son objetos. En ruby TODO es un objeto
- **Tipado**: A diferencia de swift donde el tipado es estatico, en ruby el tipado es dinamico, lo cual quiere
decir que nunca tendremos que definir un tipo de dato en una variable.
- **Interpretado**: Al contrario de swift y objective-c donde se compila a un binario, ruby es un lenguaje interpretado,
lo cual quiere decir que ruby interpreta linea por linea y ejecuta al vuelo. Por lo tanto si tenemos un error de en nuestro codigo no va haber un compilador que nos diga cual fue nuestro error. Los errores en ruby suceden en el momento de la ejecucion.

## Variables

**Swift**
```swift
  let inmutableVariable: String = "Hello World!"
  var mutableVariable = "Hello"
  mutableVariable += " World!"
```

**Ruby**
```ruby
  variable = "Hello"
  variable += " World!"
```

A diferencia de swift en ruby no hay "constantes", todo puede cambiar.

## Estructuras de Control

### If

**Swift**
```swift
  if value {
    print("SI")
  } else {
    print("NO")
  }
```

**Ruby**
```ruby
  if value
    puts("SI")
  else
    puts("NO")
  end
```

Como notaras la sintaxis del if es similar sin embargo en ruby se utilizan bloques de codigo con `begin`, `do`, `end` en ves de utilizar `{}`

### Guard

**Swift**
```swift
  func foo(input: String?) -> String {
    guard let str = input else { return "NO" }
    return str
  }
```

**Ruby**
```ruby
  def foo(input:)
    return "NO" unless input
    input
  end
```

Ruby de manera explicita no cuenta con un `guard` sin embargo el patron se puede implementar con `unless` que es un `if !value`

### Switch

**Swift**
```swift
  switch value {
  case 1:
      print("one")
  case 2:
      print("two")
  default:
      print("other")
  }
```

**Ruby**
```ruby
  case value
  when 1
    puts("one")
  when 2
    puts("two")
  else
    puts("other")
  end
```

En terminos de sintaxis es muy similar sin embargo las palabras reservadas cambian, en ruby usamos `case` en vez de `switch` y en vez de case usamos `when` esto porque ruby es un lenguaje que busca ser similar a una sintaxis en ingles.

## Ciclos

**Swift**
```swift
  let items: [Int] = [1,2,3,4,5,6]
  for item in items {
    print(item)
  }
```

**Ruby**
```ruby
  items = [1,2,3,4,5,6]
  items.each do |item|
    puts(item)
  end
```

Para iterar objetos, en ruby dado que todo es un objeto, los objeto enumerables cuentan con un metodo
each para iterar sobre cada elemento.

## Estructuras de Datos

### Arrays

**Swift**
```swift
  let items: [String] = ["a", "b", "c", "d"]
  let items: [Any] = ["a", 1, 1.0, MyClass()]
```

**Ruby**
```ruby
  items = ["a", "b", "c", "d"]
  values = [:a, 1, 1.0, MyClass.new(x)]
```

Dado que en ruby es de tipado dinamico, y todo es un objeto no es necesario definir un tipo de dato para
los elementos de un Arrays

### Dicionarios

**Swift**
```swift
  var items: [String:String] = ["a": "A", "b": "B"]
  items["c"] = "C"
  print(items["a"])
```

**Ruby**
```ruby
  items = { "a" => "A", "b" => "B" }
  items["c"] = "C"
  puts(items["a"])

  items = { a: "A", b: "B" }
  items[:c] = "C"
  puts(items[:a])
```

En ruby los dicionarios son conocidos como `hashmaps` y se definen utilizando `{}` y mientras que en Swift
las llaves las definimos con `:` en ruby usamos hash rocket `=>`, aunque generalmente en los hashmaps
se definen con symbolos como llaves, por lo tanto la sintaxis queda mas reducida.

## Clojures / Bloques

**Swift**
```swift
   func foo(bar: (Bool) -> Void) {
     bar(true)
   }

   foo() { value in
     print(value)
   }
```

**Ruby**
```ruby
  def foo(block)
    block.call(true)
  end

  foo { |value| puts(value) }
  foo do |value|
    puts value
  end
```

Gran parte de elementos en ruby usan bloques que pueden ser procs o lambdas que si bien son muy similares
tienen una similtud con los clojures de swift. La ventaja es que en ruby no se tiene que definir el tipo de dato.

## Opcionales

**Swift**
```swift
  var value: String?
```

**Ruby**
```ruby
  value = nil
```

Tanto en Objective-C como en swift todas las variables so No Opcionales, para permitir que un valor sea nulo
Swift implemento opcionales, sin embargo el resto de lenguajes de programacion todas las varialbes pueden
tener un puntero nulo.

## Clases

**Swift**
```swift
  class MyClass: ParentClass {
    init(){

    }
  }
```

**Ruby**
```ruby
  class MyClass < ParentClass
    def initialize
    end
  end
```
