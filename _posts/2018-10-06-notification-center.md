---
title: Notification Center
category: ios
layout: post
---

Es el mecanismo de envío de notificaciones que permite la transmisión de información a los observadores registrados. Este mecanismo permite transmitir datos de una parte de su aplicación a otra. Utilizando el patrón de *Observer* para informar a los observadores registrados cuando llega una notificación, utilizando el *Grand Central Dispatch* para el llamado de de notificaciones. Consta de 3 elementos:
 - Un "listener" que escucha las notificaciones, llamado observador
 - Un "sender" que envía notificaciones cuando algo sucede.
 - El propio Notification Center, que realiza un seguimiento de los observadores y notificaciones.


## Observer

```swift
  NotificationCenter.default.addObserver(self, selector: #selector(triggeredNotice(_:)), name: NSNotification.Name("Notificacion"), object: nil)
```

Consta de 4 parametros:

 - **observer** Objeto de se registra como observador.
 - **selector** Especifica el mensaje que el receptor envía al observador para notificarle la publicación de la notificación. El método especificado por el selector debe tener un argumento (una instancia de NSNotification).
 - **name** El nombre de la notificación para la cual se registra al observador; es decir, solo las notificaciones con este nombre se envían al observador.
 - **object** El objeto cuyas notificaciones el observador quiere recibir; es decir, solo las notificaciones enviadas por este remitente se envían al observador. Si es nulo, el centro de notificaciones no utiliza el remitente de una notificación para decidir si se lo entrega al observador.

Es recomendable tener los nombres de todas las notificaciones como parte de una extension, de esta manera el codigo es menos suceptible a errores de typo.

```swift
extension Notification.Name {
    static let didReceiveData = Notification.Name("didReceiveData")
}
```

## Sender

```swift
  NotificationCenter.default.post(name: NSNotification.Name("Notificacion"), object: nil)
```
Para enviar una notificacion se constan de 3 parameters:

 - **name** El nombre de las notificacion de tipo `Notification.Name`
 - **object** El objeto que se envia en la notificacion, puede ser nulo o cualquier objeto. Su proposito es filtrar la notificacion del emisor
 - **userInfo** Funciona para enviar datos adicionales a la notificacion

