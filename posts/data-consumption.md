---
title: Consumo de datos
category: ios
---

# Consumo de datos

### Ejemplo completo

```swift
let baseURLComponents = URLComponents(string: "https://example.com")
func request(_ method: String, path: String, body: Data?, authToken: String?, successHandler: dataHandler?) {
  var requestURLComponents = baseURLComponents
  requestURLComponents.path = path
  var request = URLRequest(url: requestURLComponents.url!)
  request.httpMethod = method
  request.httpBody = body
  if let token = authToken {
    request.addValue("Bearer \(token)", forHTTPHeaderField: "Authorization")
  }
  let task = URLSession.shared.dataTask(with: request) { (data, response, error) in
    if error != nil { return }
    let httpResponse = response as! HTTPURLResponse
    if httpResponse.statusCode == 200, let handler = successHandler {
      handler(data)
    }
  }
  task.resume()
}
```

## URLSession

La clase **URLSession** y las clases relacionadas proporcionan una API para descargar contenido. Esta API proporciona un amplio conjunto de métodos delegados para admitir la autenticación y le da a su aplicación la capacidad de realizar descargas en segundo plano.

### Ejemplo

```swift
  let task = URLSession.shared.dataTask(with: request) { (data, response, error) in
    ...
  }
  task.resume()
```

## Tipos de URLSession

URLSession cuenta con una sesión *shared* singleton (que no tiene ningún objeto de configuración) para requests básicos.
No es tan configurable, pero sirve como punto de partida con requisitos muy limitados. Para otros tipos de sesiones, crea una instancia de URLSession con uno de tres tipos de configuraciones:
- **default** similar a *shared*, pero permite más configuración y le permite obtener datos de forma incremental con un delegado.
- **Ephemeral** similar a *shared*, pero sin cache, cookies o credenciales en el disco.
- **Background** permite realizar *downloads* y *uploads* de contenido en segundo plano mientras su aplicación no se está ejecutando.

## Tipos de URLSessionTask

Dentro de una sesión, usted crea tareas que opcionalmente cargan datos en un servidor y luego recuperan datos del servidor como un archivo en disco o como uno o más objetos NSData en la memoria. La API de URLSession proporciona tres tipos de tareas:

- **DataTask** envían y reciben datos utilizando objetos NSData. Las tareas de datos están destinadas a solicitudes cortas, a menudo interactivas, a un servidor.
- **UploadTask** son similares a las *DataTask*, pero también envían datos (a menudo en forma de un archivo) y admiten cargas de fondo mientras la aplicación no se está ejecutando.
- **DownloadTask** recuperan datos en forma de un archivo y admiten descargas y cargas de fondo mientras la aplicación no se está ejecutando.

## URLComponents

Es una estructura que parsea URLS y construlle URLs a partir de sus componentes.

#### [URLComponents](https://developer.apple.com/documentation/foundation/urlcomponents)
- `port` el puerto como String
- `query` el query como String
- `queryItmes` el query representado como un Array de URLQueryItem

### Ejemplo
```swift
var components = URLComponents()
components.scheme = "https"
components.host = "example.com"
components.path = "/api/path"
components.url
```

## URLRequest

Encapsula dos elementos basicos al cargar un request: la URL y la politica de cache a usar mientras consulta el contenido de la URL.

#### [URLRequest](https://developer.apple.com/documentation/foundation/urlrequest)

- `httpMethod` es un attributo String de *URLRequest* que debe conformar cualquier metodo del protocolo de http: *GET*, *POST*, *PUT*, *PATCH*, *DELETE*, *HEADER*, *OPTIONS*
- `httpBody` es un attributo Data que contiene el contenido del cuerpo

#### Ejemplo
```swift
var req = URLRequest(url: URL(string: "https://example.com"))
req.httpMethod = "GET"
req.httpBody = body
req.addValue("Bearer <User Token>", forHTTPHeaderField: "Authorization")

let session = URLSession.shared
let task = session.dataTask(with: req, completionHandler: completion)
task.resume()
```
