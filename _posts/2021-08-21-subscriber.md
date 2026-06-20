---
title: Subscriber
category: Combine
layout: post
---
# Subscriber

`Subscriber` es un protocolo que define los requerimientos para que un tipo pueda recibir entradas de un `Publisher`, junto a los eventos del ciclo de vida. Los tipos de `Input` y `Failure` de de un `Subscriber` deben coincidir con los tipos `Output` y `Failure` del `Publisher` asociado.

Para realizar la conexión de un `Subscriber` con un `Publisher` es necesario llamar al método `subscribe(_:)` del `Publisher`, justo después de realizar esta llamada el `Publisher` invoca el método `receive(subscription:)` del `Subscriber`. 

En este punto se entrega una instancia de tipo `Subscription` al `Subscriber`, el cual será usado para solicitar valores del `Publisher` o en su defecto cancelar la subscripción.

Una parte del protocolo `Subscriber` se muestra a continuación.


```swift
        public protocol Subscriber: CustomCombineIdentifierConvertible {
        // 1
        associatedtype Input

        // 2
        associatedtype Failure: Error

        // 3
        func receive(subscription: Subscription)

        // 4
        func receive(_ input: Self.Input) -> Subscribers.Demand

        // 5
        func receive(completion: Subscribers.Completion<Self.Failure>)

        }

```

1. El tipo de valores que el `Subscriber` puede recibir.
2. El tipo de error que el `Subscriber` puede recibir o `Never` si no se recibe ningún tipo de error. 
3. El método `receive(subscription:)` es llamado por el `Publisher` para entregar la suscripción al `Subscriber`
4. El método `recieve(_:)` es llamado por el `Publisher` para enviar valores al `Subscriber`.
5. El método `recieve(completion:)` es llamado por el `Publisher` para notificar al `Subscriber` que ha terminado de producir valores de manera exitosa o debido a un error.

## Subscription

`Subscription` es un protocolo que representa la conexión entre un `Subscriber` y un `Publisher`. Cuando el `Subscriber` ha terminado o ya no necesita recibir los valores emitidos por un `Publiser` es momento de cancelar la suscripción para liberar recursos y detener todas las actividades relacionadas a dicha suscripción.

Las suscripciones regresan una instancia del tipo `AnyCancellable` como un token de cancelación, esto permite cancelar dicha suscripción en cualquier momento que se desee. `AnyCancellable` cumple con el protocolo `Cancellable` el cual requiere el método `cancel()` para ser cancelado.

Si el método `cancel` no es llamado de forma explícita en una suscripción, continuará hasta que el publisher termine su ciclo de vida, o hasta que  la administración de memoria cause que las subscripción sea destruída. Si se destruye la subscripción se cancela automáticamente.

Una consideración importante es que si el valor de la subscripción no es almacenado en alguna variable esta será cancelada de manera automática cuando el programa salga del contexto donde ésta fue creada.

![Figura 1](https://i.ibb.co/DDDpHjj/Sketch1629659392394.png)


Una parte del protocolo `Subscription` se muestra a continuación:

```swift
    public protocol Subscription: Cancellable,CustomCombineIdentifierConvertible {
        func request(_ demand: Subscribers.Demand)
    }
```

El `Subscriber` llama el método `request(_:)` para indicar que desea recibir más valores, hasta un máximo de números o ilimitado.


## Ejemplo de Subscriber personalizado


Definimos la clase que será `Publisher`:

```swift
    // 1
 final class IntSubscriber: Subscriber {
    // 2
    typealias Input = Int
    typealias Failure = Never

    // 3
    func receive(subscription: Subscription) {
        subscription.request(.max(3))
    }
    // 4
    func receive(_ input: Int) -> Subscribers.Demand {
      print("Valor recibido", input)
      return .none
    }
    
    // 5
    func receive(completion: Subscribers.Completion<Never>) {
      print("Notificación de término", completion)
    }
  }
```
1. Definición de la clase IntSubscriber.
2. Implementación de los `typealias` para especificar que un `Subscriber` puede recibir `Int` como entradas y no recibirá errores.
3. Implementación de los métodos requeridos. iniciando con el método `receive(subscription:)` el cual es llamado por el `Publisher`. Dentro de este se llama el método `request(_:)` de la suscripción, en este caso se indica que recibirá hasta tres valores.
4.  Se imprime cada unos de los valores recibidos y se regresa `.none` lo que indica que el `Subscriber` no incrementa su demanda más allá de la demanda inicial.
5.  Se imprime al recibir un evento de término.


Una vez que hemos definido nuestro `Subscriber` es posible utilizarlo de la siguiente manera.


```swift
    let publisher = (1...6).publisher
    let subscriber = IntSubscriber()

    publisher.subcribe(subscriber)
```

La salida del código anterior será la siguiente:

```console
    Valor recibido 1
    Valor recibido 2
    Valor recibido 3
```

En este caso no se recibió la notificación del evento de término debido a que se especificó al `Publisher` que solo se requerían 3 valores.
Si modificamos el método `recieve(_:)` del `Subscriber` de la siguiente manera podemos obtener más valores.

```swift
    func receive(_ input: Int) -> Subscribers.Demand {
      print("Valor recibido", input)
      return .unlimited
    }
```

Para este caso la ejecución producirīa la siguiente salida:

```console
    Valor recibido 1
    Valor recibido 2
    Valor recibido 3    
    Valor recibido 4
    Valor recibido 5
    Valor recibido 6
    Notificación de termino finished
```


# Referencias 

https://developer.apple.com/documentation/combine/subscription
Combine: Asynchronous Programming with Swift,Florent Pillet, Shai Mishali, Scott Gardner and Marin Todorov 