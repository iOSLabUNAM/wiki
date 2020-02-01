# Servicios Restful

## *¿Qué es un servicio Restful?*

REST cambió por completo la ingeniería de software a partir del 2000. Este nuevo enfoque de desarrollo de proyectos y servicios web fue definido por Roy Fielding, el padre de la especificación HTTP y uno los referentes internacionales en todo lo relacionado con la Arquitectura de Redes, en su disertación ‘Architectural Styles and the Design of Network-based Software Architectures’. En el campo de las APIs, REST (Representational State Transfer- Transferencia de Estado Representacional) es, a día de hoy, el alfa y omega del desarrollo de servicios de aplicaciones.

En la actualidad no existe proyecto o aplicación que no disponga de una API REST para la creación de servicios profesionales a partir de ese software. Twitter, YouTube, los sistemas de identificación con Facebook… hay cientos de empresas que generan negocio gracias a REST y las APIs REST. Sin ellas, todo el crecimiento en horizontal sería prácticamente imposible. Esto es así porque REST es el estándar más lógico, eficiente y habitual en la creación de APIs para servicios de Internet.

Buscando una definición sencilla, REST es cualquier interfaz entre sistemas que use HTTP para obtener datos o generar operaciones sobre esos datos en todos los formatos posibles, como XML y JSON. Es una alternativa en auge a otros protocolos estándar de intercambio de datos como SOAP (Simple Object Access Protocol), que disponen de una gran capacidad pero también mucha complejidad. A veces es preferible una solución más sencilla de manipulación de datos como REST.


## *Características de REST*
- Protocolo cliente/servidor sin estado: cada petición HTTP contiene toda la información necesaria para ejecutarla, lo que permite que ni cliente ni servidor necesiten recordar ningún estado previo para satisfacerla. Aunque esto es así, algunas aplicaciones HTTP incorporan memoria caché. Se configura lo que se conoce como protocolo cliente-caché-servidor sin estado: existe la posibilidad de definir algunas respuestas a peticiones HTTP concretas como cacheables, con el objetivo de que el cliente pueda ejecutar en un futuro la misma respuesta para peticiones idénticas. De todas formas, que exista la posibilidad no significa que sea lo más recomendable.

- Las operaciones más importantes relacionadas con los datos en cualquier sistema REST y la especificación HTTP son cuatro: POST (crear), GET (leer y consultar), PUT (editar) y DELETE (eliminar).

- **Los objetos en REST siempre se manipulan a partir de la URI.** Es la URI y ningún otro elemento el identificador único de cada recurso de ese sistema REST. La URI nos facilita acceder a la información para su modificación o borrado, o, por ejemplo, para compartir su ubicación exacta con terceros.

- **Interfaz uniforme:** para la transferencia de datos en un sistema REST, este aplica acciones concretas (POST, GET, PUT y DELETE) sobre los recursos, siempre y cuando estén identificados con una URI. Esto facilita la existencia de una interfaz uniforme que sistematiza el proceso con la información.

- **Sistema de capas:** arquitectura jerárquica entre los componentes. Cada una de estas capas lleva a cabo una funcionalidad dentro del sistema REST.

- **Uso de hipermedios:** hipermedia es un término acuñado por Ted Nelson en 1965 y que es una extensión del concepto de hipertexto. Ese concepto llevado al desarrollo de páginas web es lo que permite que el usuario puede navegar por el conjunto de objetos a través de enlaces HTML. En el caso de una API REST, el concepto de hipermedia explica la capacidad de una interfaz de desarrollo de aplicaciones de proporcionar al cliente y al usuario los enlaces adecuados para ejecutar acciones concretas sobre los datos.

Para cualquier API REST es obligatorio disponer del principio HATEOAS (Hypermedia As The Engine Of Application State - Hipermedia Como Motor del Estado de la Aplicación) para ser una verdadera API REST. Este principio es el que define que cada vez que se hace una petición al servidor y éste devuelve una respuesta, parte de la información que contendrá serán los hipervínculos de navegación asociada a otros recursos del cliente.


## *Métodos HTTP (REST)*

Entender los métodos HTTP es fundamental para comprender la forma en que funciona la arquitectura REST, pues mediante los métodos le indicamos al servidor la forma en que debe de tratar una determinada petición, dicho esto, una misma URL puede ser tratada de forma diferente por el servidor.


- **GET:** Es utilizado únicamente para consultar información al servidor, muy parecidos a realizar un SELECT a la base de datos. No soporta el envío del payload
GET: Obtener datos. Ej: GET /v1/empleados/1234

- **POST:** Es utilizado para solicitar la creación de un nuevo registro, es decir, algo que no existía previamente, es decir, es equivalente a realizar un INSERT en la base de datos. Soporta el envío del payload.
POST: Crear un nuevo recurso. Ej: POST /v1/empleados

- **PUT:** Se utiliza para actualizar por completo un registro existente, es decir, es parecido a realizar un UPDATE a la base de datos. Soporta el envío del payload.
PUT: Actualizar datos. Ej: PUT /v1/empleados/1234

- **PATCH:** Este método es similar al método PUT, pues permite actualizar un registro existente, sin embargo, este se utiliza cuando actualizar solo un fragmento del registro y no en su totalidad, es equivalente a realizar un UPDATE a la base de datos. Soporta el envío del payload
¿PATCH?: Para actualizar ciertos datos

- **DELETE:** Este método se utiliza para eliminar un registro existente, es similar a DELETE a la base de datos. No soporta el envío del payload.
DELETE: Borrar el recurso. Ej: DELETE /v1/empleados/1234

- **HEAD:** Este método se utilizar para obtener información sobre un determinado recurso sin retornar el registro. Este método se utiliza a menudo para probar la validez de los enlaces de hipertexto, la accesibilidad y las modificaciones recientes.

## *Filtrado y paginación de los datos*
Exponer una colección de recursos con un único URI puede dar lugar a que las aplicaciones capturen grandes cantidades de datos cuando solo se requiere un subconjunto de la información. Por ejemplo, suponga que una aplicación cliente necesita encontrar todos los pedidos con un costo cercano a un valor específico. Se podrían recuperar todos los pedidos del URI /orders y, a continuación, filtrar estos pedidos en el lado cliente. Es obvio que este proceso es muy ineficaz. Se malgasta ancho de banda de red y potencia de procesamiento en el servidor que hospeda la API web.
En su lugar, la API puede permitir que pase un filtro en la cadena de consulta del URI, como /orders?minCost=n. La API web es responsable entonces de analizar y administrar el parámetro minCost en la cadena de consulta y de devolver los resultados filtrados en el lado servidor.
Las solicitudes GET sobre recursos de la colección pueden devolver posiblemente un gran número de elementos. Debe diseñar una API que limite la cantidad de datos devueltos en una única solicitud. Considere la posibilidad de admitir cadenas de consulta que especifiquen el número máximo de elementos que se van a recuperar y un desplazamiento inicial en la colección. Por ejemplo:
HTTP
```
/orders?limit=25&offset=50
```

## *Autenticación y validación en API REST*

### Métodos de autenticación

Básicamente tenemos dos formas de implementar la autenticación en servidor:
Basada en cookies, la más utilizada:
El servidor guarda la cookie para autenticar al usuario en cada request.
Habrá que tener un almacen de sesiones: en bbdd, Redis...
- **Basada en tokens**, se confía en un token firmado que se envía al servidor en cada petición

### ¿Qué es un token?

Un token es un valor que nos autentica en el servidor

Normalmente se consigue después de hacer login mediante usuario/contraseña
¿Cómo se genera el token?

Normalmente un hash calculado con algún dato (p.ej. login del usuario + clave secreta)
Además el token puede llevar datos adicionales como el login
¿Cómo comprueba el servidor que es válido?
Generando de nuevo el Hash y comprobando si es igual que el que envía el usuario (100% stateless)
O bien habiendo almacenado el Hash en una B.D. asociado al usuario y simplemente comprobando que coincide
Beneficios de usar tokens

### OAuth

Para que una app pueda acceder a servicios de terceros sin que el usuario tenga que darle a la app sus credenciales del servicio
Ejemplo: una app que permite publicar en tu muro de FB, pero en la que no confías lo suficiente como para meter tu login y password de FB
Es el estándar en APIs REST abiertos a terceros
Se basa en el uso de un token de sesión


## *Control de versiones de una API web RESTful*
Es muy poco probable que una API web permanezca estática. Conforme los requisitos empresariales cambian, se pueden agregar nuevas colecciones de recursos, las relaciones entre los recursos pueden cambiar y la estructura de los datos de los recursos puede rectificarse. El control de versiones permite que una API web indique las características y recursos que expone y que una aplicación cliente pueda enviar solicitudes que se dirijan a una versión específica de una característica o un recurso. En las secciones siguientes se describen varios enfoques diferentes, cada uno de los cuales tiene sus propias ventajas y desventajas.

### **Sin control de versiones**

Este es el enfoque más sencillo y puede ser aceptable para algunas API internas. Los cambios significativos se pueden representar como nuevos recursos o nuevos vínculos. Agregar contenido a los recursos existentes podría no presentar un cambio importante, ya que las aplicaciones cliente que no esperan ver este contenido lo omitirán.
Por ejemplo, una solicitud al URI https://adventure-works.com/customers/3 debe devolver los detalles de un solo cliente que contiene los campos id, name y address esperados por la aplicación cliente:
```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8

{"id":3,"name":"Contoso LLC","address":"1 Microsoft Way Redmond WA 98053"}
```

### **Control de versiones de URI**

Cada vez que modifica la API web o cambia el esquema de recursos, agrega un número de versión al URI para cada recurso. Los URI ya existentes deben seguir funcionando como antes y devolver los recursos conforme a su esquema original.
Extendiendo el ejemplo anterior, si el campo de address se reestructura en subcampos que contienen cada una de las partes constituyentes de la dirección (por ejemplo, streetAddress, city, statey zipCode), esta versión del recurso podría exponerse a través de un URI que contenga un número de versión, como:
```
https://adventure-works.com/v2/customers/3:
```


### **Control de versiones de cadena de consulta**

En lugar de proporcionar varios URI, puede especificar la versión del recurso mediante un parámetro dentro de la cadena de consulta anexada a la solicitud HTTP, como:
```
https://adventure-works.com/customers/3?version=2
```
El parámetro de versión debe adoptar de forma predeterminada un valor significativo como 1 si se omite en las aplicaciones cliente más antiguas.



### **Control de versiones de encabezado**

En lugar de anexar el número de versión como un parámetro de cadena de consulta, podría implementar un encabezado personalizado que indica la versión del recurso. Este enfoque requiere que la aplicación cliente agregue el encabezado adecuado a las solicitudes, aunque el código que controla la solicitud de cliente puede usar un valor predeterminado (versión 1) si se omite el encabezado de versión. En los ejemplos siguientes se usa un encabezado personalizado denominado Custom-Header. El valor de este encabezado indica la versión de la API web.


**Version 1**
```
GET https://adventure-works.com/customers/3 HTTP/1.1
Custom-Header: api-version=1
```
**Version 2**
```
GET https://adventure-works.com/customers/3 HTTP/1.1
Custom-Header: api-version=2
```

### Referencias:

* [¿Que es un API REST?](https://bbvaopen4u.com/es/actualidad/api-rest-que-es-y-cuales-son-sus-ventajas-en-el-desarrollo-de-proyectos)

* [Metodos HTTP REST](https://www.oscarblancarteblog.com/2018/12/03/metodos-http-rest/)

* [Autenticación y validación en API REST](https://juanda.gitbooks.io/webapps/content/api/arquitectura-api-rest.html)

* [API Design](https://docs.microsoft.com/es-es/azure/architecture/best-practices/api-design)
