---
title: HealthKit
category: development kit
layout: post
---

# HealthKit

![HK](https://developer.apple.com/assets/elements/icons/healthkit/healthkit-96x96_2x.png)

**[HealthKit](https://developer.apple.com/healthkit/)** es un framework de desarrollo usado para acceder a datos almacenados en la **Health app**.
**Health app** sirve como un repositorio central para datos de salud y fitness en iOS.
Con el permiso del usuario, las apps construidas con **HealthKit** pueden comunicarse con la **Health app** para acceder y compartir informacion.
Un usuario puede permitir, por ejemplo, que una app de nutricion obtenga datos sobre el peso y las actividades diarias de forma que la app pueda definir un consumo optimo de calorias y hacer recomendaciones nutricionales.

**Threading**. El almacèn de HealthKit (HealthKit Store) opera bajo un hilo seguro (thread-safe), y gran parte de sus objetos son inmutables. Tambien se puede usar en multiprocesos (multithreaded).
Tanto el iPhone como el Apple Watch almacenan los datos del healthkit por separado pero se pueden sincronizar automaticamente, sin embargo, para guardar espacio el Apple Watch elimina datos que sean muy antiguos.
**HealthKit no esta disponible para iPad**

## [Privacidad del Usuario](https://developer.apple.com/documentation/healthkit/protecting_user_privacy).

Los datos de HealthKit deben ser almacenados localmente en el dispositivo del usuario. El almacén para HealthKit
es encriptado cuando el dispositivo es bloqueado y solo puede ser accesado por una app autorizada.
Como resultado, no se pueden leer datos del almacenamiento del Healthkit cuando el app trabaja en un hilo secundario, sin embargo, las apps a desarrollar pueden seguir escribiendo datos en el almacenamiento incluso cuando el dispositivo esta bloqueado. Healthkit toma estos datos y los guarda en el almacenamiento encriptado tan pronto como el celular es desbloqueado.

Al trabajar con **Health app** es importante tomar en cuenta los siguientes puntos:
* Pide acceso a los datos de salud solamente cuando sea necesario.
* Usa la pantalla de permiso standard para aclarar que se quiere acceder a los datos de salud. Evita añadir vistas diferentes de la vista standard para pedir permisos.
* Siempre que se compartan datos de salud se debe hacer a traves de *Settings > Privacy* del sistema.
* No uses iconos, imagenes y screenshots de la Health app en tu app de desarrollo, esto por motivos de copyright.
* No uses el termino *HealthKit*. Si necesitas explicar que tu app trabaja con datos de este framework, usa el termino **Health app**.
* HealthKit esta disenado igualmente para administrar y combinar datos de multiples dispositivos.
* El app ha desarrollar no debe acceder al API de HealthKit a menos que este diseñada precisamente para ofrecer servicios fitness o de salud.
* El rol de la app debe dejar en claro que cualquier _marketing_ y/o diseño de interfaz de usuario es sobre servicios fitness y/o de salud. No se debe usar datos del HealthKit para dar servicio a cualquier tipo de publicidad, o vender datos a revendedores de informacion o plataformas de publicidad.
* Únicamente se deben compartir datos del HealthKit a terceros si estos tambien proveen servicios fitness o de salud al usuario que, al mismo tiempo,  debe dar permiso para que se compartan.
* Se debe explicar claramente al usuario como se usaran sus datos.
* Si la app en desarrollo requiere acceso a archivos con datos clinicos especificos para funcionar, hay que especificar los tipos de archivos clinicos requeridos en el Info.plist de la app usando la llave siguiente: **lNSHealthRequiredReadAuthorizationTypeIdentifiers**.
* Se deben crear politicas de privacidad para cualquier app que use el framework de HealthKit. Se puede encontrar documentacion para crear politicas de privacidad en los siguientes sitios:

    - [Personal Health Record model (for non-HIPAA apps)](http://www.healthit.gov/policy-researchers-implementers/personal-health-record-phr-model-privacy-notice)
    - [HIPAA model (for HIPAA covered apps)](http://www.hhs.gov/ocr/privacy/hipaa/modelnotices.html)

## [HealthKit Data](https://developer.apple.com/documentation/healthkit/data_types).

Los developers no pueden crear tipos o unidades de datos propios al trabajar con HealthKit, en su lugar, se provee una amplia variedad de los mismos. De igual forma se provee un gran numero de clases y subclases.
Los tipos de datos que HealthKit puede ofrecer en su almacèn (store) son:
- Characteristic data. Estos representan items que tipicamente no cambian como el cumpleaños del usuario, tipo de sangre, sexo y tipo de piel.
- Sample data. Gran parte de los datos de salud del usuario son almacenados en _samples_ que representan datos en un punto particular del tiempo.
- Workout data. Información sobre fitness y ejercicios son almacenados en HKWorkout samples, por ejemplo.
- Source data. Cada sample almacena informacion sobre su origen, por ejemplo, el objeto HKSourceRevision contiene informacion sobre la app o el dispositivo que almacena el tipo de _sample_, y el objeto HKDevice contiene informacion sobre el hardware del dispositivo que genero los datos.
- Deleted objects. Una instancia de HKDeletedObject es usada para almacenar temporalmente el UUID de un item que ha sido eliminado del almacen (store) de HealthKit.

## [_Object properties_ y _Samples_](https://developer.apple.com/documentation/healthkit/about_the_healthkit_framework)

La clase *HKObject* es la superclase de todos los tipos de _samples_ que administra HealthKit. Todas sus subclases son inmutables y cada objeto de la clase tiene las siguientes propiedades:
* UUID. Un identificador unico para cada tipo de _log_ o entrada.
* Metadata. Es un diccionario con informacion adicional sobre la entrada.
* Source Revision. La fuente del _sample_.  Dicha fuente puede ser un dispositivo que guarde directamente datos hacia HealthKit o una app que use este framework.
* Device. El hardware del dispositivo que genero los datos almacenados en el _sample_.

Para crear cualquier tipo de objeto, se debe llamar un metodo de la clase HKObjectType, y pasar el tipo deseado de identificador.

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

## Implementación del HealthKit [(HealthKit Setup)](https://developer.apple.com/documentation/healthkit/setting_up_healthkit#2962431).

Para usar HealthKit se tienen que atender los siguientes pasos:

#### 1. Habilitar HealthKit en tu app.
Dentro de Xcode, selecciona el proyecto y habilita HealthKit. Solo habilita Health Records si tu app necesita acceso al *historial clinico* del usuario. Al subir tu app al App Store, la revision de apps (App Review) puede rechazar apps que habiliten Health Records si la app no usa ningun dato del historial clinico.

![Enable HealthKit capabilities](https://docs-assets.developer.apple.com/published/749e5c40bb/c46af629-7d07-4402-98fc-c9657cfc5594.png)

Mas información para habilitar capacidades en la configuracion del HealthKit -> [Configuracion de HealthKit](https://help.apple.com/xcode/mac/current/#/dev1a5823416)

Cuando se habilita HealthKit en una app de iOS, Xcode añade HealthKit a la lista de capacidades requeridas del dispositivo, esto previene que usuarios con dispositivos que no tengan disponible HealthKit puedan comprar o instalar la app.

#### 2. Asegurar que HealthKit este disponible en el dispositivo actual.
Usa el metodo **isHealthDataAvailable()** para confirmar si HealthKit esta disponible en el dispositivo del usuario.

```swift
if HKHealthStore.isHealthDataAvailable() {
    // Add code to use HealthKit here.
}
```
Usa este metodo antes de usar cualquier otro metodo de HealthKit. Si Healthkit no esta disponible en el dispositivo, los metodos consecuentes fallaran con el error: **errorHealthDataUnavailable** (Por ej. en Ipads). Si el HealthKit esta restringido, los metodos consecuentes fallaran con el error: **errorHealthDataRestricted**.

#### 3. Crear tu almacén de HealthKit (HealthKit Store).
Si HealthKit esta disponible y habilitado, instancia un objeto de HKHealthStore:

```swift
let healthStore = HKHealthStore()
```
Solo se necesita una sola instancia de este objeto por app. Creas el store una vez y la referencua se guarda para usos posteriores.

#### 4. Solicitar permisos para leer y compartir datos.
Para proteger la privacidad del usuario, HealthKit requiere autorizaciones especificadas. Se debe pedir permiso tanto para leer como para compartir cada tipo de dato usado en la app antes de acceder o guardar los datos, sin embargo, no se necesitan permisos para acceder a todos los tipos de datos al mismo tiempo, en lugar de esto solo pide el permiso cada vez que se necesite acceso a cada cierto tipo de dato.

En el siguiente ejemplo se configuran los datos para lectura que en este caso son _conteo de pasos_ y _sexo_, y tambien se configura el _conteo de pasos_ para escritura. (en _sexo_ no se puede escribir ningun dato).
Finalmente se pide autorizacion y se pasan los datos de lectura al parametro _read_ y los datos de escritura al parametro _toShare_ .

```swift
let healthStore = HKHealthStore()

override func viewDidLoad() {
    super.viewDidLoad()
    // Do any additional setup after loading the view, typically from a nib.

    if HKHealthStore.isHealthDataAvailable() {
        let readDataTypes : Set = [HKObjectType.quantityType(forIdentifier: HKQuantityTypeIdentifier.stepCount)!,
                               HKObjectType.characteristicType(forIdentifier: HKCharacteristicTypeIdentifier.biologicalSex)!]

        let writeDataTypes : Set = [HKObjectType.quantityType(forIdentifier: HKQuantityTypeIdentifier.stepCount)!]

        healthStore.requestAuthorization(toShare: writeDataTypes, read: readDataTypes) { (success, error) in
            if !success {
                // Handle the error here.
            } else {
                // Do the work
            }
        }
    }
}
```
Cada vez que tu app pida permisos, el sistema desplegará una vista con los tipos de datos que requieran permisos.

![Request permission for the Fit app](https://www.devfright.com/wp-content/uploads/2018/07/permissions-300x534@2x.png)

Tambien se deben proveer mensajes que soliciten el permiso para leer o escribir datos de HealthKit. En el **Info.plist** de tu app usa la llave **NSHealthShareUsageDescription** para configurar el mensaje de escritura de datos.
Si el usuario concede permisos para compartir datos de algun tipo en especifico, se pueden crear _samples_ de ese tipo y guardarlos en el almacen de HealthKit (HealthKit Store), sin embargo, antes de guardar cualquier dato, se debe revisar si el app esta autorizada para compartir los datos usando el metodo: **authorizationStatus(for:)**. Si no se ha pedido permisos, cualquier intento de guardar datos mandara un error de tipo: **HKError.Code.errorAuthorizationNotDetermined**.

## [Guardar datos en HealthKit](https://developer.apple.com/documentation/healthkit/saving_data_to_healthkit).

Cuando se trata de guardar datos en HealthKit, se debe trabajar con _samples_. Puedes crear _samples_ nuevos y añadirlos al almacen (HealthKit Store). Aunque cada _sample_ se rige por un metodo diferente de configuracion, comparten un proceso similar:

1. Revisa el tipo de identificador de tus datos. Por ejemplo, para guardar el peso de un usuario, se usa  _bodyMass_ como identificador. Revisar [Tipo de datos](https://developer.apple.com/documentation/healthkit/data_types)
2. Usa el metodo adecuado en la clase HKObjectType para crear el tipo de objeto correcto para tus datos. Por ejemplo, para guardar el peso, se deberia crear un objeto del tipo _HKQuantityType_ usando el metodo **quantityType(forIdentifier:)**.
3. Instancia el objeto de la subclase _HKSample_ correspondiente usando el tipo de objeto.
4. Guarda el objeto en el Store usando el metodo: **save(_:withCompletion:)**.

Al guardar datos al almacen de HealthKit, se debe escoger entre usar un solo _sample_ para representar los datos o dividir los datos en multiples y pequeñoa _samples_. Un _sample_ grande es mas eficiente, sin embargo, multiples y pequeños _samples_ proveen al usuario una persepcion mas detallada de como cambian los datos a traves del tiempo.
Por ejemplo, al trabajar con rutinas de ejercitamiento (workouts), se puede escojer un muestre de alta frecuencia (de un minuto o menos por _sample_) para proveer estadisticas de intensidad y analizar el rendimiento detallado del usuario durante una rutina. Por otra parte, para actividades menos intensas, como conteo de pasos, seria recomendable usar _samples_ muestreados de una hora o menos. Esto permite producir graficas utiles del registro de datos por hora o un dia, sin embargo, las apps deberian evitar guardar _samples_ de datos mayores a 24 horas.

### [Crear y Compartir HealthKit _Samples_](https://developer.apple.com/documentation/healthkit/samples)
Al guardar gran parte de los datos de salud y fitness en HealthKit  se usa una subclase de HKSample. Todas las subclases de _samples_ guardan informacion en un momento determinado. Por ejemplo, si los _samples_ de _startDate_ y _endDate_ son los mismos, el _sample_ en general es un punto unico en el tiempo. Si _endDate_ termina despues de _startDate_, el _sample_ es un intervalo de tiempo.

HealthKit usa diferentes subclases de HKSample para almacenar diversos tipos de datos:
- Objetos de tipo**HKQuantitySample** almacenan cantidades, valores numericos y unidades. (Ej. Altura, ritmo cardiaco, calorias consumidas, etc.)
    * Guardar _Quantity Samples_ en HealthKit [Tutorial.](https://www.devfright.com/creating-and-saving-data-in-healthkit/)

- Objetos de tipo **HKCategorySample** almacenan una sola opcion de una lista pequeña. (Ej. Datos de fases del sueño como, "en cama", "durmiendo" o "despierto").
    * Guardar _Category Samples_ en HealthKit [Tutorial.](https://www.devfright.com/saving-category-samples-with-healthkit/)

- Objetos de tipo **HKCorrelation** combinan dos o mas _samples_ en un solo valor. (Ej. Alimentos y presion sanguinea) .

- HealthKit tambien tiene  mas subclases de algunos _samples_ para representar tipos de datos mas especializados. (Ej. _HKCDADocumentSample_, _HKWorkoutRoute_, _HKWorkout_) .

## [Leer Datos de HealthKit.](https://developer.apple.com/documentation/healthkit/reading_data_from_healthkit#overview)

Existen tres formas principales de accesar a los datos del almacen de Healthkit:
- Usando metodos. HealthKit store provee metodos especificos para accesar datos caracteristicos.
    * Leer datos caracteristicos de HealthKit [Tutorial.](https://www.devfright.com/reading-characteristic-data-from-healthkit/)

- Usando _Queries_. _Queries_ devuelven un _snapshot_ o _'pantallazo'_  de los datos requeridos del HealthKit store.
    * Usar _HKSampleQuery_ de HealthKit [Tutorial.](https://www.devfright.com/hksamplequery-tutorial-and-examples/)

- Long-running queries. Estos  _queries_ corren en el  _background_ de la aplicacion y actualizan la app cada vez que exista un cambio realizado en el HealthKit store.
    * Usar _Long-Running HKActivitySummaryQuery_ de HealthKit [Tutorial.](https://www.devfright.com/hkactivitysummaryquery-long-running-query/)

###  [Usar _Queries_ para solicitar _sample_ datos de HealthKit](https://developer.apple.com/documentation/healthkit/queries)

Los _Queries_ pueden ser usados para enlistar todas las fuentes de un tipo particular de dato, o realizar calculos estadisticos.
Por ejemplo, _queries_ estadisticos pueden calcular el ritmo cardiaco minimo y maximo por una semana, o el total de pasos realizados en un dia.
Para usar un _query_ se usa el metodo **execute(_:)**. Al llamar este metodo, un _snapshot_ de los datos actuales es devuelto asincronamente al _handler_ de resultados del _query_.

HealthKit provee diferentes tipos de _queries_, cada uno designado a devolver diferentes tipos de datos al almacen (HealthKit store):

- [Sample query](https://developer.apple.com/documentation/healthkit/hksamplequery)
- [Anchored object query.](https://developer.apple.com/documentation/healthkit/hkanchoredobjectquery)
- [Statistics query.](https://developer.apple.com/documentation/healthkit/hkstatisticsquery)
- [Statistics collection query](https://developer.apple.com/documentation/healthkit/hkstatisticscollectionquery)
- [Correlation query.](https://developer.apple.com/documentation/healthkit/hkcorrelationquery)
- [Source query](https://developer.apple.com/documentation/healthkit/hksourcequery)
- [Activity summary query](https://developer.apple.com/documentation/healthkit/hkactivitysummaryquery)
- [Document query.](https://developer.apple.com/documentation/healthkit/hkdocumentquery)
- [Observer query.](https://developer.apple.com/documentation/healthkit/hkobserverquery)


## Fuente
[Health & Fitness Videos for iOS developers](https://developer.apple.com/videos/frameworks/health-and-fitness)
