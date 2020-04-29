---
title: CloudKit
category: ios
---

# **CloudKit**

CloudKit es la tecnología  de Apple en donde es posible tener disponibles tanto los datos de una aplicación como los datos de usuario en el momento que se requiera en múltiples dispositivos. Lo único que se requiere es conexión a internet y una cuenta de iCloud válida.

Los datos se guardan en entidades conocidas como *contenedores*, ningún otro desarrollador puede acceder al contenedor de la aplicación, a menos que se haya decidido compartirlo, incluso varias aplicaciones pueden compartir el mismo *contenedor*, y una aplicación puede usar múltiples *contenedores*. En cada *contenedor* existirán dos tipos de base de datos: pública y privada.

La base de datos pública es para guardar datos del usuario y de las aplicaciones que se comparten entre todas las instancias de la aplicación. De manera predeterminada todos los usuarios pueden leerla, pero si se requiere escribir en ella es necesario acceder con las credenciales de iCloud.

Existirá una base de datos privada por cada usuario de la aplicación, pero la aplicación sólo accederá a los datos del usuario en cuestión. Para leer y escribir en la base privada, el usuario tendrá que acceder con las credenciales de iCloud.

Existen un par de conceptos útiles para comprender el modo en el que los datos se manejan en este kit:

-   Schema: Representa los objetos de alto nivel de un *contenedor* y consiste en uno o más record types que tienen un nombre, campos y otros metadatos.

-   Record type: Es un conjunto de datos que define registros individuales. Representa datos estructurados en el *contenedor*, como una típica fila de una tabla que encapsula una serie de pares clave-valor.

-   Field Types: Son los tipos de datos permitidos dentro del framework. Existen tipos optimizados para ciertos datos como por ejemplo Location y Reference. El primero es usado para consultar eficientemente coordenadas geográficas, mientras que el segundo es usado para representar relaciones entre registros, uno a uno o bien, uno a muchos.

Para activar CloudKit en la app basta con realizar los siguientes pasos:

1.  En el target editor seleccionar la app, luego la pestaña **Sign & Capabilities**
2.  Dar click en **+Capability**
3.  En la ventana que aparece buscar **iCloud.** Es importante contar con ID de Apple asociado a la cuenta de desarrollador logueado.
4.  Seleccionar un Team

![Figura 1](https://github.com/JulesLeGrand/wiki/blob/master/cloudkit_capabilities.png)

![Figura 2](https://github.com/JulesLeGrand/wiki/blob/master/cloudkit_cloud.png)

El siguiente paso es habilitar el checkbox de CloudKit.

![Figura 3](https://github.com/JulesLeGrand/wiki/blob/master/cloudkit_checkboxes.png)

Finalmente hay dos opciones: Se puede elegir algún *contenedor* existente **(5)**, o dar click en **+**, donde aparecerá una ventana, en la que se recomienda rellenar con el *bundleId*:

![Figura 4](https://github.com/JulesLeGrand/wiki/blob/master/cloudkit_newcontainer.png)

Para acceder al Dashboard de CloudKit sólo es necesario dar click en el botón de hasta abajo con la leyenda "CloudKit Dashboard".


Para usar CloudKit es necesario agregar el import a la clase.

```swift
Import CloudKit
```

Para trabajar con el contenedor lo mejor sería usar una constante como propiedad de la clase.
```swift
let container = CKContainer.defaultContainer()
```

Para seleccionar la base pública basta agregar la propiedad `publicCloudDatabase` al *contenedor*.

  
```swift
let database = container.publicCloudDatabase
```

Para recuperar datos de la base es necesario usar un `CKQuery`, que describe cómo encontrar todos los registros de un determinado tipo que coincidan con ciertos criterios. Los criterios pueden ser algo así como *“todos los registros con el campo Apellido que comienzan ‘H’”*. Por lo que es necesario usar un `NSPredicate` para manejar este tipo de criterios.

```swift
let predicate = NSPredicate(value: true)
```
  
Por último, se emplea un objeto de tipo `CKQuery`, el cual recuperará los datos del record Type.

```swift
let query = CKQuery(recordType: “Lista”, predicate: predicate)
```

Y llamando a la instancia de la base de datos ejecutamos el query de forma asíncrona.

```swift
database.performQuery(query, inZoneWithID: nil) { results, error in
	
	if error != nil {
		print(“Algo falló con la base de datos“)
	} else {
	
		guard let resultado = results else {
			return
		}
	
		for resultado in resultado {
			let nombre = resultado objectForKey("Nombre") as! String

			let apellidos = resultado.objectForKey("Apellidos") as! String

			let telefono = resultado.objectForKey("Telefono") as! Int

			print(nombre, apellidos, telefono)

		}

	}

}
```
  

Si se requiere ordenar los resultados de la consulta, se debe crear antes del `NSPredicate` un objeto `NSSortDescriptor`.

```swift
let sort = NSSortDescriptor(key: “Apellidos”, ascending: true)
```

Antes del `performQuery` se pasa como parámetro el objeto a la propiedad `sortDescriptors`.

```swift
query.sortDescriptors = [sort]
```



Para más información, consultar:  [Cloudkit Quick Start](https://developer.apple.com/library/archive/documentation/DataManagement/Conceptual/CloudKitQuickStart/Introduction/Introduction.html#//apple_ref/doc/uid/TP40014987-CH1-SW1),  [Apple developer](https://developer.apple.com/documentation/cloudkit)
