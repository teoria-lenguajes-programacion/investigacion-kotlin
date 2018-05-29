# Kotlin

<small>**Tecnológico de Costa Rica    
Escuela de Ingeniería en Computación  
Maestría en Computación  
MC-8812 Teoría de los Lenguajes de Programación**</small>  

<small>Carlos Martín Flores González</small>     

<small>Sábado 2 de Junio, 2018</small>

---

## Agenda

- Introducción 
- Características del Lenguaje
- Ejemplos/Demo
- Conclusiones
---

## Kotlin

- Concebido en el 2010 por [JetBrains](https://www.jetbrains.com)
- Escrito para la _Java Virtual Machine_
- _Open Source_
- Para propósito general, _Client-Side_ (Kotlin JS), Android, Nativo, _scripting_
- Versión `1.0` lanzada en 2016

---
## Historia
JetBrains buscaba una alternativa para Java.  
Se buscaba:
- Tipos estáticos
- Compatibilidad con el código Java
- Productivo
- Fácil para leer y razonar

---

#### Mi primer programa en Kotlin

```kotlin

data class Person(val name: String, 
                  val age: Int? = null)

fun main (args: Array<String>){
  val persons = listOf(Person("Alice"), 
                       Person("Bob", age = 29))
  
  val oldest  = persons.maxBy { it.age ? : 0}
  println("The oldest is: $oldest")
}
// The oldest is: Person(name=Bob, age=29)
```

---

## Características del Lenguaje

---

### Valores y Tipos de Datos Base
- Números: `Double, Float, Short, Long, Byte`
- Booleanos: `Boolean`. Dos tipos: `true, false`
- _Arrays_: `Array`
- _Strings_: `String`. Son inmutables, indexables (`s[i]`), iterables 

---
##### _String Literals_
```kotlin
val msg = "Hello World"
val multi = """
  This is a multi line
  text. Awesome!
"""
```

##### _String Templates_
```kotlin
val i = 10
print("i = $i")
// imprime "i = 10"
```

---
### Variables y Almacenamiento
Para declarar una variable:  
`nombre + tipo (opcional)`

```kotlin
val question = "how old are you?"
val answer: Int = 42
// Si la variable no se inicializa se necesita el tipo
```
Palabras reservadas para declarar una variable:
1. `val`: inmutable (final)
2. `var`: mutable, puede cambiar
---

### Estructuración de datos

---

### Declaraciones, alcance de identificadores 

---

### Estructuras de Control

---

### Secuenciadores

---

### Mecanismos de modularización

---

### Soporte a concurrencia, paralelismo, distribución

---

### Sistemas de Tipos

---

### Genericidad

---
### Soporte a Paradigmas

---
### Soporte a "Programación en grande"

---
## Análisis y Conclusiones

---

## Ejemplos/Demo

---

## Tips!

<br>

@fa[arrows gp-tip](Press F to go Fullscreen)

@fa[microphone gp-tip](Press S for Speaker Notes)

---

## Template Features

- Code Presenting |
- Repo Source, Static Blocks, GIST |
- Custom CSS Styling |
- Slideshow Background Image |
- Slide-specific Background Images |
- Custom Logo, TOC, and Footnotes |

---?code=sample/go/server.go&lang=golang&title=Golang File

@[1,3-6](Present code found within any repo source file.)
@[8-18](Without ever leaving your slideshow.)
@[19-28](Using GitPitch code-presenting with (optional) annotations.)

---

@title[JavaScript Block]

<p><span class="slide-title">JavaScript Block</span></p>

```javascript
// Include http module.
var http = require("http");

// Create the server. Function passed as parameter
// is called on every request made.
http.createServer(function (request, response) {
  // Attach listener on end event.  This event is
  // called when client sent, awaiting response.
  request.on("end", function () {
    // Write headers to the response.
    // HTTP 200 status, Content-Type text/plain.
    response.writeHead(200, {
      'Content-Type': 'text/plain'
    });
    // Send data and end response.
    response.end('Hello HTTP!');
  });

// Listen on the 8080 port.
}).listen(8080);
```

@[1,2](You can present code inlined within your slide markdown too.)
@[9-17](Displayed using code-syntax highlighting just like your IDE.)
@[19-20](Again, all of this without ever leaving your slideshow.)

---?gist=onetapbeyond/494e0fecaf0d6a2aa2acadfb8eb9d6e8&lang=scala&title=Scala GIST

@[23](You can even present code found within any GitHub GIST.)
@[41-53](GIST source code is beautifully rendered on any slide.)
@[57-62](And code-presenting works seamlessly for GIST too, both online and offline.)

---

## Template Help

- [Code Presenting](https://github.com/gitpitch/gitpitch/wiki/Code-Presenting)
  + [Repo Source](https://github.com/gitpitch/gitpitch/wiki/Code-Delimiter-Slides), [Static Blocks](https://github.com/gitpitch/gitpitch/wiki/Code-Slides), [GIST](https://github.com/gitpitch/gitpitch/wiki/GIST-Slides) 
- [Custom CSS Styling](https://github.com/gitpitch/gitpitch/wiki/Slideshow-Custom-CSS)
- [Slideshow Background Image](https://github.com/gitpitch/gitpitch/wiki/Background-Setting)
- [Slide-specific Background Images](https://github.com/gitpitch/gitpitch/wiki/Image-Slides#background)
- [Custom Logo](https://github.com/gitpitch/gitpitch/wiki/Logo-Setting), [TOC](https://github.com/gitpitch/gitpitch/wiki/Table-of-Contents), and [Footnotes](https://github.com/gitpitch/gitpitch/wiki/Footnote-Setting)

---

## Go GitPitch Pro!

<br>
<div class="left">
    <i class="fa fa-user-secret fa-5x" aria-hidden="true"> </i><br>
    <a href="https://gitpitch.com/pro-features" class="pro-link">
    More details here.</a>
</div>
<div class="right">
    <ul>
        <li>Private Repos</li>
        <li>Private URLs</li>
        <li>Password-Protection</li>
        <li>Image Opacity</li>
        <li>SVG Image Support</li>
    </ul>
</div>

---

### Questions?

<br>

@fa[twitter gp-contact](@gitpitch)

@fa[github gp-contact](gitpitch)

@fa[medium gp-contact](@gitpitch)

---?image=assets/image/gitpitch-audience.jpg

@title[Download this Template!]

### <span class="white">Get your presentation started!</span>
### [Download this template @fa[external-link gp-download]](https://gitpitch.com/template/download/blue)

