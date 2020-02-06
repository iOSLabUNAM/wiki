# ¿Qué es Machine Learning?


Machine Learning es una capa habilitadora horizontal, este enfoque le da a la computadora instrucciones que le permiten aprender de los datos sin nuevas instrucciones paso a paso por parte del programador. Esto significa que las computadoras se pueden usar para tareas nuevas y complicadas que no se pueden programar manualmente. Cosas como aplicaciones de reconocimiento de fotos para personas con discapacidad visual o traducir imágenes al habla.

El proceso básico de Machine Learning es proporcionar datos de entrenamiento a un algoritmo de aprendizaje. El algoritmo de aprendizaje genera un nuevo conjunto de reglas, basado en inferencias de los datos. En esencia, esto genera un nuevo algoritmo, formalmente denominado modelo de aprendizaje automático. Al usar diferentes datos de entrenamiento, el mismo algoritmo de aprendizaje podría usarse para generar diferentes modelos. Por ejemplo, el mismo tipo de algoritmo de aprendizaje podría usarse para enseñarle a la computadora cómo traducir idiomas o predecir el mercado de valores.

Inferir nuevas instrucciones de los datos es la fuerza central del aprendizaje automático. También destaca el papel crítico de los datos: cuantos más datos estén disponibles para entrenar el algoritmo, más aprenderá. De hecho, muchos avances recientes en IA no se han debido a innovaciones radicales en los algoritmos de aprendizaje, sino a la enorme cantidad de datos habilitados por Internet. 

* **_Es el campo de estudio que le da a las computadoras la habilidad de aprender sin ser explicitamente programadas._**
    ###### -Arthur Samuel

## Tipos de entrenamientos de machine learning:

#####  Aunque un modelo de aprendizaje automático puede aplicar una combinación de diferentes técnicas, los métodos de aprendizaje generalmente se pueden clasificar en tres tipos generales:

* __Supervised Machine Learning__
    ###### El algoritmo de aprendizaje recibe datos etiquetados y la salida deseada. Por ejemplo, las imágenes de perros con la etiqueta "perro" ayudarán al algoritmo a identificar las reglas para clasificar imágenes de perros.
* __Unsupervised Machine Learning__
    ###### Los datos proporcionados al algoritmo de aprendizaje no están etiquetados y se le pide al algoritmo que identifique patrones en los datos de entrada. Por ejemplo, el sistema de recomendación de un sitio web de comercio electrónico donde el algoritmo de aprendizaje descubre artículos similares que a menudo se compran juntos.

* __Reinforcement Machine Learning__
    ###### Se trata de tomar medidas adecuadas para maximizar la recompensa en una situación particular. Es utilizado por varios softwares y máquinas para encontrar el mejor comportamiento o ruta posible que debe tomar en una situación específica. El aprendizaje por refuerzo difiere del aprendizaje supervisado en una forma en que en el aprendizaje supervisado los datos de entrenamiento tienen la clave de respuesta, por lo que el modelo se entrena con la respuesta correcta en sí misma, mientras que en el aprendizaje por refuerzo no hay respuesta, pero el agente de refuerzo decide qué hacer. para realizar la tarea dada. En ausencia de un conjunto de datos de entrenamiento, seguramente aprenderá de su experiencia.


### Supervised Machine Learning

* __Discrete Data:__  El término discreto implica distinto o separado. Entonces, los datos discretos se refieren al tipo de datos cuantitativos que dependen de los recuentos. Contiene solo valores finitos, cuya subdivisión no es posible. Incluye solo aquellos valores que solo se pueden contar en números enteros o enteros y están separados, lo que significa que los datos no se pueden dividir en fracción o decimal.
* __Continuos Data:__  Los datos continuos se describen como un conjunto ininterrumpido de observaciones; eso se puede medir en una escala. Puede tomar cualquier valor numérico, dentro de un rango finito o infinito de valor posible. Estadísticamente, el rango se refiere a la diferencia entre la observación más alta y la más baja. Los datos continuos se pueden dividir en fracciones y decimales, es decir, se pueden subdividir significativamente en partes más pequeñas de acuerdo con la precisión de la medición.

### Unsupervised Machine Learning

* __Clustering:__ El clustering implica la agrupación de objetos similares en un conjunto conocido como clustering. Es probable que los objetos en un grupo sean diferentes en comparación con los objetos agrupados en otro grupo. La agrupación en clúster es una de las tareas principales en la minería de datos exploratoria y también es una técnica utilizada en el análisis de datos estadísticos. Si bien la agrupación no es un algoritmo específico, es una tarea general que se puede resolver mediante varios algoritmos. Algunos de los métodos de agrupamiento populares que se utilizan incluyen jerarquía, particionamiento, basado en la densidad y en el modelo.

### Reinforcement Machine Learning

* __Agent:__ Es una entidad asumida que realiza acciones en un entorno para obtener alguna recompensa.
* __Environment:__ Un escenario que un agente tiene que enfrentar.
* __Reward:__ Un retorno inmediato dado a un agente cuando él o ella realiza una acción o tarea específica.
* __State:__ Estado se refiere a la situación actual que devuelve el medio ambiente.
* __Policy:__ Es una estrategia que aplica el agente para decidir la próxima acción basada en el estado actual.
* __Value:__ Se espera un rendimiento a largo plazo con descuento, en comparación con la recompensa a corto plazo.
* __Value Function:__ Especifica el valor de un estado que es la cantidad total de recompensa. Es un agente que debería esperarse a partir de ese estado.
* __Model of the environment:__ Esto imita el comportamiento del medio ambiente. Le ayuda a hacer inferencias y también a determinar cómo se comportará el entorno.
* __Model based methods:__ Es un método para resolver problemas de aprendizaje por refuerzo que utilizan métodos basados ​​en modelos.
* __Q value or action value (Q):__ El valor Q es bastante similar al valor. La única diferencia entre los dos es que toma un parámetro adicional como una acción actual.

## CoreML 
Core ML es la base de los frameworks y la funcionalidad específicos del dominio. Core ML admite Vision para analizar imágenes, Lenguaje Natural para procesar texto, Voz para convertir audio a texto y Análisis de sonido para identificar sonidos en audio. Core ML se construye sobre primitivas de bajo nivel como Accelerate y BNNS, así como Metal Performance Shaders.

![coreml2](/coreml2.png)

Core ML integra modelos de machine learning en una aplicación. Core ML proporciona una representación unificada para todos los modelos. Su aplicación utiliza las API de Core ML y los datos del usuario para hacer predicciones y entrenar o ajustar modelos, todo en el dispositivo del usuario.

![coreml1](coreml1.png)

Un modelo es el resultado de aplicar un algoritmo de machine learning a un conjunto de datos de entrenamiento. Utiliza un modelo para hacer predicciones basadas en nuevos datos de entrada. Los modelos pueden realizar una amplia variedad de tareas que serían difíciles o poco prácticas para escribir en el código. Por ejemplo, puede entrenar a un modelo para categorizar fotos o detectar objetos específicos dentro de una foto directamente desde sus píxeles.

### Primeros pasos para iniciar con CoreML:

* __Tener un modelo CoreML:__
Core ML admite una variedad de modelos de aprendizaje automático, que incluyen redes neuronales, conjuntos de árboles, máquinas de vectores de soporte y modelos lineales generalizados. Core ML requiere el formato de modelo Core ML (modelos con una extensión de archivo .mlmodel).
Con Create ML y sus propios datos, puede entrenar modelos personalizados para realizar tareas como reconocer imágenes, extraer significado del texto o encontrar relaciones entre valores numéricos. Los modelos entrenados con Create ML están en el formato de modelo Core ML y están listos para usar en su aplicación.

![coreml3](coreml3.png)
Ejemplo usando un entrenamiento de imagenes de flores
![coreml4](coreml4.png)

* __Integrar el modelo CoreML a la aplicacion:__
Utilizando un modelo ya hecho de apple, haremos un reconocimiento de mariscos. 
[![descarga](coreml5.png)](https://docs-assets.developer.apple.com/coreml/models/Inceptionv3.mlmodel)
1.  __Creamos un proyecto nuevo llamado Mariscos, en Xcode:__
![ejemplo](ejemplo.png)
2.  __Integramos el modelo que descargamos a nuestro proyecto:__
![ejemplo1](ejemplo1.png)
![ejemplo2](ejemplo2.png)
3.  __Importamos los frameworks, y protocolos en el ViewController:__
![ejemplo3](ejemplo3.png)
4.  __Integramos los objetos bar buttom item y image view:__
![ejemplo4](ejemplo4.png)
5.  __Integramos los IBOutlets y IBActions que necesitamos:__
![ejemplo5](ejemplo5.png)
6.  __Integrar funciones necesarias en el View Controller para hacer las coincidencias:__
![ejemplo6](ejemplo6.png)
7.  __Probar la app en un iPhone:__
![ejemplo7](ejemplo7.png)
8.  __Revisar los resultados en consola y determinar el porcentaje de confianza:__
![ejemplo8](ejemplo8.png)
Como podemos ver la app logro reconocer que se le esta presentando aun lobster.
* __Convertir modelos entrenados a Core ML:__
Si su modelo se crea y se entrena utilizando un marco de aprendizaje automático de terceros compatible, puede usar las herramientas Core ML o una herramienta de conversión de terceros, como el convertidor MXNet o el convertidor TensorFlow, para convertir su modelo al Core ML formato del modelo De lo contrario, debe crear sus propias herramientas de conversión.

    Core ML Tools es un paquete de Python que convierte una variedad de tipos de modelos al formato de modelo Core ML. La Tabla enumera los modelos admitidos y los frameworks de terceros
![coreml5](coreml6.png)


