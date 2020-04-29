---
title: Protocolo HTTP
category: foundations
---

# Protocolo HTTP

## *Definición*

HTTP, de sus siglas en inglés: "Hypertext Transfer Protocol", es el protocolo en el que se basa la Web. Fue inventado por Tim Berners-Lee entre los años 1989-1991. HTTP ha visto muchos cambios, manteniendo la mayor parte de su simplicidad y desarrollando su flexibilidad. Es la base de cualquier intercambio de datos en la Web, y un protocolo de estructura cliente-servidor, esto quiere decir que una petición de datos es iniciada por el elemento que recibirá los datos (el cliente), normalmente un navegador Web.

- - -

## *Versiones*

* #### HTTP/1.0

    * Se agrega la versión del protocolo cuando se envía una petición, por ejemplo: HTTP/1.0.
    * Se envía un código de estado al comienzo de la respuesta, permitiendo así que el navegador pueda responder al éxito o fracaso de la petición realizada.
    * El concepto de cabeceras de HTTP, se presentó tanto para las peticiones como para las respuestas, permitiendo la trasmisión de meta-data.
    * Con el uso de las cabeceras de HTTP, se pudieron transmitir otros documentos además de HTML, mediante la cabecera _Content-Type_.
    * Hay una conexión TCP por cada petición/respuesta intercambiada, presentando estos dos grandes inconvenientes: abrir y crear una conexión requiere varias rondas de mensajes, por lo tanto resultaba lento.

* #### HTTP/1.1

    * Una conexión podía ser reutilizada, ahorrando así el tiempo de re-abrirla repetidas veces para mostrar los recursos empotrados dentro del documento original pedido.
    * Enrutamiento ('Pipelining') se añadió a la especificación, permitiendo realizar una segunda petición de datos, antes de que fuera respondida la primera, disminuyendo de este modo la latencia de la comunicación: cabecera _Connection_ con el valor _keep-alive_.
    * Se permitió que las respuestas a peticiones, podían ser divididas en sub-partes.
    * Se añadieron controles adicionales a los mecanismos de gestión de la cache.
    * La negociación de contenido, incluyendo el lenguaje, el tipo de codificación o tipos, se añadieron a la especificación, permitiendo que servidor y cliente, acordaran el contenido más adecuado a intercambiarse.
    * Gracias a la cabecera _Host_, pudo ser posible alojar varios dominios en la misma dirección IP.


* #### HTTP/2.0

    * Es un protocolo binario, en contraposición a estar formado por cadenas de texto, tal y como estaban basados las versiones anteriores. Así no se puede leer directamente, ni crear manualmente.  
    * Es un protocolo multiplexado. Peticiones paralelas pueden hacerse sobre la misma connexión, no está sujeto pues a mantener el orden de los mensajes, ni otras restricciones que tenían los protocolos anteriores HTTP/1.x
    * Comprime las cabeceras, ya que estas, normalmente son similares en un grupo de peticiones. Esto elimina la duplicación y retardo en los datos a transmitir.
    * Esto permite al servidor almacenar datos en la caché del cliente, previamente a que estos sean pedidos, mediante un mecanismo denominado 'server push'.

- - -

## *Componentes de una URL*

Una URL para HTTP  normalmente consta de tres o cuatro componentes:

### Scheme

El esquema identifica el protocolo que se utilizará para acceder al recurso en Internet. Puede ser HTTP (sin SSL) o HTTPS (con SSL).

### Host

Identifica el host que contiene el recurso. Por ejemplo:www.ejemplo.com. Un servidor proporciona servicios en nombre del host, pero los hosts y servidores no tienen una asignación uno a uno. Los nombres de host también pueden ir seguidos de un número de puerto. Los números de puerto conocidos para un servicio normalmente se omiten de la URL. La mayoría de los servidores utilizan los números de puerto conocidos para HTTP y HTTPS, por lo que la mayoría de las URL de HTTP omiten el número de puerto.

### Path

La ruta identifica el recurso específico en el host al que el cliente web quiere acceder. Por ejemplo: /software/htp/cics/index.html.

### Query String

Si se usa una cadena de consulta, sigue el componente de ruta y proporciona una cadena de información que el recurso puede usar para algún propósito (por ejemplo, como parámetros para una búsqueda o como datos para procesar). La cadena de consulta suele ser una cadena de pares de nombre y valor; por ejemplo: term=bluebird. Los pares de nombre y valor están separados entre sí por un ampersand (&); por ejemplo: term=bluebird&source=browser-search.

El esquema y los componentes de host de una URL no se definen como mayúsculas y minúsculas, pero la ruta y la cadena de consulta son sensibles a mayúsculas y minúsculas. Por lo general, la URL completa se especifica en minúsculas.

Los componentes de la URL se combinan y delimitan de la siguiente manera:

`scheme://host:port/path?query`

- El esquema es seguido por dos puntos y dos barras diagonales.
- Si se especifica un número de puerto, ese número sigue al nombre del host, separado por dos puntos.
- El nombre de la ruta comienza con una sola barra diagonal.
- Si se especifica una cadena de consulta, está precedida por un signo de interrogación.`

- - -

## *Componentes de HTTP*

* #### Métodos

HTTP define 8 métodos (algunas veces referido como "verbos") que indica la acción que desea que se efectúe sobre el recurso identificado. Lo que este recurso representa, si los datos pre-existentes o datos que se generan de forma dinámica, depende de la aplicación del servidor. A menudo, el recurso corresponde a un archivo o la salida de un ejecutable que se encuentra en el servidor.


#### GET

Pide una representación del recurso especificado. Por seguridad no debería ser usado por aplicaciones que causen efectos ya que transmite información a través de la URI agregando parámetros a la URL.

_Ejemplo:_

    GET /images/logo.png HTTP/1.1

Explicación: obtiene un recurso llamado logo.png

_Ejemplo con parámetros:_

    GET /index.php?page=main&lang=es

#### POST

Aunque se puedan enviar datos a través del método GET, en muchos casos se utiliza POST por las limitaciones de GET. El contenido va en el body del request, no aparece nada en la URL, aunque se envía en el mismo formato que con el método GET. Si se quiere enviar texto largo o cualquier tipo de archivo este es el método apropiado.

#### HEAD

Pide una respuesta idéntica a la que correspondería a una petición GET, pero sin el cuerpo de la respuesta. Esto es útil para la recuperación de meta-información escrita en los encabezados de respuesta, sin tener que transportar todo el contenido.

#### PUT

Sube, carga o realiza un upload de un recurso especificado (archivo), es el camino más eficiente para subir archivos a un servidor, esto es porque en POST utiliza un mensaje multipart y el mensaje es decodificado por el servidor. En contraste, el método PUT te permite escribir un archivo en una conexión socket establecida con el servidor.
La desventaja del método PUT es que los servidores de hosting compartido no lo tienen habilitado.

_Ejemplo:

    PUT /path/filename.html HTTP/1.1

#### DELETE

Este método le solicita al servidor web que se borre un recurso en específico.

#### TRACE

Este método Permite monitorear los mensajes que hay entre el cliente y el servidor web. Principalmente se usa con propósitos de diagnósticos de fallas o para revisar si existen servidores intermediarios en la conexión.

#### OPTIONS

Devuelve los métodos HTTP que el servidor soporta para un URL específico.Esto puede ser utilizado para comprobar la funcionalidad de un servidor web mediante petición en lugar de un recurso específico.

#### CONNECT

Este método se utiliza para solicitar una conexión de tipo túnel TCP/IP. Principalmente se utiliza cuando se necesita utilizar un proxy para una conexión segura cifrada HTTPS o para comunicaciones vía SSL.

* #### Headers

Las cabeceras (headers) HTTP permiten al cliente y al servidor enviar información adicional junto a una petición o respuesta. Una cabecera de petición esta compuesta por su nombre (no sensible a las mayúsculas) seguido de dos puntos ':', y a continuación su valor (sin saltos de línea). Los espacios en blanco a la izquierda del valor son ignorados
Se pueden agregar cabeceras propias personalizadas usando el prefijo 'X-', pero esta convención se encuentra desfasada desde Julio de 2012, debido a los inconvenientes causados cuando se estandarizaron campos no estándar en el RFC 6648; otras están listadas en un registro IANA, cuyo contenido original fue definido en el RFC 4229, IANA tambien mantiene un registro de propuestas para nuevas cabeceras HTTP.

Las Cabeceras pueden ser agrupadas de acuerdo a sus contextos:

___Cabecera general:___ Cabeceras que se aplican tanto a las peticiones como a las respuestas, pero sin relación con los datos que finalmente se transmiten en el cuerpo.
___Cabecera de consulta:___ Cabeceras que contienen más información sobre el contenido que va a obtenerse o sobre el cliente.
___Cabecera de respuesta:___ Cabeceras que contienen más información sobre el contenido, como su origen o el servidor (nombre, versión, etc.).
___Cabecera de entidad:___ Cabeceras que contienen más información sobre el cuerpo de la entidad, como el tamaño del contenido o su tipo MIME (son una serie de convenciones o especificaciones dirigidas al intercambio a través de Internet de todo tipo de archivos de forma transparente para el usuario).

##### Cabeceras comunes para peticiones y respuestas:

* ___Content-Type:___ descripción MIME de la información contenida en este mensaje. Es la referencia que utilizan las aplicaciones Web para dar el correcto tratamiento a los datos que reciben.
* ___Content-Length:___ longitud en bytes de los datos enviados, expresado en base decimal.
* ___Content-Encoding:___ formato de codificación de los datos enviados en este mensaje. Sirve, por ejemplo, para enviar datos comprimidos (x-gzip o x-compress) o encriptados.
* ___Date:___ fecha local de la operación. Las fechas deben incluir la zona horaria en que reside el sistema que genera la operación. Por ejemplo: Sunday, 12-Dec-96 12:21:22 GMT+01. No existe un formato único en las fechas; incluso es posible encontrar casos en los que no se dispone de la zona horaria correspondiente, con los problemas de sincronización que esto produce. Los formatos de fecha a emplear están recogidos en los RFC 1036 y 1123.
* ___Pragma:___ permite incluir información variada relacionada con el protocolo HTTP en el requerimiento o respuesta que se está realizando. Por ejemplo, un cliente envía un Pragma: no-cache para informar de que desea una copia nueva del recurso especificado.

##### Cabeceras sólo para peticiones del cliente

* ___Accept:___ campo opcional que contiene una lista de tipos MIME aceptados por el cliente. Se pueden utilizar * para indicar rangos de tipos de datos; tipo/* indica todos los subtipos de un determinado medio, mientras que */* representa a cualquier tipo de dato disponible.
* ___Authorization:___ clave de acceso que envía un cliente para acceder a un recurso de uso protegido o limitado. La información incluye el formato de autorización empleado, seguido de la clave de acceso propiamente dicha. La explicación se incluye más adelante.
* ___From:___ campo opcional que contiene la dirección de correo electrónico del usuario del cliente Web que realiza el acceso.
* ___If-Modified-Since:___ permite realizar operaciones GET condicionales, en función de si la fecha de modificación del objeto requerido es anterior o posterior a la fecha proporcionada. Puede ser utilizada por los sistemas de almacenamiento temporal de páginas. Es equivalente a realizar un HEAD seguido de un GET normal.
* ___Referer:___ contiene la URL del documento desde donde se ha activado este enlace. De esta forma, un servidor puede informar al creador de ese documento de cambios o actualizaciones en los enlaces que contiene. No todos los clientes lo envían.
* ___User-agent:___ cadena que identifica el tipo y versión del cliente que realiza la petición. Por ejemplo, los browsers de Netscape envían cadenas del tipo User-Agent: Mozilla/3.0 (WinNT; I)

##### Cabeceras sólo para respuestas del servidor HTTP

* ___Allow:___ informa de los comandos HTTP opcionales que se pueden aplicar sobre el objeto al que se refiere esta respuesta. Por ejemplo, Allow: GET, POST.
* ___Expires:___ fecha de expiración del objeto enviado. Los sistemas de cache deben descartar las posibles copias del objeto pasada esta fecha. Por ejemplo, Expires: Thu, 12 Jan 97 00:00:00 GMT+1. No todos los sistemas lo envían. Puede cambiarse utilizando un \<META EXPIRES\> en el encabezado de cada documento.
* ___Last-modified:___ fecha local de modificación del objeto devuelto. Se puede corresponder con la fecha de modificación de un fichero en disco, o, para información generada dinámicamente desde una base de datos, con la fecha de modificación del registro de datos correspondiente.
* ___Location:___ informa sobre la dirección exacta del recurso al que se ha accedido. Cuando el servidor proporciona un código de respuesta de la serie 3xx, este parámetro contiene la URL necesaria para accesos posteriores a este recurso.
* ___Server:___ cadena que identifica el tipo y versión del servidor HTTP. Por ejemplo, Server: NCSA 1.4.
* ___WWW-Autenticate:___ cuando se accede a un recurso protegido o de acceso restringido, el servidor devuelve un código de estado 401, y utiliza este campo para informar de los modelos de autentificación válidos para acceder a este recurso.

* #### Códigos y mensajes de respuesta

La lista de los códigos de estado de HTTP se divide en 5 categorías:

___100’s:___ Códigos informativos indicando que la solicitud iniciada por el navegador es constante.

___200’s:___ Códigos exitosos devueltos cuando la petición del explorador se ha recibido correctamente, entendido, y procesado por el servidor.

___300’s:___ Los códigos de redirección se devuelven cuando un nuevo recurso ha sido sustituido por el recurso solicitado.

___400’s:___ Códigos de error del cliente indicando que existe un problema con la solicitud.

___500’s:___ Códigos de error del servidor indicando que la petición fue aceptada, pero que un error en el servidor impidió el cumplimiento de la solicitud.

* ##### 100's - Respuestas informativas

*100 Continue*

Esta respuesta provisional indica que todo hasta ahora está bien y que el cliente debe continuar con la solicitud o ignorarla si ya está terminada.

*101 Switching Protocol*

Este código se envía en respuesta a un encabezado de solicitud Upgrade por el cliente e indica que el servidor acepta el cambio de protocolo propuesto por el agente de usuario.

*102 Processing (WebDAV)*

Este código indica que el servidor ha recibido la solicitud y aún se encuentra procesandola, por lo que no hay respuesta disponible.

* ##### 200's - Respuestas satisfactorias

*200 OK*

La solicitud ha tenido éxito. El significado de un éxito varía dependiendo del método HTTP:
GET: El recurso se ha obtenido y se transmite en el cuerpo del mensaje.
HEAD: Los encabezados de entidad están en el cuerpo del mensaje.
PUT o POST: El recurso que describe el resultado de la acción se transmite en el cuerpo del mensaje.
TRACE: El cuerpo del mensaje contiene el mensaje de solicitud recibido por el servidor.

*201 Created*

La solicitud ha tenido éxito y se ha creado un nuevo recurso como resultado de ello. Ésta es típicamente la respuesta enviada después de una petición PUT.

*202 Accepted*

La solicitud se ha recibido, pero aún no se ha actuado. Es una petición "Sin compromiso", lo que significa que no hay manera en HTTP que permita enviar una respuesta asíncrona que indique el resultado del procesamiento de la solicitud. Está pensado para los casos en que otro proceso o servidor maneja la solicitud, o para el procesamiento por lotes.

*203 Non-Authoritative Information*

La petición se ha completado con éxito, pero su contenido no se ha obtenido de la fuente originalmente solicitada, sino que se recoge de una copia local o de un tercero. Excepto esta condición, se debe preferir una respuesta de 200 OK en lugar de esta respuesta.

*204 No Content*

La petición se ha completado con éxito pero su respuesta no tiene ningún contenido, aunque los encabezados pueden ser útiles. El agente de usuario puede actualizar sus encabezados en caché para este recurso con los nuevos valores.

*205 Reset Content*

La petición se ha completado con éxito, pero su respuesta no tiene contenidos y además, el agente de usuario tiene que inicializar la página desde la que se realizó la petición, este código es útil por ejemplo para páginas con formularios cuyo contenido debe borrarse después de que el usuario lo envíe.

*206 Partial Content*

La petición servirá parcialmente el contenido solicitado. Esta característica es utilizada por herramientas de descarga como wget para continuar la transferencia de descargas anteriormente interrumpidas, o para dividir una descarga y procesar las partes simultáneamente.

*207 Multi-Status (WebDAV)*

Una respuesta Multi-Estado transmite información sobre varios recursos en situaciones en las que varios códigos de estado podrían ser apropiados. El cuerpo de la petición es un mensaje XML.

*208 Multi-Status (WebDAV)*

El listado de elementos DAV ya se notificó previamente, por lo que no se van a volver a listar.

*226 IM Used (HTTP Delta encoding)*

El servidor ha cumplido una petición GET para el recurso y la respuesta es una representación del resultado de una o más manipulaciones de instancia aplicadas a la instancia actual.

* ##### 300's - Redirecciones

*300 Multiple Choice*

Esta solicitud tiene más de una posible respuesta. User-Agent o el usuario debe escoger uno de ellos. No hay forma estandarizado de seleccionar una de las respuestas.

*301 Moved Permanently*

Este código de respuesta significa que la URI  del recurso solicitado ha sido cambiado. Probablemente una nueva URI sea devuelta en la respuesta.

*302 Found*

Este código de respuesta significa que el recurso de la URI solicitada ha sido cambiado temporalmente. Nuevos cambios en la URI serán agregados en el futuro. Por lo tanto, la misma URI debe ser usada por el cliente en futuras solicitudes.

*303 See Other*

El servidor envia esta respuesta para dirigir al cliente a un nuevo recurso solcitado a otra dirección usando una petición GET.

*304 Not Modified*

Esta es usada para propositos de "caché". Le indica al cliente que la respuesta no ha sido modificada. Entonces, el cliente puede continuar usando la misma versión almacenada en su caché.

*305 Use Proxy*

Fue definida en una versión previa de la especificación del protocolo HTTP para indicar que una respuesta solicitada debe ser accedida desde un proxy. Ha quedado obsoleta debido a preocupaciones de seguridad correspondientes a la configuración de un proxy.

*306 unused*

Este código de respuesta ya no es usado más. Actualmente se encuentra reservado. Fue usado en previas versiones de la especificación HTTP1.1.

*307 Temporary Redirect*

El servidor envía esta respuesta para dirigir al cliente a obtener el recurso solicitado a otra URI con el mismo metodo que se uso la petición anterior. Tiene la misma semántica que el código de respuesta HTTP 302 Found, con la excepción de que el agente usuario no debe cambiar el método HTTP usado: si un POST fue usado en la primera petición, otro POST debe ser usado en la segunda petición.

*308 Permanent Redirect*

Significa que el recurso ahora se encuentra permanentemente en otra URI, especificada por la respuesta de encabezado HTTP Location:. Tiene la misma semántica que el código de respuesta HTTP 301 Moved Permanently, con la excepción de que el agente usuario no debe cambiar el método HTTP usado: si un POST fue usado en la primera petición, otro POST debe ser usado en la segunda petición.

* ##### 400's - Errores de cliente

*400 Bad Request*

Esta respuesta significa que el servidor no pudo interpretar la solicitud dada una sintaxis inválida.

*401 Unauthorized*

Es necesario autenticar para obtener la respuesta solicitada. Esta es similar a 403, pero en este caso, autenticación es posible.

*402 Payment Required*

Este código de respuesta está reservado para futuros usos. El objetivo inicial de crear este código fue para ser utilizado en sistemas digitales de pagos. Sin embargo, no está siendo usado actualmente.

*403 Forbidden*

El cliente no posee los permisos necesarios para cierto contenido, por lo que el servidor está rechazando otorgar una respuesta apropiada.

*404 Not Found*

El servidor no pudo encontrar el contenido solicitado. Este código de respuesta es uno de los más famosos dada su alta ocurrencia en la web.

*405 Method Not Allowed*

El método solicitado es conocido por el servidor pero ha sido deshabilitado y no puede ser utilizado. Los dos métodos obligatorios, GET y HEAD, nunca deben ser deshabilitados y no debiesen retornar este código de error.

*406 Not Acceptable*

Esta respuesta es enviada cuando el servidor, despues de aplicar una negociación de contenido servidor-impulsado, no encuentra ningún contenido seguido por la criteria dada por el usuario.

*407 Proxy Authentication Required*

Esto es similar al código 401, pero la autenticación debe estar hecha a partir de un proxy.

*408 Request Timeout*

Esta respuesta es enviada en una conexión inactiva en algunos servidores, incluso sin alguna petición previa por el cliente. Significa que el servidor quiere desconectar esta conexión sin usar. Esta respuesta es muy usada desde algunos navegadores, como Chrome, Firefox 27+, o IE9, usa mecanismos de pre-conexión HTTP para acelerar la navegación. También hay que tener cuenta que algunos servidores simplemente desconectan la conexión sin enviar este mensaje.

*409 Conflict*

Esta respuesta puede ser enviada cuando una petición tiene conflicto con el estado actual del servidor.

*410 Gone*

Esta respuesta puede ser enviada cuando el contenido solicitado ha sido borrado del servidor.

*411 Length Required*

El servidor rechaza la petición porque el campo de encabezado Content-Length no esta definido y el servidor lo requiere.

*412 Precondition Failed*

El cliente ha indicado pre-condiciones en sus encabezados la cual el servidor no cumple.

*413 Payload Too Large*

La entidad de petición es más larga que los limites definidos por el servidor; el servidor puede cerrar la conexión o retornar un campo de encabezado Retry-After.

*414 URI Too Long*

La URI solicitada por el cliente es más larga que el servidor está dispuesto a interpretar.

*415 Unsupported Media Type*

El formato multimedia de los datos solicitados no está soportada por el servidor, por lo cual el servidor rechaza la solicitud.

*416 Requested Range Not Satisfiable*

El rango especificado por el campo de encabezado Range en la solicitud no cumple; es posible que el rango está fuera del tamaño de los datos objetivo del URI.

*417 Expectation Failed*

Significa que la expectativa indicada por el campo de encabezado Expect solicitada no puede ser cumplida por el servidor.

*418 I'm a teapot*

El servidor se reúsa a intentar hacer café con una tetera.

*421 Misdirected Request*

La petición fue dirigida a un servidor que no es capaz de producir una respuesta. Esto puede ser enviado por un servidor que no esta configurado para producir respuestas por la combinación del esquema y la autoridad que estan incluidos en la URI solicitada

*422 Unprocessable Entity (WebDAV)*

La petición estaba bien formada pero no se pudo seguir debido a errores de semántica.

*423 Locked (WebDAV)*

El recurso que está siendo accedido está bloqueado.

*424 Failed Dependency (WebDAV)*

La petición falló debido a una falla de una petición previa.

*426 Upgrade Required*

El servidor se reúsa a aplicar la solicitud usando el protocolo actual pero puede estar dispuesto a hacerlo después que el cliente se actualize a un protocolo diferente. El servidor envía un encabezado Upgrade en una respuesta para indicar los protocolos requeridos.

*428 Precondition Required*

El servidor origen requiere que la solicitud sea condicional. Tiene la intención de prevenir problemas de 'actualización perdida', donde un cliente OBTIENE un estado del recurso, lo modifica, y lo PONE devuelta al servidor, cuando mientras un tercero ha modificado el estado del servidor, llevando a un conflicto.

*429 Too Many Requests*

El usuario ha enviado demasiadas solicitudes en un periodo de tiempo dado.

*431 Request Header Fields Too Large*

El servidor no está dispuesto a procesar la solicitud porque los campos de encabezado son demasiado largos. La solicitud PUEDE volver a subirse después de reducir el tamaño de los campos de encabezado solicitados.

*451 Unavailable For Legal Reasons*

El usuario solicita un recurso ilegal, como alguna página web censurada por algún gobierno.

* ##### 500's - Errores de servidor

*500 Internal Server Error*

El servidor ha encontrado una situación que no sabe como manejarla.

*501 Not Implemented*

El método solicitado no esta soportado por el servidor y no puede ser manejada. Los unicos métodos que los servidores requieren soporte (y por lo tanto no deben retornar este código) son GET y HEAD.

*502 Bad Gateway*

Esta respuesta de error significa que el servidor, mientras trabaja como una puerta de enlace para obtener una respuesta necesaria para manejar la petición, obtuvo una respuesta inválida.

*503 Service Unavailable*

El servidor no esta listo para manejar la petición. Causas comunes puede ser que el servidor está caido por mantenimiento o está sobrecargado. Hay que tomar en cuenta que junto con esta respuesta, una página usuario-amigable explicando el problema debe ser enviada. Estas respuestas deben ser usadas para condiciones temporales y el encabezado HTTP Retry-After: debería, si es posible, contener el tiempo estimado antes de la recuperación del servicio. El webmaster debe también cuidar los encabezados relacionados al caché que son enviados junto a esta respuesta, ya que estas respuestas de condicion temporal deben usualmente no estar en el caché.

*504 Gateway Timeout*

Esta respuesta de error es dada cuando el servidor está actuando como una puerta de enlace y no puede obtener una respuesta a tiempo.

*505 HTTP Version Not Supported*

La versión de HTTP usada en la petición no está soportada por el servidor.

*506 Variant Also Negotiates*

El servidor tiene un error de configuración interna: negociación de contenido transparente para la petición resulta en una referencia circular.

*507 Insufficient Storage*

El servidor tiene un error de configuración interna: la variable de recurso escogida esta configurada para acoplar la negociación de contenido transparente misma, y no es por lo tanto un punto final adecuado para el proceso de negociación.

*508 Loop Detected (WebDAV)*

El servidor detectó un ciclo infinito mientras procesaba la solicitud.

*510 Not Extended*

Extensiones adicionales para la solicitud son requeridas para que el servidor las cumpla.

*511 Network Authentication Required*

El código de estado 511 indica que el cliente necesita auntenticar para ganar acceso a la red.

- - -

## *Mensajes HTTP*

#### Peticiones

![HTTP_REQUEST](https://media.prod.mdn.mozit.cloud/attachments/2016/08/09/13687/5d4c4719f4099d5342a5093bdf4a8843/HTTP_Request.png)

La primera línea es la request line y el resto son cabeceras HTTP.
Una petición de HTTP, está formado  por los siguientes campos:

* Un método HTTP. El objetivo de un cliente, suele ser una petición de recursos, usando GET, o presentar un valor de un formulario HTML, usando POST, aunque en otras ocasiones puede hacer otros tipos de peticiones.
* La dirección del recurso pedido (Path).
* Cabeceras HTTP opcionales, que pueden aportar información adicional a los servidores.
* Opcional, un cuerpo de mensaje en algún método, como puede ser POST, en el cual envía la información para el servidor.

#### Respuestas

![HTTP_RESPONSE](https://media.prod.mdn.mozit.cloud/attachments/2016/08/09/13691/58390536967466a1a59ba98d06f43433/HTTP_Response.png)

La primera línea es la status line o línea de estado, seguida de las cabeceras HTTP y finalmente el contenido servido.
Las respuestas están formadas por los siguentes campos:

* La versión del protocolo HTTP que están usando.
* Un código de estado, indicando si la petición ha sido exitosa, o no, y debido a que.
* Un mensaje de estado, una breve descripción del código de estado.
* Cabeceras HTTP, como las de las peticiones.
* Opcionalmente, el recurso que se ha pedido.


## Fuentes

* [Componentes de URL](https://www.ibm.com/support/knowledgecenter/SSGMCP_5.1.0/com.ibm.cics.ts.internet.doc/topics/dfhtl_uricomp.html)
* [Versiones de HTTP](https://somostechies.com/que-es-http2/)
* [Versiones de HTTP (2)](https://developer.mozilla.org/es/docs/Web/HTTP/Basics_of_HTTP/Evolution_of_HTTP)
* [Métodos de HTTP](https://sites.google.com/site/httpsprotocolo/versiones-de-http)
* [Métodos de HTTP (2)](https://es.wikibooks.org/wiki/M%C3%A9todos_HTTP)
* [Mensajes HTTP](https://developer.mozilla.org/es/docs/Web/HTTP/Overview)
* [Códigos de respuesta](https://developer.mozilla.org/es/docs/Web/HTTP/Status)
* [Códigos de respuesta (2)](https://kinsta.com/es/blog/codigos-de-estado-de-http/)
* [Headers](https://developer.mozilla.org/es/docs/Web/HTTP/Headers)
* [Headers (2)](http://redesdecomputadores.umh.es/aplicacion/HTTP.htm)
