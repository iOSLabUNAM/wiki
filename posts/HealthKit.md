# HealthKit. 

![HK](https://developer.apple.com/assets/elements/icons/healthkit/healthkit-96x96_2x.png)

**[HealthKit](https://developer.apple.com/healthkit/)** es un framework de desarrollo usado para acceder a datos almacenados en la **Health app**.
**Health app** sirve como un repositorio central para datos de salud y fitness en iOS. 
Con el permiso del usuario, las apps construidas con **HealthKit** pueden comunicarse con la **Health app** para acceder y compartir informacion.
Un usuario puede permitir, por ejemplo, que una app de nutricion obtenga datos sobre el peso y las actividades diarias de forma que la app pueda definir un consumo optimo de calorias y hacer recomendaciones nutricionales.

**Threading**. El almacèn (store) del HealthKit  opera bajo un hilo seguro (thread-safe), y gran parte de sus objetos son inmutables. Tambien se puede usar en multiprocesos (multithreaded).
Tanto el iPhone como el Apple Watch almacenan los datos del healthkit por separado pero se pueden sincronizar automaticamente, sin embargo, para guardar espacio el Apple Watch elimina datos que sean muy antiguos. 
**HealthKit no esta disponible para iPad**

## [Privacidad del Usuario](https://developer.apple.com/documentation/healthkit/protecting_user_privacy).

Los datos del **HealthKit** deben ser almacenados localmente en el dispositivo del usuario. El almacèn para HealthKit
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

* Specify Required Clinical Record Types. If your app requires access to specific clinical record data to function properly, specify the required clinical record types in your app’s Info.plist file using the NSHealthRequiredReadAuthorizationTypeIdentifiers key. This key defines the data types that your app must have permission to read. Set the value to an array of strings containing the type identifiers for your required types. you must specify three or more required clinical record types.

* Se deben crear politicas de privacidad para cualquier app que use el framework de HealthKit. Se puede encontrar documentacion para crear politicas de privacidad en los siguientes sitios: 

    - [Personal Health Record model (for non-HIPAA apps)](http://www.healthit.gov/policy-researchers-implementers/personal-health-record-phr-model-privacy-notice)
    - [HIPAA model (for HIPAA covered apps)](http://www.hhs.gov/ocr/privacy/hipaa/modelnotices.html)

## [HealthKit Data](https://developer.apple.com/documentation/healthkit/data_types). 

Los developers no pueden crear tipos o unidades de datos propios al trabajar con HealthKit, en su lugar, se provee una amplia variedad de los mismos. De igual forma se provee un gran numero de clases y subclases.
Los tipos de datos que HealthKit puede ofrecer en su almacèn (store) son: 
- Characteristic data. Estos representan items que tipicamente no cambian como el cumpleaños del usuario, tipo de sangre, sexo y tipo de piel. 
- Sample data. Gran parte de los datos de salud del usuario son almacenados en _samples_ que representan datos en un punto particular del tiempo. 
- Workout data. Informarmacion sobre fitness y ejercicios son almacenados en HKWorkout samples, por ejemplo.
- Source data. Cada sample almacena informacion sobre su origen, por ejemplo, el objeto HKSourceRevision contiene informacion sobre la app o el dispositivo que almacena el tipo de _sample_, y el objeto HKDevice contiene informacion sobre el hardware del dispositivo que genero los datos.  
- Deleted objects. Una instancia de HKDeletedObject es usada para almacenar temporalmente el UUID de un item que ha sido eliminado del almacen (store) de HealthKit. 

## [_Object properties_ y _Samples_](https://developer.apple.com/documentation/healthkit/about_the_healthkit_framework)

La clase *HKObject* es la superclase de todos los tipos de _samples_ que administra HealthKit. Todas sus subclases son inmutables y cada objeto de la clase tiene las siguientes propiedades: 
* UUID. Un identificador unico para cada tipo de _log_ o entrada. 
* Metadata. Es un diccionario con informacion adicional sobre la entrada. 
* Source Revision. La fuente del _sample_.  Dicha fuente puede ser un dispositivo que guarde directamente datos hacia HealthKit o una app que use este framework. 
* Device. El hardware del dispositivo que genero los datos almacenados en el _sample_. 

To create a type object, call the appropriate HKObjectType class method, and pass in the desired type identifier.

```swift
let bloodType = HKObjectType.characteristicType(forIdentifier: .bloodType)

let caloriesConsumed = HKObjectType.quantityType(forIdentifier: .dietaryEnergyConsumed)

let sleepAnalysis = HKObjectType.categoryType(forIdentifier: .sleepAnalysis)
```
La clase *HKSample* es una subclase de *HKObject*.  Los objetos _Sample_ son aquellos que representan datos en cualquier punto particular del tiempo y tienen las siguientes propiedades: 
* Type. El tipo de _sample_ como analisis de sueño, estatura o conteo de pasos. 
* Start date. Tiempo de inicio de procesamiento de datos del _sample_. 
* End date. Tiempo final del _sample_. 

    A su vez, los _samples_ estan divididos en 4 subclases concretas: 

    * Category samples. Datos que pueden ser clasificados en un set finito de categorias. 
    * Quantity samples. Datos que pueden ser almacenados como valores numericos. Se incluyen estatura y peso, temperatura corporal, pulso cardiaco, conteo de pasos, etc. 
    * Correlations. Compuesto de datos que representan uno o mas _samples_ de comida o presion arterial. 
    * Workouts. Datos que representan actividades fisicas como correr, nadar o jugar. Estos generalmente tienen propiedades de  tipo, duracion, distancia y calorias quemadas.  

## Implementacion del HealthKit [(HealthKit Setup)](https://developer.apple.com/documentation/healthkit/setting_up_healthkit#2962431).

Para usar HealthKit se tienen que atender los siguientes pasos: 

1. Habilitar HealthKit en tu app.  
In Xcode, select the project and turn on the HealthKit capability (see Figure 1). Only enable the Health Records checkbox if your app needs to access the user’s clinical records. App Review may reject apps that enable the Health Records capability if the app doesn’t use the Health Record data.

![Enable HealthKit capabilities](https://docs-assets.developer.apple.com/published/749e5c40bb/c46af629-7d07-4402-98fc-c9657cfc5594.png)

For a detailed discussion about enabling capabilities, see Configure HealthKit in Xcode Help. [Configuracion de HealthKit](https://help.apple.com/xcode/mac/current/#/dev1a5823416)
When you enable the HealthKit capabilities on an iOS app, Xcode adds HealthKit to the list of required device capabilities. This prevents users from purchasing or installing the app on devices that don’t support HealthKit.


2. Asegurar que HealthKit este disponible en el dispositivo actual. 
Call the isHealthDataAvailable() method to confirm that HealthKit is available on the user's device.

```swift
if HKHealthStore.isHealthDataAvailable() {
    // Add code to use HealthKit here.
}
```
Call this method before calling any other HealthKit methods. If HealthKit is not available on the device (for example, on an iPad), other HealthKit methods fail with an errorHealthDataUnavailable error. If HealthKit is restricted (for example, in an enterprise environment), the methods fail with an errorHealthDataRestricted error.


3. Crear tu almacen de HealthKit (HealthKit store).
If HealthKit is both enabled and available, instantiate an HKHealthStore object for your app as shown:

```swift
let healthStore = HKHealthStore()
```
You need only a single HealthKit store per app. These are long-lived objects; you create the store once, and keep a reference for later use.


4. Solicitar permisos para leer y compartir datos. 
To help protect the user’s privacy, HealthKit requires fine-grained authorization. You must request permission to both read and share each data type used by your app before you attempt to access or save the data. However, you don’t need to request permission for all data types at once. Instead, it may make more sense to wait until you need to access the data before asking for permission.
The example below shows the SpeedySloth app asking for permission to read and share energy burned, cycling distance, walking or running distance, and heart rate samples.

```swift
let allTypes = Set([HKObjectType.workoutType(),
                    HKObjectType.quantityType(forIdentifier: .activeEnergyBurned)!,
                    HKObjectType.quantityType(forIdentifier: .distanceCycling)!,
                    HKObjectType.quantityType(forIdentifier: .distanceWalkingRunning)!,
                    HKObjectType.quantityType(forIdentifier: .heartRate)!])

healthStore.requestAuthorization(toShare: allTypes, read: allTypes) { (success, error) in
    if !success {
        // Handle the error here.
    }
}
```
Any time your app requests new permissions, the system displays a form with all the requested data types shown.

![Request permission for the Fit app](https://docs-assets.developer.apple.com/published/b29fb46f50/fddfad5c-7cc0-4aa9-a643-19d7e9d3893d.png)

You must also provide custom messages for the permissions sheet. Xcode requires a separate custom message for reading and writing HealthKit data. In your app’s Info.plist, set the NSHealthShareUsageDescription key to customize the message for reading data. Set the NSHealthUpdateUsageDescription key to customize the message for writing data.
If the user grants permission to share a data type, you can create new samples of that type and save them to the HealthKit store. However, before attempting to save any data, check to see if your app is authorized to share that data type by calling the authorizationStatus(for:) method. If you have not yet requested permission, any attempts to save fail with an HKError.Code.errorAuthorizationNotDetermined error.

## [Guardar datos en HealthKit](https://developer.apple.com/documentation/healthkit/saving_data_to_healthkit). 



### [Crear y Compartir HealthKit _Samples_](https://developer.apple.com/documentation/healthkit/samples) 


## [Leer Datos de HealthKit.](https://developer.apple.com/documentation/healthkit/reading_data_from_healthkit#overview)


###  [Usar _Queries_ para solicitar _sample_ datos de HealthKit](https://developer.apple.com/documentation/healthkit/queries) 


##Para consultar mucha mas información: [Health & Fitness Videos for iOS developers](https://developer.apple.com/videos/frameworks/health-and-fitness)


