# SwiftUI
&nbsp;

![SWIFTUI](https://i.udemycdn.com/course/240x135/2397342_68bf_2.jpg)

&nbsp;

### Primeros pasos

&nbsp;

1. Abre un playground en Xcode puedes nombrarlo "PruebaSwiftUI"
2. Antes de empezar con los ejemplos de codigo debemos de importar algunas librerias que nos permitiran trabajar con la vista previa y con el framework de **SwiftUI** estas librerias son: 
`SwiftUI ` y `PlaygraundSupport `, acompañadas siempre de la palabra reservada `import` no lo olvides.
3. El proyecto por defecto de **SwiftUI** nos entrega 2 estructuras cuyo codigo es el siguiente:

&nbsp;

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
&nbsp;

Como puedes observar tenemos la primera estructura cuyo nombre es **ContentView** que se va a conformar al protocolo `View` y la segunda estructura llamada **ContentView_Preview** se va a conformar a `PreviewProvider`, la razon de ser de estas estructuras es muy sencilla, en la primera vamos a crear una vista y el contenido de dicha vista, en este caso solamente tenemos un texto con la palabra *Hello World* dentro de nuestra funcion `Text()`; la segunda estructura declara un *preview* donde vamos a mostrar la vista que anteriormente creamos, por lo tanto en el cuerpo de la estructura **ContentView_Preview** tenemos que poner el nombre de la estructura donde se encuentra nuestra vista, en este caso `ContentView()`.

&nbsp;

4. Como verás aunque ya codificamos un poco aun nuestra vista no nos muestra nada, para poder ver en el live view del playground nuestro codigo  es necesario añadir una linea más que es la razon por la cual importamos la libreria de playground, esta linea es la siguiente:
`PlaygroundPage.current.setLiveView(ContentView())`.
5. Ahora que ya completamos los pasos anteriores solamente ejecuta el codigo del playground y el live preview te mostrara una pantalla con el fondo blanco pero con nuestro *Hello World* en el centro de ella.

&nbsp;

### Modificadores

&nbsp;

**SwiftUI** nos ofrece "modificadores" para poder customizar nuestra vista como mejor se acomode acorde a las necesidades del proyecto. Algunos de los modificadores basicos son:
```
font()
background()
clipShape
padding()
foregroundColor()
```

Estos "modificadores" los podremos aplicar usando el operador "." antes de cada sentencia, es decir si quieres cambiar el color de un texto tu sintaxis debera ser `.foregroundColor(.pink)` con esto nos damos cuenta que la palabra `UIColor()` que se usaba en los storyboards ya no es necesaria en **SwiftUI**.

Una cosa más que debes saber es que los "Modificadores" deben de ir en el cuerpo de la estructura del **ContentView** un ejemplo es el siguiente:

&nbsp;

```swift
struct ContentView: View {
    var body: some View {
        Text("Hello World")
        .bold()
        .italic()
        .foregroundColor(.pink)
        .font(.title)
    }
}

struct ContentView_Preview: PreviewProvider {
    static var previews: some View {
        ContentView()
    }
}
```
Te aconsejo probar el codigo para que puedas ver el cambio en el **canvas**.

&nbsp;

### Layout Views

&nbsp;

En **SwiftUI** como ya te diste cuenta es muy facil agregar y modificar un elemento, pero aqui viene un poco la complejidad de este framework, dentro del cuerpo de la estructura solo se puede agregar un elemento, es decir hasta ahora solo teniamos el `Text("Hello World")` en la estructura del **ContentView** pero si intentamos agregar otro elemento Xcode no lo permitirá ya que solo se puede albergar un elemento dentro del body, es ahi donde surge la interrogante ¿Como puedo agregar mas elementos a mi vista?. Bueno esto se hace  atravez de contenedores, llamados  **VStack** el cual va a actuar como un elemento dentro del body con lo cual cumplimos con la regla de solo tener un elemento dentro de la estructura. 
Para ejemplificar veamos su codigo.

&nbsp;

```swift
struct ContentView: View {
    var body: some View {
        VStack{
            Text("Hola Mundo")
        }
    }
}
```
&nbsp;

Hasta ahora lo unico que emos agregado es el **VStack** y dentro de el la funcion `Text()` pero nuestro *canvas* no cambiara en nada, ahora viene lo interesante, agrega otra funcion  `Text()` dentro del **VStack** y ve lo que pasa.

Si lo has intentado te habrás dado cuenta que agrega el texto de tu nueva funcion `Text()` justo de bajo de la que teniamos antes, bueno esto se debe a que nuestro **VStack** actua como un solo contenedor que va a contener a los stack de tus funciones `Text()` haciendose pasar por un solo contenedor ante Xcode, pero ¿Por que los añade de bajo?, bueno aqui va la explicacion:

Hay tres tipos de **Stack** basicos :
* VStack (vertical Stack)
* HStack (horizontal Stack)
* ZStack (Stack de profundidad)

&nbsp;

VStack| HStack | ZStack
---|---|---
Agrega elementos de forma vertical uno arriba de otro en el orden en que sean declarados. | Agrega elementos de forma horizontal uno al lado de otro en el orden en que sean declarados. | Este es el mas complejo de entender de los 3 pero la definicion sería que tenemos un stack que agrega elementos de forma uno sobre de otro en el orden en que sean declarados.

&nbsp;

Ahora que ya  sabemos los elementos de los Stacks debemos saber que los stack tambien tienen "modificadores", un ejemplo de ellos es el siguiente:

```swift
VStack(alignment: .leading, spacing: 30){
    Text("Hola Mundo como estas el dia de hoy")
    Text("Hola Mundo2")

}
```

&nbsp;

Con el codigo anterior verás como los elementos del Stack se alinean a la izquierda 
y puedes probar a alinear tus elementos hacia la derecha cambiando la propiedad a `.trailing` dentro del aligment del Stack.

&nbsp;

#### Enlazar contenedores

Con lo visto hasta ahora probablemente piensas que **SwiftUI** es muy simple, pero ahota agregaremos otro grado de complejidad, Ya vimos que con **VStack** podemos añadir elementos verticales uno arriba de otro, pero ¿Que pasa si quiero un elemento horizontal dentro del VStack sin perder los elementos verticales que ya tengo?

Buena pregunta, como antes lo dije, no podemos agregar dos Stacks dentro del Body por lo que debe de haber otra manera, y estas en lo correcto. Para agregar elementos de diferente forma dentro de un Stack lo que hacemos es anidar Stacks, de esta manera tendremos un codigo como el Siguiente:


```swift
VStack(alignment: .leading, spacing: 30){
    Text("Hola Mundo como estas el dia de hoy")
    Text("Hola Mundo2")

    HStack(alignment: .center, spacing:10){
        Text("Hola Mundo")
        Text("Hola Mundo2")
    }
}
```
&nbsp;

Con este cambio aplicado a nuestro proyecto nos daremos cuenta que ahora en el *canvas* tenemos nuestros primeros dos `Text()` de forma vertical y debajo de ellos los `Text()` que tenemos dentro del **HStack** alineados de forma horizontal.

&nbsp;

### Agregar Elementos

&nbsp;

Ya hemos aprendido la mayoria de la teoria básica que nos trae este framework como minimo para poder usarlo. Ahora solo enlistare algunas funciones que agregaran elementos a nuestros **Stack**.

* Nota: Una consideración importante es que SwiftUI solo permite 10 elementos dentro de cada Stack para evitar problemas de rendimiento, aunque si tu quieres poner 10 Stack dentro de un solo Stack la capacidad de elementos será de 100, aunque puede que tu aplicación se vea afectada en cuanto a rendimiento y posiblemente en su logica, entonces es  recomendable usar solo aquellos elementos que sean importantes o sin los que tu App no pueda vivir. 

&nbsp;



- `Spacer()` - expande o da espacio entre un elemento y otro en el orden de su **Stack**
- `HStack(){ }.padding(.all)` - Genera espacio entre los elementos con cierto margen de separación apegado al espacio de neustra vista
- `Text()` - Equivalente al Label en SB
- `Image("imagen")` - Añade una imagen al canvas
- `Button(){}` - Boton simple, dentro debe tener elementos para hacerlo funcional

&nbsp;

### Estados en SwiftUI

#### State

¿Que es el State?

Los **State** funcionan para poder verificar los estados de variables o de elementos de nuestro proyecto y poder cambiarlos en tiempo real despues de la interacción de un usuario con dicho elemento, para ello habrá que usar siempre `@State` antes de nuestra declaracion de la variable , la nomenclatura para esto es la siguiente: `@State <private> var nombre = "Pedro"` el private es opcional pero se recomienda que se añada por razones que veremos mas adelante.

#### Tipos de State

En SwiftUI podemos tener 3 tipos de State los cuales se usan dependiendo de la cantidad de vistas en las que dicha variable se va a usar. Los tipos son los siguientes:

`@State` - Variable que se va a usar en una vista, se recomienda que se use la palabra reservada `private`despues de la sentencia para reafirmar que nuestra variable se usara solo en la vista en la que se esta declarando.

`@ObservedObject` - Se usa como prefijo de las variables que serán usadas por dos vistas como maximo.

`@EnviromentObject` - Se usa como prefijo de las variables que serán usadas en todo el proyecto.


Con esto terminamos la introducción a SwiftUI, las explicaciones aquí vistas servirán solo como referencia, se recomienda revisar el tutorial de SwiftUI en apple.developer.com para interactual con los elementos de una mejor manera.

Al tiempo de esta redacción para la wiki de IOSLab SwiftUI lleva 9 meses de "vida" por lo que la sintaxis o elementos, así como funcionalidades o protocolos pueden llegar a cambiar.

> "SwiftUI será el futuro de las tecnologias moviles" 