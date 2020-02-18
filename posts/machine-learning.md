---
title: ¿Qué es Machine Learning?
category: foundations
---

# ¿Qué es Machine Learning?

Machine Learning es una capa habilitadora horizontal, este enfoque le da a la computadora instrucciones que le permiten aprender de los datos sin nuevas instrucciones paso a paso por parte del programador. Esto significa que las computadoras se pueden usar para tareas nuevas y complicadas que no se pueden programar manualmente. Cosas como aplicaciones de reconocimiento de fotos para personas con discapacidad visual o traducir imágenes al habla.

El proceso básico de Machine Learning es proporcionar datos de entrenamiento a un algoritmo de aprendizaje. El algoritmo de aprendizaje genera un nuevo conjunto de reglas, basado en inferencias de los datos. En esencia, esto genera un nuevo algoritmo, formalmente denominado modelo de aprendizaje automático. Al usar diferentes datos de entrenamiento, el mismo algoritmo de aprendizaje podría usarse para generar diferentes modelos. Por ejemplo, el mismo tipo de algoritmo de aprendizaje podría usarse para enseñarle a la computadora cómo traducir idiomas o predecir el mercado de valores.

Inferir nuevas instrucciones de los datos es la fuerza central del aprendizaje automático. También destaca el papel crítico de los datos: cuantos más datos estén disponibles para entrenar el algoritmo, más aprenderá. De hecho, muchos avances recientes en IA no se han debido a innovaciones radicales en los algoritmos de aprendizaje, sino a la enorme cantidad de datos habilitados por Internet.

> Es el campo de estudio que le da a las computadoras la habilidad de aprender sin ser explicitamente programadas.  _- Arthur Samuel_

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
