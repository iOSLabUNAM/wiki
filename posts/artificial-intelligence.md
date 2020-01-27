# Inteligencia Artificial en iOS

- [Definición de Inteligencia Artificial](#inteligencia-artificial)

- [Definición de Machine Learning](#machine-learning)

- [Definición de Modelo](#modelo)

- [Ejemplo Create ML](#cómo-crear-un-modelo-utilizando-createml)

- [Ejemplo de CoreML](#cómo-integrar-un-modelo-utilizando-coreml)


### Inteligencia Artificial
Consiste en el desarrollo de sistemas computacionales capaces de llevar a cabo tareas que normalmente requieren inteligencia humana; tales como percepción visual, reconocimiento de lenguaje, toma de decisiones y traducción, entre otros.
___

### Machine Learning 
Es una manera de aplicar la Inteligencia Artificial que provee a los sistemas con la habilidad de aprender automáticamente y tener mejoras continuas basadas en la experiencia sin ser explícitamente programados.
___

### Modelo
Un modelo en “Machine Learning” consiste en la representación matemática de un proceso en la vida real. Para generar un modelo se necesita proveer datos de entrenamiento a un algoritmo para que pueda aprender de ellos.
___

## Cómo crear un modelo utilizando CreateML
En este ejemplo generaremos un modelo que sepa clasificar imágenes en dos categorías: manzanas y plátanos.  
Necesitamos crear dos conjuntos de imágenes, uno para entrenar el modelo (Training Data) y otro para probarlo (Testing Data); los cuales a su vez estarán divididos en plátanos (Banana) y manzanas (Apple). Se recomienda tener una división del 80% de datos para entrenar y 20% para probar.
Una vez que se tienen listos los datos, creamos un nuevo Playground seleccionando las opciones “macOS” y “Blank”.

![Paso 1](https://firebasestorage.googleapis.com/v0/b/cinema-fa766.appspot.com/o/ia%2Fstep1.png?alt=media&token=1dfa2391-2d8a-40f1-a2f2-172c7e8c67d9)


Nombrar y crear el Playground e ingresar el código:

```swift
import CreateMLUI
 
let builder = MLImageClassifierBuilder()
builder.showInLiveView()
```

Por medio de la clase MLImageClassifierBuilder instanciamos un clasificador de imágenes que entrenaremos a través del Playground.

1. Activar “Live View” para que se muestre la interfaz gráfica.
![Paso 2](https://firebasestorage.googleapis.com/v0/b/cinema-fa766.appspot.com/o/ia%2Fstep2.png?alt=media&token=bd465726-e744-4b11-90ba-763e168ae522)

2. Arrastrar carpeta “Training Data” hacia el área asignada por la interfaz.
![Paso 3](https://firebasestorage.googleapis.com/v0/b/cinema-fa766.appspot.com/o/ia%2Fstep3.png?alt=media&token=33e8c5ad-033c-4458-8617-9963131fe202)
 
3. Arrastrar carpeta “Testing Data” hacia el área asignada por la interfaz.
![Paso 4](https://firebasestorage.googleapis.com/v0/b/cinema-fa766.appspot.com/o/ia%2Fstep4.png?alt=media&token=e3b66f8d-f9d2-4b83-98af-f1cc2197654d)

Al finalizar el procesamiento de los datos se muestra una tabla con 3 porcentajes (Training, Validation y Evaluation). “Training” nos indica el porcentaje de imágenes que el modelo ha podido utilizar para el entrenamiento de manera exitosa, “Validation” nos muestra el porcentaje de imágenes que el clasificador acertó (con respecto a un subconjunto que Xcode separa de los datos de entrenamiento “Training Data”) y finalmente “Evaluation” nos muestra el porcentaje de imágenes que el clasificador acertó pero del conjunto que se designó desde un inicio para probar (Testing Data).
![Paso 5](https://firebasestorage.googleapis.com/v0/b/cinema-fa766.appspot.com/o/ia%2Fstep5.png?alt=media&token=7d0d9e8e-0662-4451-945a-5f71c84d8ccd)

4. Modificar los datos del modelo (nombre, autor, metadatos, ubicación) y guardarlo.
![Paso 6](https://firebasestorage.googleapis.com/v0/b/cinema-fa766.appspot.com/o/ia%2Fstep6.png?alt=media&token=b835d377-77a6-4bf1-8dd2-c07cd2807adc)
___

## Cómo integrar un modelo utilizando CoreML

Arrastrar nuestro modelo dentro del proyecto.

![Paso 7](https://firebasestorage.googleapis.com/v0/b/cinema-fa766.appspot.com/o/ia%2Fstep7.png?alt=media&token=2a9dc931-54b3-4238-beea-b7a6df907da9)

Dentro del ViewController integrar el siguiente código:

```swift
import CoreML

Class ViewController: UIViewController {

//Utilizar nombre del modelo importado
var model: FruitClassifier! 
 
override func viewWillAppear(_ animated: Bool) {
    model = FruitClassifier()
}

//Código para capturar la imagen y convertirla al formato recibido por el modelo

guard let prediction = try? model.prediction(image: pixelBuffer!) else {
    return
}

classifier.text = "I think this is a \(prediction.classLabel).”

}
```

Podemos observar que en la variable “model” creamos una instancia del modelo que entrenamos previamente para la clasificación de manzanas y plátanos.

Posteriormente utilizamos el método “prediction”, el cual recibe una imagen y la clasifica de acuerdo al entrenamiento brindado al modelo.
Finalmente mostramos el resultado de la predicción obtenida por medio de la etiqueta “classifier”.

Este ejemplo sólo contiene las líneas de código necesarias para utilizar el modelo, para poder generar un proyecto funcional es necesario agregar la funcionalidad para la captura o el ingreso de la imagen, así como su procesamiento para cumplir con el formato requerido por el modelo (299 x 299 pixeles).

