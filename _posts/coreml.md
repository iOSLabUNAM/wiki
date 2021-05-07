---
title: CoreML
category: development kit
layout: post
---

## CoreML

CoreML es la base de los frameworks y la funcionalidad específicos del dominio. Core ML admite Vision para analizar imágenes, Lenguaje Natural para procesar texto, Voz para convertir audio a texto y Análisis de sonido para identificar sonidos en audio. Core ML se construye sobre primitivas de bajo nivel como Accelerate y BNNS, así como Metal Performance Shaders.

![coreml2](/wiki/assets/img/coreml2.png)

Core ML integra modelos de machine learning en una aplicación. Core ML proporciona una representación unificada para todos los modelos. Su aplicación utiliza las API de Core ML y los datos del usuario para hacer predicciones y entrenar o ajustar modelos, todo en el dispositivo del usuario.

![coreml1](/wiki/assets/img/coreml1.png)

Un modelo es el resultado de aplicar un algoritmo de machine learning a un conjunto de datos de entrenamiento. Utiliza un modelo para hacer predicciones basadas en nuevos datos de entrada. Los modelos pueden realizar una amplia variedad de tareas que serían difíciles o poco prácticas para escribir en el código. Por ejemplo, puede entrenar a un modelo para categorizar fotos o detectar objetos específicos dentro de una foto directamente desde sus píxeles.

### Primeros pasos para iniciar con CoreML:

* __Tener un modelo CoreML:__
Core ML admite una variedad de modelos de aprendizaje automático, que incluyen redes neuronales, conjuntos de árboles, máquinas de vectores de soporte y modelos lineales generalizados. Core ML requiere el formato de modelo Core ML (modelos con una extensión de archivo .mlmodel).
Con Create ML y sus propios datos, puede entrenar modelos personalizados para realizar tareas como reconocer imágenes, extraer significado del texto o encontrar relaciones entre valores numéricos. Los modelos entrenados con Create ML están en el formato de modelo Core ML y están listos para usar en su aplicación.

![coreml3](/wiki/assets/img/coreml3.png)
Ejemplo usando un entrenamiento de imagenes de flores
![coreml4](/wiki/assets/img/coreml4.png)

* __Integrar el modelo CoreML a la aplicacion:__
Utilizando un modelo ya hecho de apple, haremos un reconocimiento de mariscos.
[![descarga](/wiki/assets/img/coreml5.png)](https://docs-assets.developer.apple.com/coreml/models/Inceptionv3.mlmodel)
1.  __Creamos un proyecto nuevo llamado Mariscos, en Xcode:__
![ejemplo](/wiki/assets/img/ejemplo.png)
2.  __Integramos el modelo que descargamos a nuestro proyecto:__
![ejemplo1](/wiki/assets/img/ejemplo1.png)
![ejemplo2](/wiki/assets/img/ejemplo2.png)
3.  __Importamos los frameworks, y protocolos en el ViewController:__
![ejemplo3](/wiki/assets/img/ejemplo3.png)
4.  __Integramos los objetos bar buttom item y image view:__
![ejemplo4](/wiki/assets/img/ejemplo4.png)
5.  __Integramos los IBOutlets y IBActions que necesitamos:__
![ejemplo5](/wiki/assets/img/ejemplo5.png)
6.  __Integrar funciones necesarias en el View Controller para hacer las coincidencias:__
![ejemplo6](/wiki/assets/img/ejemplo6.png)
7.  __Probar la app en un iPhone:__
![ejemplo7](/wiki/assets/img/ejemplo7.png)
8.  __Revisar los resultados en consola y determinar el porcentaje de confianza:__
![ejemplo8](/wiki/assets/img/ejemplo8.png)
Como podemos ver la app logro reconocer que se le esta presentando aun lobster.
* __Convertir modelos entrenados a Core ML:__
Si su modelo se crea y se entrena utilizando un marco de aprendizaje automático de terceros compatible, puede usar las herramientas Core ML o una herramienta de conversión de terceros, como el convertidor MXNet o el convertidor TensorFlow, para convertir su modelo al Core ML formato del modelo De lo contrario, debe crear sus propias herramientas de conversión.

    Core ML Tools es un paquete de Python que convierte una variedad de tipos de modelos al formato de modelo Core ML. La Tabla enumera los modelos admitidos y los frameworks de terceros
![coreml5](/wiki/assets/img/coreml6.png)
