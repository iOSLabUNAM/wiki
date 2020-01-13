# SwiftUI
![SWIFTUI](https://i.udemycdn.com/course/240x135/2397342_68bf_2.jpg)

### Primeros pasos


1. Abre un playground en Xcode puedes nombrarlo "PruebaSwiftUI"
2. Antes de empezar con los ejemplos de codigo debemos de importar algunas librerias que nos permitiran trabajar con la vista previa y con el framework de **SwiftUI** estas librerias son: 
`SwiftUI ` y `PlaygraundSupport `, acompañadas siempre de la palabra reservada `import` no lo olvides.
3. El proyecto por defecto de **SwiftUI** nos entrega 2 estructuras cuyo codigo es el siguiente:
``` swift
struct ContentView: View {
    var body: some View {
        Text("Hello World")
    }
}

struct ContentView_Preview: PreviewProvider {
    static var previews: some View {
        ContentView()
    }
}
```
Como puedes observar tenemos la primera estructura cuyo nombre es **ContentView** que se va a conformar al protocolo `View` y la segunda estructura llamada **ContentView_Preview** se va a conformar a `PreviewProvider`, la razon de ser de estas estructuras es muy sencilla, en la primera vamos a crear una vista y el contenido de dicha vista, en este caso solamente tenemos un texto con la palabra *Hello World* dentro de nuestra funcion `Text()`; la segunda estructura declara un *preview* donde vamos a mostrar la vista que anteriormente creamos, por lo tanto en el cuerpo de la estructura **ContentView_Preview** tenemos que poner el nombre de la estructura donde se encuentra nuestra vista, en este caso `ContentView()`.
4. Como verás aunque ya codificamos un poco aun nuestra vista no nos muestra nada, para poder ver en el live view del playground nuestro codigo  es necesario añadir una linea más que es la razon por la cual importamos la libreria de playground, esta linea es la siguiente:
`PlaygroundPage.current.setLiveView(ContentView())`.
5. Ahora que ya completamos los pasos anteriores solamente ejecuta el codigo del playground y el live preview te mostrara una pantalla con el fondo blanco pero con nuestro *Hello World* en el centro de ella.



**Principios** *Basicos* de esta ***Tecnologia***

asi se escribe la palabra reservada `func () {}`

```swift
let a: String = "¿Como estas?"
```
> SwiftUI será el futuro de las tecnologias moviles 


