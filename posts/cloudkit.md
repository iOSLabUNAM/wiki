---
title: CloudKit
category: ios
---

#**CloudKit**

CloudKit es la tecnología  de Apple en donde es posible tener disponibles tanto los datos de una aplicación como los datos de usuario en el momento que se requiera en múltiples dispositivos. Lo único que se requiere es conexión a internet y una cuenta de iCloud válida.

Los datos se guardan en entidades conocidas como contenedores. Ningún otro desarrollador puede acceder al contenedor de la aplicación, a menos que se haya decidido compartirlo, incluso varias aplicaciones pueden compartir el mismo contenedor, y una aplicación puede usar múltiples contenedores. En cada contenedor existirán dos tipos de base de datos: Pública y privada.

La base de datos pública es para guardar datos del usuario y de las aplicaciones que se comparten entre todas las instancias de la aplicación. De manera predeterminada todos los usuarios pueden leerla, pero si se requiere escribir en ella es necesario acceder con las credenciales de iCloud.

Existirá una base de datos privada por cada usuario de la aplicación, pero la aplicación sólo accederá a los datos del usuario en cuestión. Para leer y escribir en la base privada, el usuario tendrá que acceder con las credenciales de iCloud.

Existen un par de conceptos útiles para comprender el modo en el que los datos se manejan en este kit:

-   Schema: Representa los objetos de alto nivel de un contenedor y consiste en uno o más record types que tienen un nombre, campos y otros metadatos.

-   Record type: Es un conjunto de datos que define registros individuales. Representa datos estructurados en el contenedor, como una típica fila de una tabla que encapsula una serie de pares clave-valor.

-   Field Types: Son los tipos de datos permitidos dentro del framework. Existen tipos optimizados para ciertos datos como por ejemplo Location y Reference. El primero es usado para consultar eficientemente coordenadas geográficas, mientras que el segundo es usado para representar relaciones entre registros, uno a uno o bien, uno a muchos.

Para activar CloudKit en la app basta con realizar los siguientes pasos:

1.  En el target editor seleccionar la app, luego la pestaña **Sign & Capabilities**
2.  Dar click en **+Capability**
3.  En la ventana que aparece buscar **iCloud.** Es importante contar con ID de Apple asociado a la cuenta de desarrollador logueado.
4.  Seleccionar un Team

![Figura 1](https://raw.githubusercontent.com/JulesLeGrand/wiki/blob/master/assets/img/cloudkit_capabilities.png)