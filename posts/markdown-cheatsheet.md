---
title: Markdown Cheat Sheet
category: annex
---

# Markdown Cheat Sheet


## Encabezados

```
# H1
## H2
### H3
#### H4
##### H5
###### H6
```

# Encabezado tipo H1
## Encabezado tipo  H2
### Encabezado tipo  H3
####  Encabezado tipo H4
#####  Encabezado tipo H5
######  Encabezado tipo H6

## Formato de texto

### Negritas
 ```
  **Este texto está en negritas**
  __Este texto está en negritas__
```
 **Este texto está en negritas**

### Cursiva

```
  *Este texto está en cursiva*
  _Este texto está en cursiva_
```
 _Este texto está en cursiva_


### Combinado

 ```
_Formato de **texto** combinado_
 ```

 _Formato de **texto** combinado_



## Listas
### Listas Ordenadas
```
1. Primer elemento
2. Segundo elemento
3. Tercer elemento
```
1. Primer elemento
2. Segundo elemento
3. Tercer elemento

### Listas Desordenadas
```
* Primer elemento
* Segundo elemento
* Tercer elemento

- Primer elemento
- Segundo elemento
- Tercer elemento
```

* Primer elemento
* Segundo elemento
* Tercer elemento

### Listas Combinadas

```
1. Primer elemento
  * Primer subelemento
  - Segundo subelemento
2. Segundo elemento
  1. Primer subelemento
  2. Segundo subelemento
3. Tercer elemento
```

1. Primer elemento
  * Primer subelemento
  - Segundo subelemento
2. Segundo elemento
  1. Primer subelemento
  2. Segundo subelemento
3. Tercer elemento

## Imágenes
```
![texto](imagen.jpg)

![Swift Logo](swift.jpg)

```

![Swift Logo](/assets/img/swift.jpg)


## Links
```
[título](link)

[Wiki](https://ioslabunam.github.io/wiki/)
```
[Wiki](https://ioslabunam.github.io/wiki/)

## Blockquotes
```
> Esto es un blockquote
```
> Esto es un blockquote

## Carácteres con escape
```
\(carácter de escape)

\* \` \+
```

Markdown provee escape para los siguentes carácteres:

| Símbolo | Símbolo | Símbolo |
| ----------- | ----------- |----------- |
| \\  | \` | \* |
| \_ | \{\} |  \[\] |
| \(\) | \# | \+ |
| \- | \. | \! |

## Listas de Tareas
 ```
- [x] Tarea 1
- [x] Tarea 2
- [ ] Tarea 3
- [x] Tarea 4
- [ ] Tarea 5
```
- [x] Tarea 1
- [x] Tarea 2
- [ ] Tarea 3
- [x] Tarea 4
- [ ] Tarea 5

## Bloques de Código
\```

print("hola mundo")

\```


``` swift
print("hola mundo")
```

## Tablas
```
| Encabezado Columna| Encabezado Colunma |
| ----------- | ----------- |
| Contenido Celda | Contenido Celda  |
| Contenido Celda  | Contenido Celda  |
```

| Encabezado columna| Encabezado Columna |
| ----------- | ----------- |
| Contenido Celda | Contenido Celda  |
| Contenido Celda  | Contenido Celda  |

## Emoji
```
:tada:
:+1:
:octocat:
:metal:
```
:tada: :+1: :octocat: :metal:
