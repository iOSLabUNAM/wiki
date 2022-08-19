---
title: Evolucion de URLSession
category: ios
layout: post
---

### Implementacion con closures

Utilizando `dataTask` dentro de URLSession, podemos crear una tarea que reciba una función de callback para ser llamada cuando la tarea termine.
Esta implementacion es heredada de Objective-C, y utiliza closures para pasar la información de la tarea, en casos exitosos y de error.


```swift
func request(request: URLRequest, success: @escaping (Data?)->Void)?, fail: ((Error)-> Void)?) {
  let task = URLSession.shared.dataTask(with: request) { (data, response, error) in
    guard let error = error {
      fail?(error)
      return
    }
                                                        
    let httpResponse = response as! HTTPURLResponse
                                                        
    if httpResponse.statusCode == 200 {
      success?(data)
    }
  }
  task.resume()
}
```

El principal problema es que tenemos que manejar closures para el flujo de datos y el error, en las implementaciones de este metodo. Resultando en una implementacion mas compleja.

## Implementacion con Result Type

Por ello con el surgimeiento de ResultType en Swift 5, solo creamos un closure para completar cuando la tarea termine. Y al turilizarlo podemos capturar el resultado utlizando los mecanismos de ResultType.


```swift
func request(request: URLRequest, complete: @escaping (Result<Data?, Error>)->Void)) {
  let task = URLSession.shared.dataTask(with: request) { (data, response, error) in
    guard let error = error {
      complete(.failure(error))
      return
    }
                                                        
    let httpResponse = response as! HTTPURLResponse
                                                        
    if httpResponse.statusCode == 200 {
      complete(.success(data))
    }
  }
  task.resume()
}
```

Sin embargo, con esta implementacion al concatenar objetos subsecuentes de ResultType resulta complicado de manejar por lo que se recurren a metodos como flatMap y map para manejar los resultados.

## Implementacion con Async/Await

Todas las implementaciones anteriores require una tarea que se ejecute en el background, y una tarea que se ejecute en el main thread. Lo cual en SwiftUI no es posible por lo que se requirere de una implementacion mas compleja utilizando Combine.

Con el surgimeiento de Async/Await en Swift 5.5 y el patron de actores, podemos crear implementaciones mas simples y leegibles.

```swift
enum NetworkError: Error {
  case invalidResponse(String)
}

func request(request: URLRequest) async throws -> Data? {
  let (data, response) = try await session.data(for: req)

  guard let httpResponse = response as? HTTPURLResponse else {
    throw NetworkError.invalidResponse("Invalid http url response")
  }

  if httpResponse.statusCode == 200 {
    return data
  } else {
    throw NetworkError.invalidResponse("Unsuccessful response :\(httpResponse.statusCode) [status code]")
  }
}
```

Gracias a este patron, podemos manejar el resultado de la tarea de forma mas sencilla y compatibles con SwiftUI.