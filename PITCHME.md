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
} // Implícitamente hereda de Any
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
// Un archivo
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
En Kotlin se pueden utilizar todas las librerías `Futures`, `CompletableFutures`, _Reactive Extensions_ para concurrencia, paralelismo y programación asincrónica en general que son utilizadas en Java.

---
###### Soporte a concurrencia, paralelismo, distribución (Cont.)

**Corutinas**: A partir de la versión 1.1 de Kotlin se introdujo el concepto de Corutina que proporciona una forma de evitar bloquear un hilo y reemplazarlo con una operación más económica y de mayor control: la suspensión de una corutina.  

[KotlinConf 2017 - Corutinas](https://www.youtube.com/watch?v=_hfBv0a09Jc&t=1233s)

---

###### Soporte a concurrencia, paralelismo, distribución (Cont.)
_Everything like in blocking code_
```kotlin
/* 
Suspendiendo funciones: esto sucede cuando se 
llama a una función marcada con la palabra
reservada "suspend"
*/
suspend fun doSomething(foo: Foo) : Bar {
  ...
}

// 1.
suspend fun requestToken(): Token{
  // makes request for a token & suspend
  return token // returns result when received
}

// 2.
suspend fun createPost(tokenL token, item: Item) : Post {
  //sends item to server & suspend
  return post // return result when received
}

fun processPost(post: Post){ ... }

suspend fun postItem(item: Item){
  val token = requestToken() // suspension point
  val post  = createPost(token, item) // suspension point
  processPost(post)
}

// Se puede utilizar en ciclos
for((token, item) in list) {
  createPost(token, item)
}

// Se puede manejar excepciones
try {
  createPost(token, item)
} catch(e: BadTokenException){
  ...
}

// Junto con funciones
file.readLines().forEach { line ->
  createPost(token, line.toItem())
}
```

@[1-8](Suspendiendo funciones)
@[10-28](Ejemplo)
@[30-45](Usos)
---

### Sistemas de Tipos
```kotlin
/* 
Modificadores de accesso para clases:
- final: No puede ser sobreescrita(por defecto)
- open: Puede ser sobreescrita
- abstract: Debe ser sobreescrita
- override: sobreescribe un miembro de una 
super clase o interfaz

Modificadores de visibilidad
- public: (por defecto). Visible en todas partes
- internal: Visible en un modulo
- protected: Visible en subclases
- private: Visible en una clase
*/

// Herencia: todas las clases heredan de Any
open class Base(p: Int) {...}

class Derived(p: Int): Base(p) {...}

// Sobreescritura de métodos
open class Base{
  open fun v(){ ... }
  fun nv(){ ... }
}
class Derived(): Base() {
  override fun v(){ 
    // sobreescritura
  }
}

/* Extensiones: similar a C#, Kotlin proporciona 
la habilidad de extender una clase con nueva 
funcionalidad sin tener que heredar de la clase o 
usar algún tipo de patrón de diseño como el 
patrón decorador
*/
fun MutableList<Int>.swap(index1: Int, index2: Int) {
    val tmp = this[index1] //"this" corresponde a la lista
    this[index1] = this[index2]
    this[index2] = tmp
}
val l = mutableListOf(1, 2, 3)
l.swap(0,2) 
```
@[2-7](Modificadores de accesso para clases)
@[9-13](Modificadores de visibilidad)
@[15-19](Herencia)
@[21-30](Sobreescritura de métodos)
@[31-44](Extensiones)
---

### Genericidad
```kotlin
/*
Tal y como en Java, las clases y funciones en 
Kotlin pueden tener tipos parametrizados
*/
class Box<T>(t: T){
  var value = t
}
val box = Box<Int> = Box<Int>(1)
val box: Box(1)
// 1 es un Int, así que se puede inferir el tipo

/* 
Star projections: Existen situaciones en donde 
no se tiene conocimiento del tipo específico del 
tipo del valor. Supóngase que solamente se desea 
imprimir todos los elementos de un arreglo y que 
no importa el tipo de los elemento en ese arreglo. 
*/
fun printArray(array: Array<*>) {
    array.forEach { println(it) }
}
// Uso
val array = arrayOf(1, 2, 3)
printArray(array)

/*
Funciones genericas: Los tipos parametrizados se 
colocan antes del nombre de la función
fun <T> List<T>.slice(indices: IntRange): List<T>
*/
val letters = ('a'..'z').toList()
println(letters.slice<Char>(0..2))
// [a, b, b]
println(letters.slice(10..13))
// [k, l, m, n]
```
@[1-10](Clases parametrizadas)
@[12-24](Star projections)
@[26-35](Funciones parametrizadas)

---
### Soporte a Paradigmas
Los dos grandes paradigmas soportados son: programación orientada a objetos y programación funcional. Las funciones pueden ser almacenadas en variables, estructuras de datos, pasadas como argumentos y retornadas des otra función de orden superior.  

Kotlin también puede ser utilizado como lenguaje de _scripting_. 

---
```kotlin
// Lambda
strings.filter { it.length == 5 }
       .sortedBy { it }
       .map { it.toUpperCase() }

/* Closures: una expresion lambda o una funcion
anonima puede acceder a su closure */
var sum = 0
ints.filter { it > 0 }.forEach {
    sum += it
}
print(sum)
```
```bash
# Scripting
$ kotlinc // Inicia el REPL
$ kotlinc -script sample.kts // Ejecuta un script de Kotlin 
```
---
### Soporte a "Programación en grande"
- Backend: _Spring Framework_, Vert.x, Ktor
- Android: Soporte oficial
- Client-side: KotlinJS, traspilar código Kotlin a JavaScript
- Kotlin/Native: compilar Kotlin a binarios nativos sin necesidad de una VM.

---
### Análisis y Conclusiones

- La interoperatibilidad con Java y la versatibilidad de Kotlin lo convierte en una alternativa para muchos programadores
- Agrupa muchas de las ideas de otros lenguajes populares
- Se puede programar desde sistemas embebidos y hasta aplicaciones móviles

---

## ¡Muchas Gracias!