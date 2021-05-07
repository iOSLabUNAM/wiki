---
title: Persistencia de datos
category: ios
layout: post
---

## UserDefaults
- [UserDefaults](https://developer.apple.com/documentation/foundation/userdefaults)

Es la interface para configuracion default de ususario, donde se almacenan parejas de `key-value` persistentes a traves de la aplicacion.

### Cuando usar

- Cuando son configuraciones basicas del usuario
- Cuando no importa que los datos esten expuestos
- Cuando usamos primitivas de objective-c NSData, NSString, NSNumber, NSDate, NSArray, or NSDictionary
- Cuando queremos guardar configuraciones de ambiente
- Cuando queremos un acceso facil en toda la aplicacion

### Como usar

```swift
UserDefaults.standard.set(true, forKey: "myKey")
UserDefaults.standard.<dataType>(forKey: "myKey")
```


### Nota
Para situaciones donde se requiere almacenar datos de manera segura se recomienda utilizar [Keychain](https://developer.apple.com/documentation/security/keychain_services) ya que al contrario de UserDefaults donde se tiene en un archivo de texto plano, keychain encripta la informacion.


## FileManager(Archivos en Disco)
- [FileManager](https://developer.apple.com/documentation/foundation/filemanager)

Es un objeto que provee una interface de conveniencia a los contenidos del sistema de archivo.

### Cuando usar

- Persistencia de clases archivables que hereden de `NSCoder` interface o datos.
- Facilidad de uso y baja complejidad de datos.
- Cache de datos
- Persistencia de imagenes y datos binarios

### Como usar

#### Uso de directorios [SearchPathDirectory](https://developer.apple.com/documentation/foundation/filemanager.searchpathdirectory)

- **.documentDirectory** User/Documents
- **.cachesDirectory** Lib/Cache

#### Manejo de Directorios

```swift
var url = FileManager.default.urls(for: SearchPathDirectory, in: .userDomainMask).first!
let subfolder = "my-subfolder"
url.appendPathComponent(subfolder)
```

##### Crear Directorios

```swift
try fileManager.createDirectory(at: url, withIntermediateDirectories: false, attributes: nil)
```

#### ¿Existe el archivo? ¿Es directorio?

```swift
var isDir: ObjCBool = false
let fileExits = FileManager.default.fileExists(atPath: folder.path, isDirectory: &isDir)
```

#### Eliminar el archivo

```swift
try fileManager.removeItem(at: url)
```

#### NSKeyedArchiver / NSKeyedUnarchiver

##### Salvar archivo *(Deprecated)*

```swift
NSKeyedArchiver.archiveRootObject(<NSCoder>, toFile: url.path)
```

##### Abrir archivo *(Deprecated)*

```swift
NSKeyedUnarchiver.unarchiveObject(withFile: url.path)
```

#### Codable

##### Salvar codable

```swift
let json = try JSONEncoder().encode(<Codable instance>)
try json.write(to: url)
```

##### Abrir codable

```swift
if let data = try? Data(contentsOf: url) {
    return try JSONDecoder().decode(<Codable>.self, from: data)
}
```

## NSCache
- [NSCache](https://developer.apple.com/documentation/foundation/nscache)

Una colección mutable que se utiliza para almacenar temporalmente en memoria datos transitorios. Se maneja de manera similar a un diccionario o lo que se conoce en NoSQL key-value store. Los datos que están sujetos a liberacion arbitraria por parte del sistema operativo cuando los recursos son bajos.

### Cuando usar
Normalmente, NSCache se utiliza para almacenar temporalmente objetos con datos transitorios que son costosos de crear. La reutilización de estos objetos puede proporcionar beneficios de rendimiento, ya que sus valores no tienen que volver a calcularse. Sin embargo, los objetos deven de no ser críticos para la aplicación ya se pueden descartar por el sistema operativo cuando requiera mayor uso de memoria y esta sea limitada.

### Como usar

```swift
let cache = NSCache<NSString, Any>()
```

#### Set Object

```swift
cache.setObject(image, forKey: key as NSString)
```

#### Get Object
```swift
cache.object(forKey: key as NSString)
```

## CoreData
- [CoreData](https://developer.apple.com/documentation/coredata)
  - [Guide](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/CoreData/index.html#//apple_ref/doc/uid/TP40001075-CH2-SW1)
  - [Persistent Store Features](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/CoreData/PersistentStoreFeatures.html)

Contrario a la creencian **CoreData NO es un ORM**, ya que se cuenta con features mas extensos que permiten el manejo de datos a manera de control de versiones, por lo que muy pocos escenarios lo requieren, ademas que la implementacion y el mantenimiento es complejo.
