# AVKIT

AVKIT es un framework de alto nivel para construir interfaces multimedia para reproducción audio y video.

Para reproducir archivos de audio y video Apple creó el framework AVFoundation, el cual contiene una gran cantidad de clases y elementos que provee controles de bajo nivel sobre los cuales iOS reproduce audio y video. Dicho framework no solo esta disponible en iOS, sino en todo el ecosistema Apple, como OSx. Con AVFoundation se pueden construir y personalizar reproductores de audio a un nivel muy específico.

Por otra parte Apple ha creado AVKIT, un framework de alto nivel para construir interfaces multimedia para reproducción audio y video de una forma más sencilla y de fácil integración con iOS. AVKit es un framework que utiliza y se soporta sobre  AVFoundation, y que permite una abstracción mas sencilla de las funcionalidades de AVFoundation.

En resumen, si se desea crear una interfaz  con funcionalidades más complejas y personalizables, se puede utilizar AVFoundation, sin embargo si se desea crear reproductores multimedia estándar y simples, AVKit es la solución ideal.

[![Foo](https://developer.apple.com/library/archive/documentation/AudioVideo/Conceptual/MediaPlaybackGuide/Contents/Resources/en.lproj/Art/media_playback_framework_2x.png)](https://developer.apple.com/library/archive/documentation/AudioVideo/Conceptual/MediaPlaybackGuide/Contents/Resources/en.lproj/Art/media_playback_framework_2x.png)

## Integración básica de AVKit para reproducir video

Para crear un reproductor simple de video debemos primero crear un AVPlayerViewController esta clase que hereda de UIViewController nos proporciona un “wrapper” que contiene varios componentes de AVFoundation y proporciona controles básicos de reproducción de videos.

AVPlayerViewController es altamente configurable por lo que puedes elegir que elementos del reproductor se deberán mostrar, si deseas cono ver la lista completa de opciones de configuración puedes consultarlos en la página: https://developer.apple.com/documentation/avkit/avplayerviewcontroller

Para importar el framework lo primero que tenemos que hacer es agregar la siguiente línea a nuestro ViewController sobre el cual deseamos impolementar AVKit

```swift
import AVKit
```
posteriormente creamos una variable con la instancia del AVPlayerViewController de la siguiente forma:

```swift
let videoPlayerController = AVPlayerViewController()
```

Ya que AVPlayerViewController es una subclase de UIViewController se debe agregar como un hijo de nuestro view controller sobre el cual estamos implementando AVKIT, supongamos que nuestro ViewController se llama VideoViewController, entonces deberíamos integrarlo de la siguiente forma:

```swift
addChild(videoPlayerController)
videoPlayerController.didMove(toParent: self)
view.addSubview(videoPlayerController.view)
let videoPlayerController = videoPlayerController.view!
```

El código anterior agrega el reproductor de video a nuestro view controller	 como un hijo de la vista padre, cuando tu agregas un view controller como hijo de otro view controller, siempre deberás llamar el método didMove(toParent: ) sobre el controller hijo para asegurarse de que sabe que ha sido agregado como hijo de otro view controller. Posteriormente de agregar el reproductor como hijo del view controller, el reproductor es agregado como una subview del controller en el que queremos integrar el reproductor. Posteriormente si se desea, se pueden configurar algunos constraints para posicionarlo en un sector de la vista.

Así de sencillo podemos integrar nuestro reproductor de video en una vista de view controller, el ultimo paso que restaría sería obtener una referencia al video que deseamos reproducir y asignarlo al reproductor, lo cual podemos realizar de la siguiente forma:

```swift
let url = Bundle.main.url(forResource: “videito”, withExtension: “mp4”)!
videoPlayerController.player = AVPlayer(url: url)
```

El Código anterior busca un video en los recursos llamado “videito.mp4” y obtiene una url del archivo. Posteriormente crea una instancia de AVPlayer el cual apunta al archivo de video y es asignado a la instancia del reproductor de video. La instancia de AVPlayerViewController usa la instancia de AVPlayer para reproducir el video y maneja el control del mismo de forma interna.

Esta es la forma más básica de integrar videos con AVKIt en una aplicación de iOS y sirve de punto de partida para realizar integraciones más avanzadas.

[![Foo](https://i.stack.imgur.com/erb6e.jpg)](https://i.stack.imgur.com/erb6e.jpg)


Fuentes:
  - https://developer.apple.com/documentation/avkit/avplayerviewcontroller
  - Complete iOS 12 Development Guide: Become a professional iOS developer by mastering Swift, Xcode 10, ARKit, and Core ML, Craig Clayton, Donny Wals, 1st Edition., 2019.
  - https://stackoverflow.com/questions/25932570/how-to-play-video-with-avplayerviewcontroller-avkit-in-swift
