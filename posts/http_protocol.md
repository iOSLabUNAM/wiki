# Protocolo HTTP 

## *Definición*

<div style="text-align: justify">
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

## *Mensajes HTTP*

### Peticiones



#### Métodos

#### Path

#### Versión del protocolo

#### Headers

#### 

