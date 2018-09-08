---
title: Consumo de datos
category: ios
---

# Consumo de datos

## DataTask

#### Request Example

```swift
var components = URLComponents()
components.scheme = "https"
components.host = "example.com"
components.path = "/my_path"

var req = URLRequest(url: components.url!)
req.httpMethod = "GET"
// req.httpBody = try? JSONEncoder().encode(Encodable)
req.addValue("Bearer <User Token>", forHTTPHeaderField: "Authorization")

let session = URLSession.shared
let task = session.dataTask(with: req, completionHandler: completion)
task.resume()
```

#### [URLComponents](https://developer.apple.com/documentation/foundation/urlcomponents)
`port` the port subcomponent as a string
`query` the query subcomonent as a string
`queryItmes` the query represented as an array of URLQueryItem objects


#### [URLRequest](https://developer.apple.com/documentation/foundation/urlrequest)

`httpMethod` es una cadena variable de *URLRequest* que deve conformar cualquier metodo del protocolo de http:
- GET
- POST
- PUT
- PATCH
- DELETE
- HEADER
- OPTIONS

`httpBody` es una variable de tipo Data que contiene el cuerpo del request, este puede ser constuido con:
- Texto plano
- XML
- Encoded JSON
- Multipart data
