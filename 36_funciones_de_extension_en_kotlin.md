# Funciones De Extensión En Kotlin

Una **función de extensión** es una función que extiende las funcionalidades de una clase con la introducción de un parámetro llamado *parámetro recibidor*, sin necesidad de modificar la clase original.

---

## Declarar Funciones de Extensión

El tipo recibidor se declara antes del nombre de la función, separado por un punto:

```
TipoRecibidor.nombre()
```

Dentro del cuerpo, se puede usar `this` para referirse al objeto recibidor.

### Ejemplo básico

Convertir un `Boolean` a las palabras "SI" o "NO":

```kotlin
fun Boolean.adverb() = if (this) "SI" else "NO"

fun main() {
    val a = 4
    val b = 3
    val res = (a > b).adverb()
    print("¿$a es mayor que $b?: $res")
}
// ¿4 es mayor que 3?: SI
```

---

## Ejemplo con Clases Propias

Clases de dominio:

```kotlin
class Student(val name: String, val age: Int)
class Course(val students: List<Student>)
```

Funciones de extensión para consultas sin mezclar lógica en las entidades:

```kotlin
fun Course.olderStudentAge(): Int {
    return students.maxOf { it.age }
}

fun Course.studentsWithInitial(initial: Char): Int {
    return students.filter { it.name[0] == initial }.size
}
```

Uso:

```kotlin
fun main() {
    val course = Course(listOf(
        Student("María", 17),
        Student("Rupertina", 25),
        Student("Ricardina", 18)
    ))
    println("La mayor tiene ${course.olderStudentAge()}")
    println("Estudiantes cuyo nombre empieza con R: ${course.studentsWithInitial('R')}")
}
// Estudiante mayor: 25
// Estudiantes cuyo nombre empieza con R: 2
```

> Nota: dentro de la función de extensión, `students` puede usarse directamente sin `this` ya que el compilador lo infiere del contexto del recibidor.

---

## Sintaxis de Expresión Única

Las funciones de extensión admiten sintaxis compacta:

```kotlin
fun Course.olderStudentAge() = students.maxOf { it.age }

fun Course.studentsWithInitial(initial: Char) =
    students.filter { it.name[0] == initial }.size
```
