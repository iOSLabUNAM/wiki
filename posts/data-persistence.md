---
title: Persistencia de datos
category: ios
---


## Persistencia de datos

- [UserDefaults](https://developer.apple.com/documentation/foundation/userdefaults)
- [FileManager](https://developer.apple.com/documentation/foundation/filemanager)
  - Documents
  - Cache
  - [Temporal](https://developer.apple.com/documentation/foundation/1409211-nstemporarydirectory)
- [NSCache](https://developer.apple.com/documentation/foundation/nscache)
- [Keychain](https://developer.apple.com/documentation/security/keychain_services)
- [CoreData](https://developer.apple.com/documentation/coredata)
  - [Guide](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/CoreData/index.html#//apple_ref/doc/uid/TP40001075-CH2-SW1)
  - [Persistent Store Features](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/CoreData/PersistentStoreFeatures.html)

## UserDefaults

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

## FileManager

Es un objeto que provee una interface de conveniencia a los contenidos del sistema de archivo.

### Cuando usar

- Persistencia de clases archivables que hereden de `NSCoder` interface o datos.
- Facilidad de uso y baja complejidad de datos.
- Cache de datos
- Persistencia de imagenes y datos binarios

### Como usar

### Uso de directorios [SearchPathDirectory](https://developer.apple.com/documentation/foundation/filemanager.searchpathdirectory)

- **.documentDirectory** User/Documents
- **.cachesDirectory** Lib/Cache

### Manejo de Directorios

```swift
var url = FileManager.default.urls(for: SearchPathDirectory, in: .userDomainMask).first!
let subfolder = "my-subfolder"
url.appendPathComponent(subfolder)
```

#### Crear Directorios

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

### NSKeyedArchiver / NSKeyedUnarchiver

#### Salvar archivo

```swift
NSKeyedArchiver.archiveRootObject(<NSCoder>, toFile: url.path)
```

#### Abrir archivo

```swift
NSKeyedUnarchiver.unarchiveObject(withFile: url.path)
```

### Codable

#### Salvar codable

```swift
let json = try JSONEncoder().encode(<Codable instance>)
try json.write(to: url)
```

#### Abrir codable

```swift
if let data = try? Data(contentsOf: url) {
    return try JSONDecoder().decode(<Codable>.self, from: data)
}
```

### NSCache

```swift
let cache = NSCache<NSString, UIImage>()
```

#### Set Object

```swift
cache.setObject(image, forKey: key as NSString)
```

#### Get Object
```swift
cache.object(forKey: key as NSString)
```
