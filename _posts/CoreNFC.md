---
title: CoreNFC
category: development kit
layout: post
---

# Core NFC

La biblioteca core NFC (Near Field Communication) permite detectar etiquetas NFC, leer mensajes que contienen datos NDEF (Data Exchange Format) y guardar datos en etiquetas escribibles. Es posible leer etiquetas NFC de los tipos del 1 al 5 que contienen datos NDEF y también es posible escribir datos e interactuar con etiquetas bajo protocolos específicos como ISO 7816, ISO 15693, FeliCa™, y MIFARE®.

## Configurando la app para detectar etiquetas NFC

Para empezar es necesario activar Near Field Communication Tag Reading en la pestaña Capabilites para el target del proyecto, este paso añade:

* La funcionalidad de leer etiquetas NFC al App ID.
* El derecho de los formatos de sesión del lector de etiquetas NFC al archivo entitlements.

Después añadimos NFCReaderUsageDescription como un string item al archivo Info.plist.

## Inicializando una Reader Session

Creamos un objeto NFCNDEFReaderSession llamando al constructor init(delegate:queue:invalidateAfterFirstRead:) y pasando como parámetros:

* El objeto reader session delegate.
* La cola de despacho para usar cuando se llaman métodos en el delegado.
* El indicador invalidateAfterFirstRead para determinar si el reader session lee solo una etiqueta o varias etiquetas.

Después de crear el reader session, le damos instrucciones al usuario por medio de la propiedad alertMessage, algo del estilo "Mantén tu teléfono cerca del objeto para obtener más información", que será el mensaje mostrado al usuario cuando el teléfono está buscando etiquetas cerca.

Finalmente llamamos el método begin() para comenzar una reader session, lo que activa el sondeo por radiofrecuencia en el teléfono y comienza a buscar etiquetas.

A continuación se muestra el código de un botón que se encarga de activar el escaneo en un teléfono.

```

@IBAction func beginScanning(_ sender: Any) {
    guard NFCNDEFReaderSession.readingAvailable else {
        let alertController = UIAlertController(
            title: "Scanning Not Supported",
            message: "This device doesn't support tag scanning.",
            preferredStyle: .alert
        )
        alertController.addAction(UIAlertAction(title: "OK", style: .default, handler: nil))
        self.present(alertController, animated: true, completion: nil)
        return
    }

    session = NFCNDEFReaderSession(delegate: self, queue: nil, invalidateAfterFirstRead: false)
    session?.alertMessage = "Hold your iPhone near the item to learn more about it."
    session?.begin()
}

```

## Adoptando el protocolo Reader Session Delegate

El reader session necesita un delegado que implemente un el protocolo NFCNDEFReaderSessionDelegate, al adoptar este protocolo el delegado será capaz de recibir notificaciones del reader session cuando:

* Lee un mensaje NDEF
* Se vuelve inválido debido a que se terminó la sesión o se encontró un error

```
class MessagesTableViewController: UITableViewController, NFCNDEFReaderSessionDelegate {
```

## Leyendo un mensaje NDEF

Cada vez que el reader session encuentra un mensaje NDEF, esté envía el mensaje al delegado por medio del método readerSession(_:didDetectNDEFs:), que es cuando la aplicación debe decidir qué hacer con él. A continuación se muestra un código de ejemplo, en el que una aplicación decide almacenar el mensaje para mostrarle posteriormente al usuario.

```
func readerSession(_ session: NFCNDEFReaderSession, didDetectNDEFs messages: [NFCNDEFMessage]) {
    DispatchQueue.main.async {
        // Process detected NFCNDEFMessage objects.
        self.detectedMessages.append(contentsOf: messages)
        self.tableView.reloadData()
    }
}
```

## Manejando un reader session inválido

Cuando un reader session finaliza, llama al método readerSession(_:didInvalidateWithError:) y le pasa un objeto de error con la razón que finalizó la sesión, entre las posibles razones están:

* El teléfono exitosamente leyó una etiqueta NFC con un reader session configurado para invalidar la sesion despues de leer la primera etiqueta, y el código de error en ese caso sería NFCReaderError.Code.readerSessionInvalidationErrorFirstNDEFTagReado.
* El usuario canceló la sesión, o la aplicación llamo invalidate() al finalizar la sesión, en ese caso el código de error sería NFCReaderError.Code.readerSessionInvalidationErrorUserCanceled.
* Un error ocurrio durante la lectura, la lista de completa de errores se puede encontrar aqui: [NFCReaderError.Code](https://developer.apple.com/documentation/corenfc/nfcreadererror/code).

Es importante mencionar que una reader session invalidada no puede ser reutilizada.

A continuación se muestra un ejemplo en el que el delegado muestra una alerta cuando la reader session termina por cualquier razón que no sea leer la primera etiqueta durante una reader session de una sola etiqueta o que el usuario cancele la sesión el mismo.

```
func readerSession(_ session: NFCNDEFReaderSession, didInvalidateWithError error: Error) {
    // Check the invalidation reason from the returned error.
    if let readerError = error as? NFCReaderError {
        // Show an alert when the invalidation reason is not because of a
        // successful read during a single-tag read session, or because the
        // user canceled a multiple-tag read session from the UI or
        // programmatically using the invalidate method call.
        if (readerError.code != .readerSessionInvalidationErrorFirstNDEFTagRead)
            && (readerError.code != .readerSessionInvalidationErrorUserCanceled) {
            let alertController = UIAlertController(
                title: "Session Invalidated",
                message: error.localizedDescription,
                preferredStyle: .alert
            )
            alertController.addAction(UIAlertAction(title: "OK", style: .default, handler: nil))
            DispatchQueue.main.async {
                self.present(alertController, animated: true, completion: nil)
            }
        }
    }

    // To read new tags, a new session instance is required.
    self.session = nil
}
```

## Escribiendo un mensaje NDEF

Para escribir en una etiqueta, primero se inicializa una reader session, y esta debe permanecer activa para escribir un mensaje NDEF en la etiqueta, por lo que si se desea hacer esto, invalidateAfterFirstRead debe ser asignado como false.

```
@IBAction func beginWrite(_ sender: Any) {
    session = NFCNDEFReaderSession(delegate: self, queue: nil, invalidateAfterFirstRead: false)
    session?.alertMessage = "Hold your iPhone near an NDEF tag to write the message."
    session?.begin()
}
```

Cuando la reader session detecta una etiqueta, llama al metodo readerSession(_:didDetectNDEFs:) del delegado, sin embargo, como la sesión no se invalida despues de leer la primera etiqueta, es posible para la sesión detectar más de una etiqueta.

En el código de ejemplo solo se escribe en una etiqueta, así que revisa que la sesión detecte solo una etiqueta. Si la sesión detecta más de una, la aplicación le pide al usuario que remueva las etiquetas y reinicia el escaneo. Cuando la aplicación confirma que solo hay una etiqueta, se conecta a la etiqueta, verifica que sea escribible y escribe el mensaje NDEF.

```
func readerSession(_ session: NFCNDEFReaderSession, didDetect tags: [NFCNDEFTag]) {
    if tags.count > 1 {
        // Restart polling in 500 milliseconds.
        let retryInterval = DispatchTimeInterval.milliseconds(500)
        session.alertMessage = "More than 1 tag is detected. Please remove all tags and try again."
        DispatchQueue.global().asyncAfter(deadline: .now() + retryInterval, execute: {
            session.restartPolling()
        })
        return
    }

    // Connect to the found tag and write an NDEF message to it.
    let tag = tags.first!
    session.connect(to: tag, completionHandler: { (error: Error?) in
        if nil != error {
            session.alertMessage = "Unable to connect to tag."
            session.invalidate()
            return
        }

        tag.queryNDEFStatus(completionHandler: { (ndefStatus: NFCNDEFStatus, capacity: Int, error: Error?) in
            guard error == nil else {
                session.alertMessage = "Unable to query the NDEF status of tag."
                session.invalidate()
                return
            }

            switch ndefStatus {
            case .notSupported:
                session.alertMessage = "Tag is not NDEF compliant."
                session.invalidate()
            case .readOnly:
                session.alertMessage = "Tag is read only."
                session.invalidate()
            case .readWrite:
                tag.writeNDEF(self.message, completionHandler: { (error: Error?) in
                    if nil != error {
                        session.alertMessage = "Write NDEF message fail: \(error!)"
                    } else {
                        session.alertMessage = "Write NDEF message successful."
                    }
                    session.invalidate()
                })
            @unknown default:
                session.alertMessage = "Unknown NDEF tag status."
                session.invalidate()
            }
        })
    })
}
```

