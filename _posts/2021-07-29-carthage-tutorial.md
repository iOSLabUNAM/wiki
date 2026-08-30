---
title: Tutorial de Carthage
category: dependencies
layout: post
---

# Tutorial de Carthage

Una de las mejores cosas del desarrollo de iOS es la amplia gama de bibliotecas
de terceros disponibles para su uso. Con tantas bibliotecas disponibles, 
administrar las dependencias puede resultar complicado. Ahí es donde entran 
los administradores de dependencias.

![carthage](https://miro.medium.com/max/860/1*Xv_W2QYW2zTO0pYSEIpX3w.jpeg)

[Carthage](https://github.com/Carthage/Carthage) es un administrador de dependencias 
simple para macOS y iOS, creado por un grupo de desarrolladores de GitHub.

Carthage no solo fue el primer administrador de dependencias en trabajar con Swift, 
sino que también está escrito en Swift. Utiliza exclusivamente frameworks dinámicos, 
en lugar de bibliotecas estáticas.

En este tutorial de Carthage, se podrá:
- Descubrir por qué y cuándo utilizar un administrador de dependencias 
y qué diferencia a Carthage de otras herramientas.

- Instalar Carthage.

- Declarar dependencias, instalándolas e integrándolas dentro de un proyecto.

- Actualizar sus dependencias a diferentes versiones.


## Ventajas de la gestión de dependencias

Los gerentes de dependencia realizan algunas funciones útiles, que incluyen:

- Simplificar y estandarizar el proceso de obtención de código de terceros e 
incorporarlo a su proyecto. Sin esta herramienta, haría esto copiando manualmente 
los archivos de código fuente, colocando binarios precompilados o utilizando un 
mecanismo como los submódulos de Git.

- Facilitar la actualización de bibliotecas de terceros en el futuro. Imagina 
tener que visitar la página de GitHub de cada dependencia, descargar la fuente 
y colocarla en tu proyecto cada vez que hay una actualización. ¿Por qué te harías 
eso a ti mismo?

- Seleccionar versiones apropiadas y compatibles de cada dependencia que use. Por ejemplo, 
agregar dependencias manualmente puede resultar complicado cuando dependen unas de otras 
o comparten otra dependencia.

![dependencies](https://koenig-media.raywenderlich.com/uploads/2020/01/02-Dependency-Management.png)

La mayoría de los administradores de dependencias construyen un grafo de dependencias 
de las dependencias del proyecto y sus subdependencias, luego determinan la mejor 
versión de cada una para usarla.

## Comparando con otros Gestores de Dependencia

Uno de los administradores de dependencias más populares es [CocoaPods](https://cocoapods.org), 
que agiliza la integración de bibliotecas en su proyecto. Es muy utilizado en la comunidad de iOS.

Apple ofrece su propio administrador de dependencias llamado [Swift Package Manager](https://swift.org/package-manager/)
para compartir y distribuir paquetes en Swift 3.0 y superior.

Si bien CocoaPods y Swift Package Manager son excelentes herramientas, Carthage ofrece
una alternativa más sencilla y práctica. Entonces, ¿cuál es el adecuado para el proyecto?

### Carthage contra CocoaPods
¿En qué se diferencia Carthage de CocoaPods y por qué usaría algo además del 
administrador de dependencias más popular para iOS?

Si bien CocoaPods es fácil de usar, no es *simple*. La filosofía detrás de 
Carthage es que un administrador de dependencias debe ser *simple*.

CocoaPods agrega complejidad al desarrollo de la aplicación y los procesos 
de distribución de la biblioteca:

- Las bibliotecas deben crear, actualizar y alojar archivos Podspec. Los 
desarrolladores de aplicaciones deben escribir las suyas propias si no existe 
ninguna para una biblioteca que deseen utilizar.

- Al agregar pods a un proyecto, CocoaPods crea un nuevo proyecto de Xcode 
con un target para cada pod individual, además de un espacio de trabajo para 
contenerlos. Se tiene que usar el espacio de trabajo y confiar en que el 
proyecto CocoaPods funciona. También debe mantener esas configuraciones de 
compilación adicional.

- CocoaPods usa un repositorio de Podspecs centralizado. Esto puede desaparecer 
o volverse inaccesible, causando problemas.

Carthage tiene como objetivo proporcionar una herramienta **más simple** que 
sea más flexible y más fácil de entender y mantener.

Así es como Carthage logra esto:

- No cambia tu proyecto de Xcode ni te obliga a usar un espacio de trabajo.

- No necesita Podspecs ni un repositorio centralizado donde los autores de la 
biblioteca envíen sus pods. Si puede construir su proyecto como un framwork, 
puede usarlo con Carthage, que aprovecha la información existente directamente 
de Git y Xcode.

- Carthage no hace nada por arte de magia; siempre se tiene el control. 
Agrega dependencias al proyecto Xcode y Carthage las recupera y crea.

### Carthage contra Swift Package Manager

¿Qué hay de las diferencias entre Carthage y Swift Package Manager?

El enfoque principal de Swift Package Manager es compartir código Swift de una 
manera amigable para los desarrolladores. El enfoque de Carthage es compartir 
framweorks dinámicos. Los framworks dinámicos son un superconjunto de paquetes Swift.

Un paquete es una colección de código fuente de Swift más un archivo de manifiesto. 
El archivo de manifiesto define el nombre del paquete y su contenido. Un paquete 
contiene código Swift, código Objective-C, activos sin código como imágenes o cualquier 
combinación de los tres.

SPM tiene mucho a su favor, especialmente porque Xcode 11 tiene soporte incorporado 
para paquetes SPM. Sin embargo, SPM tiene un par de limitaciones que impiden que muchas 
bibliotecas lo admitan. Por ejemplo, no admite compartir binarios ya construidos, 
solo el código fuente de sus paquetes. Si desea tener una biblioteca de código cerrado, 
no puede usar SPM. Además, SPM admite la adición de código fuente a los framworks, 
pero no recursos como imágenes u otros archivos de datos.

Esto significa que muchas bibliotecas que podría utilizar no recibirán soporte SPM 
en el corto plazo. Por ahora, todavía tendrá que confiar en Carthage o CocoaPods 
para esas bibliotecas.

## Instalación de Carthage

En el núcleo de Carthage hay una herramienta de línea de comandos que ayuda a buscar 
y construir dependencias.

Hay mútiples formas de instalar Carthage:

- **Instalador**: descargue y ejecute el archivo *Carthage.pkg* para la última 
versión, luego siga las instrucciones en pantalla. Si está instalando el paquete 
a través de CLI, es posible que primero deba ejecutar 
`sudo chown -R $ (whoami)/usr/local`.

- **Homebrew**: Puede usar Homebrew e instalar la herramienta Carthage en su
sistema simplemente ejecutando `brew update` y `brew install carthage`. 
(nota: si instaló previamente la versión binaria de Carthage, debe eliminar 
/Library/Frameworks/CarthageKit.framework).

- **MacPorts**: puede usar MacPorts e instalar la herramienta carthage en su
sistema  simplemente ejecutando sudo port selfupdate y sudo port install carthage. 
(nota: si instaló previamente la versión binaria de Carthage, debe eliminar 
/Library/Frameworks/CarthageKit.framework).

- **Desde la fuente**: si desea ejecutar la última versión de desarrollo (que puede 
ser muy inestable o incompatible), simplemente clone la rama maestra del 
repositorio y luego ejecute make install. Requiere Xcode 10.0 (Swift 4.2).

¡Y está listo! Para comprobar que Carthage se instaló correctamente, abra 
Terminal y ejecute el siguiente comando:

```bash
carthage version
```

Esto le muestra la versión de Carthage que instaló.
A continuación, debe indicarle a Carthage qué bibliotecas instalar 
utilizando un Cartfile.

## Creando el archivo Cartfile

Un Cartfile es un archivo de texto simple que describe las dependencias 
de su proyecto con Carthage, por lo que puede determinar qué instalar. Cada línea 
en un Cartfile indica dónde buscar una dependencia, el nombre de la dependencia 
y, opcionalmente, qué versión usar. Un Cartfile es el equivalente a un 
CocoaPods Podfile.

Para crear el primero, vaya a Terminal, luego navegue hasta el directorio 
raíz de su proyecto, el directorio que contiene su archivo **.xcodeproj**, 
usando el comando cd:

```bash
cd ~/Path/To/Starter/Project
```

Crear un Cartfile vacío con el coamndo `touch`:

```bash
touch Cartfile
```

Agregue las siguientes líneas al Cartfile y guárdelo:

```swift
github "Alamofire/Alamofire" ~> "5.4"
```

Esta línea le dice a Carthage que su proyecto requiere Alamofire versión 5.4.

## El formato Cartfile

Escribe Cartfiles en un subconjunto de **OGDL**: Ordered Graph Data Language. 
Suena elegante, pero es bastante simple. Hay dos piezas clave de información 
en cada línea de un Cartfile:

- **Origen de la dependencia**: esto le dice a Carthage dónde buscar una 
dependencia. Carthage tiene dos tipos de orígenes:

  - **github** para proyectos alojados en GitHub. Especifica un proyecto de 
  GitHub en el formato de nombre de usuario / nombre de proyecto,
  como con el Cartfile anterior.

  - **git** para repositorios Git genéricos alojados en otro lugar. Se usa la 
  palabra clave git seguida de la ruta al repositorio git, ya sea una URL 
  remota usando `git://`, `http://` o `ssh://` o una ruta local a un 
  repositorio Git en tu máquina de desarrollo.

- **Versión de dependencia**: aquí, le indica a Carthage qué versión de una 
dependencia desea utilizar. Hay varias opciones a tu disposición, 
dependiendo de qué tan específico se quiera ser:

  - **== 1.0**: indica "Usar exactamente la versión 1.0".
  - **>= 1.0**: Significa "Use la versión 1.0 o superior".
  - **~> 1.0**: se traduce como "Use cualquier versión que sea compatible con 1.0", 
  es decir, cualquier versión hasta la próxima versión principal.
 - **Nombre de rama/nombre de etiqueta/nombre de commit** significa 
 "Usar esta rama / etiqueta / commit de git específico". Por ejemplo, puede 
 especificar master o un hash de confirmación como 5c8a74a.

Carthage utiliza [versiones semánticas](https://semver.org) para determinar 
la compatibilidad.

Si no especifica una versión, Carthage utilizará la última versión que sea 
compatible con sus otras dependencias.

## Construyendo las Dependecias

Ahora que tiene un Cartfile, es hora de ponerlo en uso e instalar algunas dependencias.

Cierre su Cartfile en Xcode y regrese a la Terminal. Ejecute el siguiente comando:

```bash
carthage update --platform iOS --use-xcframeworks
```

Esto le indica a Carthage que clone los repositorios de Git del Cartfile y luego cree 
cada dependencia en un framwork. Verá un resultado que muestra los resultados, como este:

```bash
*** Cloning Alamofire
*** Checking out Alamofire at "5.4"
*** xcodebuild output can be found in /var/folders/bj/3hftn5nn0qlfrs2tqrydgjc80000gn/T/carthage-xcodebuild.7MbtQO.log
*** Building scheme "Alamofire iOS" in Alamofire.xcworkspace
````

`--platform iOS` garantiza que Carthage solo cree frameworks para iOS. Si no 
especifica una plataforma, Carthage creará marcos para todas las plataformas, 
a menudo tanto Mac como iOS, compatibles con la biblioteca.

Si desea ver más opciones, ejecute `carthage help update`.

De forma predeterminada, Carthage realiza sus compras y crea un nuevo 
directorio llamado Carthage, que encontrará en la misma ubicación que su Cartfile.

## Construcción de artefactos

Cuando usa CocoaPods, realiza varios cambios en su proyecto de Xcode y vincula 
el resultado, junto con un proyecto de Pods especial, en un espacio de trabajo de Xcode.

Carthage es un poco diferente. Verifica el código para sus dependencias y construye 
el resultado en frameworks binarios. Luego, depende de usted integrar los marcos 
en su proyecto.

Parece un trabajo extra, pero es beneficioso. Solo se necesitan unos pocos pasos 
y, como resultado, eres más consciente de los cambios en tu proyecto.

Cuando se ejecuta la actualización de Carthage, Carthage crea un par de archivos 
y directorios.

- **Cartfile.resolved**: este archivo sirve como complemento del Cartfile. Define
exactamente qué versiones de sus dependencias Carthage seleccionó para su instalación. 
Se recomienda encarecidamente enviar este archivo a su repositorio de control de 
versiones. Su presencia asegura que otros desarrolladores puedan comenzar rápidamente
usando exactamente las mismas versiones de dependencia.

- **Directorio de Carthage**, que contiene dos subdirectorios:
  - **Build**: contiene el framework construido para cada dependencia. Se puede 
  integrar en los proyectos. Carthage crea cada framework a partir de la fuente
  o lo descarga de la página de lanzamientos del proyecto en GitHub.
  - **Checkouts**: aquí es donde Carthage comprueba el código fuente de cada 
  dependencia que está lista para integrarse en los marcos. Carthage mantiene 
  su propia caché interna de repositorios de dependencia, por lo que no tiene 
  que clonar la misma fuente varias veces para diferentes proyectos.

## Agregar frameworks al proyecto

De vuelta en Xcode, haga clic en el proyecto en el navegador de proyectos. 
Seleccione el target del proyecto. Elija en la pestaña **General** en la parte 
superior y luego desplácese hasta la sección **Frameworks, Libraries, and 
Embedded Content** en la parte inferior.

En la ventana de Carthage en el Finder, navegue hasta **Build**. Arrastre todos
los frameworks instalados en la sección **Linked Frameworks and Libraries** en
Xcode.

Esto le dice a Xcode que vincule su aplicación a estos frameworks, lo que le 
permite hacer uso de ellos en su código.

A continuación, cambie a **Build Phases**. Haga clic en el icono + en la parte 
superior izquierda del editor y seleccione **New Run Script Phase**. 

Agregue el siguiente comando al bloque de código en Ejecutar script:

```bash
/usr/local/bin/carthage copy-frameworks
```

Estrictamente hablando, esta fase de compilación no es necesaria para que su 
proyecto se ejecute. Sin embargo, es una solución ingeniosa para un error de 
envío de la App Store en el que las aplicaciones con frameworks que contienen 
imágenes binarias para el simulador de iOS se rechazan automáticamente.

El comando `carthage copy-frameworks` elimina estas arquitecturas adicionales.

Compile y ejecute para asegurarse de que todo funcione como se esperaba.
Cuando se inicie la aplicación, verá el controlador de la vista de búsqueda.

# Referencias

[1] Laso-Marsetti, F. (2020, 18 marzo). Carthage Tutorial: Getting Started. 
Raywenderlich.Com. https://www.raywenderlich.com/7649117-carthage-tutorial-getting-started

[2] https://github.com/Carthage/Carthage