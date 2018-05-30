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
- Escrito para la _Java Virtual Machine_(JVM)
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

### Mi primer programa en Kotlin

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

Se delega el manejo del almacenamiento a la JVM

---

### Declaraciones, alcance de identificadores
- **Declaración de tipos:** nuevos tipos son introducidos a través de `Data Classes, Enum Classes`, interfaces, clases y objetos.
- **Alcance de identificadores:** no se introduce ningún cambio en el manejo del alcance de los identificadores en comparación con Java. Los identificadores "viven" dentro del ámbito en el que fueron declaradas.

---

```kotlin
// Declaración de una clase
class Invoice { 
}
// Clase con constructor primario
class User(_nickname: String){
  val nickname = _nickname;
}
val invoice = Invoice()
val user = User("Luigi");

// Data Classes: propósito principal es contener datos
data class User(val name: String, val age: Int)
val admin = User("John", 40)

// Enum Classes
enum class Color{
  RED, ORANGE, YELLOW, GREEN, BLUE, PINK
}
val primaryColor = Color.GREEN

// Interfaces: similares a las de Java8
interface Clickable {
  fun click()
}
class Button : Clickable {
  override fun click() = println("I was clicked")
}
val submitBtn = Clickable = Button()
submitBtn.click()

// Interfaz con implementaciones
interface Focusable {
  fun setFocus(b: Boolean) =
    println("I ${if (b) "got" else "lost"} focus")

  fun showOf() = println("I'm focusable")  
}

/* object: declaración e instanciación combinada 
de una clase */
object Payroll {
    val allEmployees = arrayListOf<Person>()
    
    fun calculateSalary() {
        for (person in allEmployees) {
            ...
        }
    }
}
Payroll.allEmployees.add(Person(...)
Payroll.calculateSalary()

/*
Companion objects: utilizados como factory methods y 
miembros estáticos. Las clases en Kotlin no pueden 
tener miembros estáticos.
*/
class A {
    companion object {
        fun bar() {
            println("Companion object called")
        }
    }
}

A.bar()
//Companion object called

/* object puede ser usado para declarar objetos anónimos.
Los objetos anónimos reemplazan el uso de clases anónimas 
internas en Java. */
window.addMouseListener{
  object: MouseAdapter(){
    override fun mouseClicked(e: MouseEvent){
      ...
    }
    override fun mouseEntered(e: MouseEvent){
      ...
    }
  }
}

/* Declaración de funciones*/
fun max(a: Int, b: Int): Int {
  return if (a > b) a else b
} 

/* Single Expression Functions*/
fun double(x: Int): Int = x * 2

/* "Procedimientos" - funciones que retornan Unit. 
Si una función no retorna ningún valor útil, su 
tipo de retorno es Unit. Unit es un tipo con solo 
un valor: Unit */
fun printHello(name: String?): Unit {
  if(name != null)
    println("Hello ${name}")
  else
    println("Hi There!")
    // "return Unit" o "return" es opcional
}
```

@[1-9](Declaración de una Clase)
@[11-13](Data Classes)
@[15-19](Enum Classes)
@[21-29](Interfaces)
@[31-37](Interfaz con implementación)
@[39-51](object: declaración e instanciación combinada de una clase)
@[53-68](companion object)
@[69-82](object expression)
@[83-87](Declaración de función)
@[88-90](Single-Expression functions)
@[91-102](Procedimientos)

---

### Estructuras de Control
```kotlin
// If-else
var max : Int
if (a > b){
  max = a
} else {
  max = b
}

// If como expresión
var max = if(a > b) a else b

/* Expresion when: reemplaza al operador switch de
lenguajes basados en C */
when(x){
  1          -> print("x == 1")
  2          -> print("x == 2")
  3,4        -> print("x == 3 or x == 4")
  in 5..10   -> print("x is between 5 and 10")
  !in 20..30 -> print("x is out of range")
  else -> {
    print("none of the above")
  }
}

// Ciclos for: forma equivalente al for-each de Java
for(item: Int in ints){
  print(item)
}

// Se puede iterar sobre un rango de numeros
for(i in 1..3){
  println(i)
}

for(i in 6 downTo 0 step 2){
  println(i)
}

/* Ciclos while: tanto el while como el do-while
trabajan de la misma forma que en Java
*/
while(x > 0){
  x--
}

do{
  val y = retrieveData()
} while (y != null) // "y" es visible aqui
```
@[1-10](If-Else)
@[12-24](When)
@[25-37](Ciclo For)
@[39-48](Ciclo While, Do-While)

---

### Secuenciadores
- `return`: retorna de la función más reciente
- `break`: termina un ciclo
- `continue`: continua con la siguiente iteración de un ciclo
- Excepciones: todas descienden de `Throwable`. Tiene un mensaje, _stack trace_ y una causa (opcional)
- Para lanzar una excepción se usa `throw`

---
#### Secuenciadores (continuación)
```kotlin
// break y continue con etiquetas
loop@ for(in in 1..100){
  for(j in 1..100){
    if(...) break@loop
  }
}

// Lanzar una excepción
throw MyException("Houston we have problem!")

// Atrapar una excepción
try{
  // algún código
} catch (e: SomeException){
  /* código que maneja la excepción.
  Pueden haber uno o varios bloques catch
  */
} finally {
  /* bloque finalizador opcional, de ser
  incluido, se ejecutará siempre. */
}
```
@[1-7](break y continue con etiquetas)
@[8,9](Lanzar excepción)
@[10-21](Captura de Excepciones)
---

### Mecanismos de modularización
**Paquetes**. Cada archivo Kotlin puede tener una declaración de `package` al inicio y todas las demás declaraciones definidas en el archivo serán colocados bajo ese paquete.  

Las declaraciones definidas en otros archivos puede ser usados directamente si están en el mismo paquete sino, hay que importarlas.

---

```kotlin
// {Proyecto}/geometry/shapes.kt
package geometry.shapes

import java.util.Random

class Rectangle(val height: Int, val width: Int){
  val isSquare: Boolean
    get() = height == width
}

fun createRandomRectangle(): Rectangle{
  val random = Random()
  return Rectangle(random.nextInt(), random.nextInt())
}

// Otro archivo
package geometry.example

import geometry.shapes.createRandomRectangle

fun main(args: Array<String>){
  println(createRandomRectangle().isSquare())
}

```

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

