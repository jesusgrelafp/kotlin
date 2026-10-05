# Ultimate Kotlin Cheatsheet

*Posted on Mar 29, 2025 by Dev Cookies*    

---

## Table of Contents
- [Basics](#basics)
- [Variables & Data Types](#variables--data-types)
- [Control Flow](#control-flow)
- [Functions](#functions)
- [Collections](#collections)
- [Classes & Objects](#classes--objects)
- [Null Safety](#null-safety)
- [Coroutines](#coroutines)
- [Extension Functions](#extension-functions)
- [Functional Programming](#functional-programming)
- [Learning Resources](#learning-resources)

---

## Basics

### Hello World
```kotlin
fun main() {
    println("Hello, World!")
}
```

### Comments
```kotlin
// Single-line comment

/* Multi-line 
   comment */

/**
 * KDoc comment
 * @param args command line arguments
 */
```

---

## Variables & Data Types

### Variable Declaration
```kotlin
val immutable: String = "Cannot be changed" // Read-only (immutable)
var mutable: String = "Can be changed" // Mutable
mutable = "New value"

// Type inference
val inferred = "Type is inferred as String"
```

### Basic Types
```kotlin
// Numbers
val byte: Byte = 127 // 8 bits
val short: Short = 32767 // 16 bits
val int: Int = 2147483647 // 32 bits
val long: Long = 9223372036854775807L // 64 bits
val float: Float = 3.14f // 32 bits
val double: Double = 3.14159 // 64 bits

// Characters and strings
val char: Char = 'A'
val string: String = "Hello"
val multiline: String = """
    This is a multiline string
    No escaping needed
"""

// Boolean
val boolean: Boolean = true

// Type conversion
val longFromInt: Long = int.toLong()
```

### String Templates
```kotlin
val name = "Kotlin"
println("Hello, $name!") // Simple variable
println("Array size: ${array.size}") // Expression
```

---

## Control Flow

### Conditionals
```kotlin
// If expression (returns a value)
val max = if (a > b) a else b

// If statement
if (x > 0) {
    println("Positive")
} else if (x < 0) {
    println("Negative")
} else {
    println("Zero")
}

// When expression (enhanced switch)
when (x) {
    1 -> println("One")
    2, 3 -> println("Two or Three")
    in 4..10 -> println("Between 4 and 10")
    !in 20..30 -> println("Not between 20 and 30")
    is String -> println("Is a String of length ${x.length}")
    else -> println("Otherwise")
}

// When as an expression
val result = when (x) {
    0, 1 -> "Binary digit"
    else -> "Not a binary digit"
}
```

### Loops
```kotlin
// For loop with range
for (i in 1..5) {
    println(i) // 1, 2, 3, 4, 5
}

// For loop with step
for (i in 1..10 step 2) {
    println(i) // 1, 3, 5, 7, 9
}

// For loop downward
for (i in 5 downTo 1) {
    println(i) // 5, 4, 3, 2, 1
}

// For loop with indices
for (i in array.indices) {
    println(array[i])
}

// For loop with index
for ((index, value) in array.withIndex()) {
    println("Element at $index is $value")
}

// While loop
while (condition) {
    // code
}

// Do-while loop
do {
    // code
} while (condition)
```

### Loop Control
```kotlin
// Break
for (i in 1..10) {
    if (i == 5) break
    println(i) // 1, 2, 3, 4
}

// Continue
for (i in 1..10) {
    if (i % 2 == 0) continue
    println(i) // 1, 3, 5, 7, 9
}

// Labeled break/continue
outer@ for (i in 1..10) {
    for (j in 1..10) {
        if (i * j > 50) break@outer
    }
}
```

---

## Functions

### Basic Function
```kotlin
fun greet(name: String): String {
    return "Hello, $name!"
}

// Single-expression function
fun greet(name: String): String = "Hello, $name!"

// Type inference for return value
fun greet(name: String) = "Hello, $name!"
```

### Parameters
```kotlin
// Default parameters
fun greet(name: String, greeting: String = "Hello") = "$greeting, $name!"

// Named arguments
greet(greeting = "Hi", name = "Kotlin")

// Variable number of arguments (varargs)
fun sum(vararg numbers: Int): Int {
    return numbers.sum()
}
sum(1, 2, 3, 4) // 10

// Spread operator for varargs
val numbers = intArrayOf(1, 2, 3)
sum(*numbers)
```

### Local Functions
```kotlin
fun outer() {
    fun inner() {
        // Has access to outer's scope
    }
    inner()
}
```

### Infix Functions
```kotlin
infix fun Int.plus(other: Int): Int = this + other
val result = 1 plus 2 // Same as 1.plus(2)
```

### Operator Overloading
```kotlin
operator fun Point.plus(other: Point): Point {
    return Point(x + other.x, y + other.y)
}
val result = point1 + point2 // Calls point1.plus(point2)
```

### Higher-Order Functions
```kotlin
// Function that takes a function as parameter
fun operation(x: Int, y: Int, op: (Int, Int) -> Int): Int {
    return op(x, y)
}

// Calling with lambda
operation(1, 2) { a, b -> a + b }

// Function that returns a function
fun multiplier(factor: Int): (Int) -> Int {
    return { it * factor }
}
val double = multiplier(2)
double(5) // 10
```

---

## Collections

### Creating Collections
```kotlin
// Immutable collections (preferred)
val list = listOf(1, 2, 3) // List<Int>
val set = setOf("apple", "banana") // Set<String>
val map = mapOf("a" to 1, "b" to 2) // Map<String, Int>

// Mutable collections
val mutableList = mutableListOf(1, 2, 3)
val mutableSet = mutableSetOf("apple", "banana")
val mutableMap = mutableMapOf("a" to 1, "b" to 2)

// Empty collections
val emptyList = emptyList<String>()
val emptySet = emptySet<Int>()
val emptyMap = emptyMap<String, Int>()

// Array
val array = arrayOf(1, 2, 3)
val intArray = intArrayOf(1, 2, 3) // Primitive int[]
```

### Collection Operations
```kotlin
// Element access
list[0] // First element
list.first() // First element
list.last() // Last element
map["a"] // Value for key "a"

// Adding elements (mutable collections)
mutableList.add(4)
mutableSet.add("cherry")
mutableMap["c"] = 3

// Removing elements (mutable collections)
mutableList.remove(2)
mutableSet.remove("apple")
mutableMap.remove("a")

// Collection transformations
val doubled = list.map { it * 2 } // [2, 4, 6]
val even = list.filter { it % 2 == 0 } // [2]
val sum = list.reduce { acc, i -> acc + i } // 6
val grouped = list.groupBy { it % 2 } // {1=[1, 3], 0=[2]}
val flattened = listOf(listOf(1), listOf(2, 3)).flatten() // [1, 2, 3]

// Checking elements
list.contains(2) // true
2 in list // true
list.any { it > 2 } // true
list.all { it < 10 } // true
list.none { it < 0 } // true
list.count { it % 2 == 0 } // 1

// Collection information
list.size // 3
list.isEmpty() // false
list.isNotEmpty() // true

// Finding elements
list.find { it > 2 } // 3
list.findLast { it < 3 } // 2
list.indexOf(2) // 1

// Sorting
list.sorted() // Natural order
list.sortedDescending() // Reverse natural order
list.sortedBy { it % 2 } // Custom order
```

---

## Classes & Objects

### Class Declaration
```kotlin
class Person {
    var name: String = ""
    var age: Int = 0

    fun introduce() {
        println("I'm $name, $age years old")
    }
}

// Instantiation
val person = Person()
person.name = "John"
person.age = 25
person.introduce()
```

### Constructors
```kotlin
// Primary constructor
class Person(val name: String, var age: Int) {
    // Init blocks run in sequence with property initializers
    init {
        require(age >= 0) { "Age cannot be negative" }
    }
}

// Secondary constructor
class Person {
    val name: String
    var age: Int

    constructor(name: String, age: Int) {
        this.name = name
        this.age = age
    }

    constructor(name: String) : this(name, 0)
}
```

### Properties
```kotlin
class Person {
    // Backing field auto-generated
    var name: String = ""
        get() = field.uppercase()
        set(value) {
            field = value.trim()
        }

    // Custom getter (read-only property)
    val isAdult: Boolean
        get() = age >= 18

    // Late-initialized property (no initial value needed)
    lateinit var job: String

    // Lazy property - initialized on first access
    val socialSecurityNumber: String by lazy {
        calculateSSN() // Expensive operation
    }
}
```

### Data Classes
```kotlin
// Automatically implements equals(), hashCode(), toString(), copy()
data class User(val name: String, val age: Int)

val user1 = User("John", 25)
val user2 = user1.copy(age = 26)
val (name, age) = user1 // Destructuring declaration
```

### Inheritance
```kotlin
// All classes are final by default
open class Animal(val name: String) {
    open fun makeSound() {
        println("Some sound")
    }
}

class Dog(name: String) : Animal(name) {
    override fun makeSound() {
        println("Woof!")
    }
}
```

### Abstract Classes
```kotlin
abstract class Shape {
    abstract val area: Double
    abstract fun draw()

    // Non-abstract function
    fun display() {
        println("Displaying shape with area: $area")
    }
}

class Circle(val radius: Double) : Shape() {
    override val area: Double
        get() = Math.PI * radius * radius

    override fun draw() {
        println("Drawing a circle")
    }
}
```

### Interfaces
```kotlin
interface Clickable {
    // Abstract property
    val clickCount: Int

    // Abstract method
    fun onClick()

    // Method with default implementation
    fun showOff() {
        println("I'm clickable!")
    }
}

interface Focusable {
    fun showOff() {
        println("I'm focusable!")
    }
}

// Multiple interface implementation
class Button : Clickable, Focusable {
    override val clickCount: Int = 0

    override fun onClick() {
        println("Button clicked")
    }

    // Must override conflicting method
    override fun showOff() {
        super<Clickable>.showOff()
        super<Focusable>.showOff()
    }
}
```

### Singleton (Object)
```kotlin
object Singleton {
    val property = "I'm a singleton"
    fun method() = "Only one instance exists"
}

// Usage
Singleton.property
Singleton.method()
```

### Companion Object
```kotlin
class MyClass {
    companion object Factory {
        fun create(): MyClass = MyClass()
    }
}

// Usage (like static methods in Java)
val instance = MyClass.create()
```

### Enum Classes
```kotlin
enum class Direction {
    NORTH, EAST, SOUTH, WEST
}

// Enum with properties and methods
enum class Color(val rgb: Int) {
    RED(0xFF0000),
    GREEN(0x00FF00),
    BLUE(0x0000FF);

    fun containsRed(): Boolean = (rgb and 0xFF0000 != 0)
}
```

### Sealed Classes
```kotlin
// Restricted class hierarchy
sealed class Result {
    class Success(val data: Any) : Result()
    class Error(val message: String) : Result()
    object Loading : Result()
}

// Ideal for use with when
fun handleResult(result: Result) = when (result) {
    is Result.Success -> println("Success: ${result.data}")
    is Result.Error -> println("Error: ${result.message}")
    is Result.Loading -> println("Loading...")
    // No else branch needed as all subclasses are covered
}
```

### Type Aliases
```kotlin
typealias ClickHandler = (Button, ClickEvent) -> Unit
typealias StringMap = Map<String, String>
```

---

## Null Safety

### Nullable Types
```kotlin
// Non-nullable type
var nonNull: String = "value"
// nonNull = null // Compilation error

// Nullable type
var nullable: String? = "value"
nullable = null // OK
```

### Safe Calls
```kotlin
// Returns null if user is null
val length = user?.name?.length

// Chain of safe calls
val city = user?.address?.city

// Safe call with let
user?.let { println("User name is ${it.name}") }
```

### Elvis Operator
```kotlin
// Default value if null
val length = str?.length ?: 0

// Throw exception if null
val name = user?.name ?: throw IllegalArgumentException("User must have a name")
```

### Not-null Assertion
```kotlin
// Throws NullPointerException if null
val length = str!!.length
```

### Safe Casts
```kotlin
// Returns null if cast fails
val str: String? = value as? String
```

### Platform Types
```kotlin
// Types coming from Java are treated as platform types (neither nullable nor non-null)
import java.util.Date

fun getDate(): Date = Date() // Java method

val date: Date = getDate() // Treated as non-nullable
val nullableDate: Date? = getDate() // Treated as nullable
```

---

## Coroutines

### Basic Coroutine
```kotlin
import kotlinx.coroutines.*

fun main() = runBlocking {
    launch {
        delay(1000)
        println("World!")
    }
    println("Hello,")
}
// Prints: Hello, (waits 1 second) World!
```

### Coroutine Builders
```kotlin
// launch - fire and forget
launch {
    // Coroutine code
}

// async - returns a result
val deferred = async {
    // Coroutine code that returns a value
    "Result"
}
val result = deferred.await()

// runBlocking - bridges blocking and non-blocking worlds
runBlocking {
    // Coroutine code
}

// coroutineScope - creates a new scope and waits for all children
coroutineScope {
    launch { delay(1000) }
    launch { delay(2000) }
}
// Waits for both launches to complete
```

### Coroutine Context & Dispatchers
```kotlin
// Dispatchers
launch(Dispatchers.Default) { /* CPU-intensive work */ }
launch(Dispatchers.IO) { /* I/O operations */ }
launch(Dispatchers.Main) { /* UI updates */ }

// Named coroutines for debugging
launch(CoroutineName("my-coroutine")) { /* ... */ }

// Combined context
launch(Dispatchers.IO + CoroutineName("io-work")) { /* ... */ }

// Job for cancellation control
val job = launch { /* ... */ }
job.cancel()
job.join() // Wait for completion
```

### Exception Handling
```kotlin
val handler = CoroutineExceptionHandler { _, exception ->
    println("Caught $exception")
}

val job = GlobalScope.launch(handler) {
    throw RuntimeException("Oops")
}

// supervisorScope for independent failure of children
supervisorScope {
    val job1 = launch { /* may fail */ }
    val job2 = launch { /* continues even if job1 fails */ }
}
```

### Flow
```kotlin
// Creating a flow
val flow = flow {
    for (i in 1..3) {
        delay(100)
        emit(i)
    }
}

// Collecting a flow
flow.collect { value ->
    println(value)
}

// Flow operators
flow.map { it * 2 }
    .filter { it > 0 }
    .take(2)
    .collect { println(it) }
```

---

## Extension Functions

### Basic Extension Function
```kotlin
// Add a method to String class
fun String.addExclamation(): String {
    return this + "!"
}

// Usage
val excited = "Hello".addExclamation() // "Hello!"
```

### Extension Properties
```kotlin
val String.lastChar: Char
    get() = this[length - 1]

// Usage
val last = "Kotlin".lastChar // 'n'
```

### Nullable Receiver
```kotlin
fun String?.isNullOrBlank(): Boolean {
    return this == null || this.isBlank()
}

// Usage
val result = null.isNullOrBlank() // true
```

### Companion Object Extensions
```kotlin
class MyClass {
    companion object {}
}

fun MyClass.Companion.create(): MyClass = MyClass()

// Usage
val instance = MyClass.create()
```

---

## Functional Programming

### Lambda Expressions
```kotlin
// Full syntax
val sum = { a: Int, b: Int -> a + b }

// Type inference
val multiply: (Int, Int) -> Int = { a, b -> a * b }

// Calling a lambda
sum(1, 2) // 3

// Lambda with receiver
val greet: String.() -> String = { "Hello, $this!" }
"Kotlin".greet() // "Hello, Kotlin!"
```

### Function References
```kotlin
// Reference to a function
fun isOdd(x: Int) = x % 2 != 0
val numbers = listOf(1, 2, 3)
numbers.filter(::isOdd) // [1, 3]

// Reference to a constructor
class Person(val name: String)
val createPerson = ::Person
val person = createPerson("John")

// Reference to an instance method
val predicate = String::isNotEmpty
```

### Higher-Order Functions
```kotlin
// Standard library examples
val numbers = listOf(1, 2, 3, 4)

numbers.filter { it % 2 == 0 } // [2, 4]
numbers.map { it * it } // [1, 4, 9, 16]
numbers.forEach { println(it) } // Prints each number
numbers.fold(0) { acc, n -> acc + n } // 10
```

### Sequences
```kotlin
// Lazy evaluation (more efficient for chained operations)
val result = sequenceOf(1, 2, 3, 4)
    .filter { println("Filter: $it"); it % 2 == 0 }
    .map { println("Map: $it"); it * it }
    .first() // Only processes elements until first result

// Generate sequences
val fibonacci = sequence {
    var a = 0
    var b = 1
    while (true) {
        yield(a)
        val next = a + b
        a = b
        b = next
    }
}
fibonacci.take(5).toList() // [0, 1, 1, 2, 3]
```

### Scope Functions
```kotlin
// let - object as it, returns lambda result
val length = str?.let {
    println("Processing '$it'")
    it.length
}

// run - object as this, returns lambda result
val upperCase = str.run {
    println("Processing '$this'")
    uppercase()
}

// with - object as this, returns lambda result (extension-like)
val result = with(str) {
    println("Processing '$this'")
    length * 2
}

// apply - object as this, returns the object (builder-like)
val person = Person().apply {
    name = "John"
    age = 30
}

// also - object as it, returns the object (side effects)
val numbers = mutableListOf(1, 2, 3)
    .also { println("List: $it") }
    .also { it.add(4) }
```

---

## Learning Resources

### Official Resources
- Kotlin Official Website
- Kotlin Documentation
- Kotlin Koans - Interactive coding exercises
- Kotlin Blog

### Books
- *"Kotlin in Action"* by Dmitry Jemerov and Svetlana Isakova
- *"Atomic Kotlin"* by Bruce Eckel and Svetlana Isakova
- *"Programming Kotlin"* by Venkat Subramaniam
- *"Head First Kotlin"* by Dawn Griffiths and David Griffiths

### Online Courses
- Kotlin for Java Developers - Coursera
- Kotlin Bootcamp for Programmers - Google
- Kotlin for Android Developers - Udacity

### Community
- Kotlin Discuss - Official forum
- Kotlin Slack - Official Slack
- Reddit Kotlin - Reddit community

### Frameworks and Libraries
- **Ktor** - Web framework
- **Exposed** - SQL library
- **Kotest** - Testing framework
- **Koin** - Dependency injection
- **Arrow** - Functional programming
- **kotlinx.coroutines** - Coroutines library
- **Compose Multiplatform** - UI framework
