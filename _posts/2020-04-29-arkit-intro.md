---
title: Introduccion a ARKit
category: development kit
author: Rodolfo Ortiz
layout: post
---

La realidad aumentada nos permite entremezclar el mundo real con el virtual de manera contextualizada. Para lograr esta ilusión se requiere procesar en tiempo real el movimiento del dispositivo que se está utilizando para poder modificar diferentes características del contenido virtual que se quiere mostrar, como lo son la posición, la escala o la rotación de los objetos.

Con las capacidades técnicas que se iban presentando en las útlimas generaciones de dispositivos Apple la realidad aumentada podía ser implementada. Sin embargo, el gran reto para el programador consistía en la complejidad de crear los algoritmos de detección de objetos en el mundo real para luego poder desplegar objetos virtuales. Es por esto que Apple creó **ARKit**, un framework para poder crear proyectos inmersivos de realidad aumentada de manera más sencilla.

Como ARKit requiere mucho poder de procesamiento, así como una cámara y una pantalla de alta resolución, sólo se pueden crear y correr apps con ARKit en dispositivos con iOS modernos, es decir, a partir del iPhone 6s/6s Plus o del iPad Pro. También es necesario el uso del compilador Xcode, así como el uso de alguno de los dos lenguajes de programación oficiales de Apple, es decir, Swift y Objective-C.

Arkit utiliza VIO (Visual Inertial Odometry) para seguir el movimiento del dispositivo y relacionarlo con el mundo exterior. Para esto fusiona la entrada de AVFoundation del sensor de la cámara y la información de movimiento obtenida por CoreMotion.

Algunas de las cosas que ARKit puede hacer son:

- Detecta y sigue el movimiento del dispositivo en tiempo real a través del espacio.
- Detecta imagenes en 2D y objetos en 3D para poder superponer objetos virtuales.
- Para lograr el seguimiento sin marcador, ARKit crea y maneja su propio mapa de las superficies detectadas.
- Puede ajustar de forma automática los niveles de brillo de tu contenido virtual para coincidir con el ambiente real.

Por otro lado, algunas de las limitaciones que se tienen son:

- La detección de superficies toma tiempo, por lo que es recomendado avisar al usuario y guiarlo durante el uso de la aplicación.
- Un excesivo movimiento del dispositivo altera el procesamiento de ARKit.
- Lugares con poca luz complican la detección de las escenas, así como superficies con texturas planas.

Al momento de crear un proyecto nuevo que requiera utilizar ARKit en Xcode es necesario, en primer lugar, modificar los requerimientos de hardware para el dispositivo iOS. Estas modificaciones se realizan en el *Info.plist*. Se debe de pedir permiso para el acceso a la cámara del dispostivo, por lo que se añade un requerimiento llamado *Privacy- Camera Usage Description*. Luego, para que el dispositivo tenga las capacidades requeridas para utilizar realidad aumentada, se debe de añadir un ítem a *Required device capabilities* dándole como valor *arkit*.

Habiendo hecho esos cambios en el *Info.plist* es momento de modificar el *Main.storyboard* para continuar con la configuración básica para un proyecto de ARKit. Buscando en la librería un objeto llamado *ARKit Scene View* lo agregamos para que cubra toda la vista del dispositivo. Haciendo control+click llevamos el *ARSCNView* al *ViewController.swift* y lo añadimos a nuestra clase de *Viewcontroller*, quedando el código de la siquiente manera:


```swift
import UIKit
import ARKit
import SceneKit

class ViewController: UIViewController {

    @IBOutlet var sceneView: ARSCNView!

}
```

Podemos notar que se importaron tanto la libreria de *ARKit* como la de *SceneKit*. Ahora es necesario agregar un protocolo a nuestra clase llamado *ARSCNViewDelegate* que contiene métodos que tú puedes implementar para sincronizar el contenido *SceneKit* con tu sesión de AR.

A continuación se prepara la aplicación para indicarle lo que hará una vez que sea ejecutada. Para esto se modifica nuevamente la clase de *ViewController*, quedando de la siguiente manera:

```swift
import UIKit
import ARKit
import SceneKit

class ViewController: UIViewController {

    @IBOutlet var sceneView: ARSCNView!

    override func viewDidLoad() {
        super.viewDidLoad()

        sceneView.delegate = self
        sceneView.showsStatistics = true
    }

    override func viewWillAppear(_ animated: Bool) {
        super.viewWillAppear(animated)

        let configuration = ARWorldTrackingConfiguration()
        sceneView.session.run(configuration)
    }

    override func viewWillDisappear(_ animated: Bool) {
        super.viewWillDisappear(animated)

        sceneView.session.pause()
    }
}
```

Para lograr la detección y seguimiento de la realidad aumentada se utiliza *ARWorldTrackingConfiguration( )*, el cual necesita la vista de *ARSCNView* para ser ejecutado. Dicha vista fue la que se colocó anteriormente en el *Main.storyboard*.

De esta forma tenemos una configuración básica para ejecutar una sesión con realida aumentada. El siguiente paso sería crear los objetos virtuales que queramos agregar a nuestro mundo. Esto se logra creando los modelos de los objetos y desplegándolos en una escena. Para poder ver un ejemplo de esto Xcode nos facilita un *template* de AR donde demuestra el uso de *Arkit*. Para esto solo debemos de ir a *Xcode> File> New Proyect> Augmented Reality App.* Ahí podemos apreciar una carpeta nueva llamada *art.scnassets* donde encontramos el modelo de un avión creado para ser utilizado con AR. Si observamos el código en la  función  de *viewWillAppear* se agrega una escena que ejecutará el objeto virtual creado.

Con esto terminamos la introducción a *ARKit* y se espera el lector siga indagando en más aspectos divertidos y curiosos que esta herramienta tan poderosa puede lograr.

### Bibliografía

- Bandekar, N., Bello, A., & Coron, T. (2018). *ARKit by Tutorials: Building Augmented Reality Apps in Swift 4.2*. Razeware LLC.
- Wang, W. (2018). *Beginning ARKit for IPhone and IPad: Augmented Reality App Development for IOS*. Apress.