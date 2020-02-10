
---
title: Vision
category: annex
---

# ¿Qué es Vision?

Vision, aparte de ser uno de los Vengadores,  es uno de los frameworks desarrollados por Apple para aplicar Machine Learning a nuestras apps.

Aplica algoritmos de visión por computadora para realizar una variedad de tareas en imágenes de entrada y video.

Esta construido sobre CoreML y Core Image, Vision nos da las herramientas necesarias para trabajar con imágenes, además de:

* Detección de rostro y cuerpo.
* Encontrar caras y sus características.
* Rectángulos,como tarjetas y letreros en imágenes .
* Seguimiento de objetos (tracking).
* Detección de códigos de barras (en diferentes formatos).
* Situar la línea del horizonte.
* Alineación de imágenes.
* Análisis de imágenes con Machine Learning.
* Encontrar texto en imágenes.
* Reconocimiento de texto.
* Análisis de imagen fija.
* Detección de de codigo de Barras.
* Detección de animales.

Vision también permite el uso de modelos Core ML personalizados para tareas como clasificación o detección de objetos.

## Ejemplo de detección de texto con Vision
![](https://i.ibb.co/fn08r7V/app.png)

En este ejemplo utilizaremos el framework Vision para detectar un párrafo en una imágen y convertirlo a texto.

Primero debemos de crear un nuevo proyecto en Xcode como Single View App y en el **Main.storyboard** crea la siguente pantalla.

![](https://i.ibb.co/yXrDp9W/pantalla.png)

Después ligaremos el TextView y el Botón al ViewController.swift.

* El TextView lo nombraremos  __*scannedText*__ y será de tipo __*Outlet*__
* El Botón  se ligará como tipo __*Action*__ y lo nombraremos __*scanButton*__

Ahora mandarémos a llamar al framework de la siguente manera:
```
import VisionKit
import Vision
```

Crearemos una extensión del ViewController.

```
extension ViewController: VNDocumentCameraViewControllerDelegate {
    
}
```

Pondrémos las siguientes variables dentro de nuestra clase ViewController:

```
var textRecognitionRequest = VNRecognizeTextRequest()
var recognizedText = ""
```

Dentro de la funcion scanButton creada al ligar el botón y el controlador, meteremos el siguente codigo:

```
 @IBAction func scanButton(_ sender: Any) {
    let documentCameraViewController = VNDocumentCameraViewController()
    documentCameraViewController.delegate = self
    self.present(documentCameraViewController, animated: true, completion: nil)
}
```
Este código nos ayudará a poder prender la camara en el modo escáner de documentos .

Seguido a eso crearemos esta función, la cual nos permitirá obtener una imágen y poder trabajar con ella para reconocer el párrafo y convertilo a texto.

```
func documentCameraViewController(_ controller: VNDocumentCameraViewController, didFinishWith scan: VNDocumentCameraScan) {

    let image = scan.imageOfPage(at: 0)
    let handler = VNImageRequestHandler(cgImage: image.cgImage!, options: [:])
    do {
        try handler.perform([textRecognitionRequest])
    } catch {
        print(error)
    }
    controller.dismiss(animated: true)
}
```

Por último dentro de la función ViewDidLoad( ), debajo de super.viewDidLoad() pondremos el siguente código, el cual al obtener la imágen aplicará los algorítmos del kit Vision para poder reconocer el texto y presentarlo en el TextView.

```
textRecognitionRequest = VNRecognizeTextRequest(completionHandler: { (request, error) in
    if let results = request.results, !results.isEmpty {
        if let requestResults = request.results as? [VNRecognizedTextObservation] {
            self.recognizedText = ""
            for observation in requestResults {
                guard let candidiate = observation.topCandidates(1).first else { return }
                                   
                self.recognizedText += candidiate.string
                
                self.recognizedText += "\n"
            }
                self.scannedText.text = self.recognizedText
        }
    }
})
textRecognitionRequest.recognitionLevel = .accurate
textRecognitionRequest.usesLanguageCorrection = false
textRecognitionRequest.customWords = ["@gmail.com", "@outlook.com", "@yahoo.com", "@icloud.com"]
```