# Comentarios En Kotlin

En este tutorial te mostraremos las formas de escribir comentarios en Kotlin para agregar información a tu código que te permita expresar aspectos relacionados con documentación, intenciones, claridad, consecuencias, legalidad, etc.

---

## Comentarios De Una Sola Línea

Al igual que en Java y muchos otros lenguajes, el compilador de Kotlin interpreta comentarios de una sola línea y de múltiples líneas con un formato que inicia por barra (`/`).

Para realizar un comentario de una sola línea, usa barra doble (`//...`) y seguidamente escribes las palabras que proporcionen el contexto en el lugar del código:

```kotlin
fun main() {
    // Ejemplo de suma de dos números
    val sumOfTwoNumbers: Int // (1)

    val firstNumber = 1     // (2)
    val secondNumber = 5    // (3)

    sumOfTwoNumbers = firstNumber.plus(secondNumber) // (4)
    println("($firstNumber + $secondNumber) = $sumOfTwoNumbers") // (5)
}
```

El ejemplo anterior muestra un formato para comentar ejemplos que requieren ser explicados en detalle: agregar un comentario de línea al inicio para darle un título al objetivo del programa, y luego agregar comentarios en la misma línea de las sentencias para nombrar los pasos que se están dando.

Este formato permite dar contexto a las descripciones, con el fin de referirse al código por los números escritos.

> En IntelliJ IDEA los comentarios son diferenciados del código compilable con letra cursiva y color gris claro.

---

## Comentarios Multilínea

Si requieres insertar un comentario que contenga múltiples líneas, entonces abre con barra-asterisco, escribe *n* cantidad de líneas y cierra con asterisco-barra (`/* ... */`).

El compilador ignorará del código compilable todo lo que se encuentre entre estos dos:

```kotlin
/*
 * Copyright 2021 James Revelo. Todos los derechos reservados.
 * Ver Copyright.txt para más detalles de permisos
 */
package basics

fun main() {
    /* Código */
}
```

En el código anterior se ve cómo se usa un comentario con múltiples líneas para aplicar un ejemplo de copyright a un archivo Kotlin.

> Si se incluyen muchas líneas, IntelliJ IDEA te permite contraer dichos comentarios para mejorar la vista. Solo presionas uno de los dos botones de los extremos del comentario para colapsarlo.

---

## Atajos Para Comentar En IntelliJ IDEA

IntelliJ IDEA provee accesos directos para comentar y descomentar líneas:

- **Comentario de línea:** Ve a `Code | Comment with Line Comment` para comentar la línea donde se encuentre el cursor. Atajo de teclado: `Ctrl+/`
- **Comentario de bloque:** Selecciona la línea y dirígete a `Code | Comment with Block Comment`. Atajo de teclado: `Ctrl+Mayús+/`

---

## Comentarios TODO

Los comentarios TODO te permiten marcar partes de tu código con tareas que deseas realizar en un futuro.

Para añadirlos en IntelliJ IDEA, antepón la palabra `TODO` en un comentario de única línea y luego escribe la tarea a realizar:

```kotlin
fun main() {
    // TODO: Crear test unitario del controlador de "animales"
}
```

> Otra forma de añadirlo es tipear *todo* y seleccionar el constructor emergente que te ofrece el IDE.

Si deseas crear un comentario TODO con múltiples líneas, usa el patrón `FIXME` en el comentario:

```kotlin
fun main() {
    //FIXME Completar característica "listar animales":
    // - Crear controlador para lista de animales
    // - Crear comandos
    // - Crear repositorio de animales
}
```

Ambos tipos de TODOs pueden ser vistos y accedidos a través de la ventana de herramientas llamada **TODO**. Si la abres, verás la ubicación de todos los comentarios y podrás navegar hacia ellos para comenzar a completar sus instrucciones.

---

## Documentación Con KDoc

Kotlin posee un formato de documentación similar a Javadoc llamado **KDoc**. Este usa etiquetas de bloque denotadas con `@` para especificar diferentes aspectos de la entidad documentada, y Markdown para marcado en línea.

La forma de crear un comentario con KDoc es iniciándolo con `/**` y terminándolo con `*/`. Por ejemplo, la documentación para la cabecera de una clase:

```kotlin
/**
 * Representa a los animales del zoo
 *
 * @property name Nombre del animal
 * @property type Clasificación taxonomica del animal
 * @property age Edad en meses del animal
 *
 * @author James Revelo
 * @constructor Crea un nuevo animal
 */
class Animal(val name: String, val type: String, val age: Int)
```

Para generar el archivo de documentación a partir de KDoc, puedes usar la herramienta **Dokka**.
