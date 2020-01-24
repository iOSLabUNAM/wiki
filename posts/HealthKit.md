# HealthKit. 

**HealthKit** es un framework de desarrollo usado para acceder a datos almacenados en la **Health app**.
**Health app** sirve como un repositorio central para datos de salud y fitness en iOS. 
Con el permiso del usuario, las apps construidas con **HealthKit** pueden comunicarse con la **Health app** para acceder y compartir informacion.
Un usuario puede permitir, por ejemplo, que una app de nutricion obtenga datos sobre el peso y las actividades diarias de forma que la app pueda definir un consumo optimo de calorias y hacer recomendaciones nutricionales.

Threading. The HealthKit store is thread-safe, and most HealthKit objects are immutable. In general, you can use HealthKit safely in a multithreaded environment.
Syncing Data Between Devices. iPhone and Apple Watch each have their own HealthKit store, and data is automatically synced between the phone and watch. To save space, old data is periodically purged from Apple Watch. HealthKit is not available on iPad.

## Privacidad del Usuario.

Los datos del **HealthKit** deben ser almacenados localmente en el dispositivo del usuario. El almacenamiento para HealthKit
es encriptado cuando el dispositivo es bloqueado y solo puede ser accesado por una app autorizada. 
Como resultado, no se pueden leer datos del almacenamiento del Healthkit cuando el app trabaja en un hilo secundario (background): sin embargo, las apps a desarrollar pueden seguir escribiendo datos en el almacenamiento incluso cuando el dispositivo esta bloqueado. Healthkit toma estos datos y los guarda en el almacenamiento encriptado tan pronto como el celular es desbloqueado. 

Al trabajar con **Health app** es importante tomar en cuenta los siguientes puntos: 
* Pide acceso a los datos de salud solamente cuando sea necesario.
* Usa la pantalla de permiso standard para aclarar que se quiere acceder a los datos de salud. Evita añadir vistas diferentes de la vista standard para pedir permisos.
* Siempre que se compartan datos de salud se debe hacer a traves de *Settings > Privacy* del sistema.  
* No uses iconos, imagenes y screenshots de la Health app en tu app de desarrollo, esto por motivos de copyright.
* No uses el termino *HealthKit*. Si necesitas explicar que tu app trabaja con datos de este framework, usa el termino **Health app**.
* **HealthKit** esta disenado igualmente para administrar y combinar datos de multiples dispositivos.
* El app ha desarrollar no debe acceder al API de HealthKit a menos que este diseñada precisamente para ofrecer servicios fitness o de salud.
* El rol de la app debe dejar en claro que cualquier _marketing_ y/o diseño de interfaz de usuario es sobre servicios fitness y/o de salud. No se debe usar datos del HealthKit para dar servicio a cualquier tipo de publicidad, o vender datos a revendedores de informacion o plataformas de publicidad.  
* Unicamente se deben compartir datos del HealthKit a terceros si estos tambien proveen servicios fitness o de salud al usuario que, al mismo tiempo,  debe dar permiso para que se compartan. 
* Se debe explicar claramente al usuario como se usaran sus datos. 
* Se deben crear politicas de privacidad para cualquier app que use el framework de HealthKit. Se puede encontrar documentacion para crear politicas de privacidad en los siguientes sitios: 

    - [Personal Health Record model (for non-HIPAA apps)] (http://www.healthit.gov/policy-researchers-implementers/personal-health-record-phr-model-privacy-notice)
    - [HIPAA model (for HIPAA covered apps)] (http://www.hhs.gov/ocr/privacy/hipaa/modelnotices.html)

## HealthKit Data. 

Developers cannot create custom data types or units. Instead, HealthKit provides a wide variety of data types and units.
Additionally, the framework uses a large number of subclasses, producing deep hierarchies of similar classes.

HealthKit saves a variety of data types in the HealthKit Store:
Characteristic data. These records represent items that typically do not change, such as the user’s birthdate, blood type, biological sex, and skin type.
Sample data. Most of the user’s health data is stored in samples that represent data at a particular point in time. 
Workout data. Information about fitness and exercise activities are stored as HKWorkout samples.
Source data. Each sample stores information about its source. The HKSourceRevision object contains information about the app or device that saved the sample. The HKDevice object contains information about the hardware device that generated the data.
Deleted objects. An HKDeletedObject instance is used to temporarily store the UUID of an item that has been deleted from the HealthKit store. You can use deleted objects to respond when an object is deleted by the user or another app.

## Propiedades de los Objetos y _Samples_

The HKObject class is the superclass of all HealthKit sample types. All HKObject subclasses are immutable. Each object has the following properties:
UUID. A unique identifier for that particular entry.
Metadata. A dictionary containing additional information about the entry.
Source Revision. The source of the sample. The source can be a device that directly saves data into HealthKit, or an app.
Device. The hardware device that generated the data stored in this sample.
The HKSample class is a subclass of HKObject. Sample objects represent data at a particular point in time. They have the following properties:
Type. The sample type, such as a sleep analysis sample, a height sample, or a step count sample.
Start date. The sample’s start time.
End date. The sample’s end time.

Samples are further divided into four concrete subclasses:
Category samples. Data that can be classified into a finite set of categories.
Quantity samples. Data that can be stored as numeric values. These include the user’s height and weight, the number of steps taken, the user’s temperature, and their pulse rate
Correlations. Composite data containing one or more samples to represent food and blood pressure.
Workouts. Data representing a physical activity, like running, swimming, or even play. Workouts often have type, duration, distance, and energy burned properties.

https://developer.apple.com/videos/frameworks/health-and-fitness

