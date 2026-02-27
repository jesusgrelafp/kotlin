# Lambdas Con Recibidor En Kotlin

Un **tipo función con recibidor** agrega a la sintaxis base un tipo recibidor, denotado por un punto antes de la lista de argumentos:

```kotlin
TipoRecibidor.(Arg1, Arg2, ..., ArgN) -> TipoRetorno
```

La función expresada por este tipo puede ser llamada desde un objeto del tipo del recibidor. Esta sintaxis es equivalente a la de las funciones de extensión.

---

## Ejemplo

Tipo función con recibidor para operar sobre `String`:

```kotlin
String.(Char) -> String
```

Representa una función que puede ser llamada desde un objeto `String`, recibe un `Char` y retorna un `String`.

---

## Lambda Con Recibidor

Crear una lambda a partir de un tipo función con recibidor permite acceder al recibidor dentro del cuerpo mediante `this`.

```kotlin
fun main() {
    val mapMessage: String.(Char) -> String = { it + this + it }
    println("Mensaje".mapMessage('*'))
}
// *Mensaje*
```

El objeto `"Mensaje"` actúa como recibidor (`this`) y el asterisco `'*'` se pasa como argumento (`it`).

---

## Intercambio de Sintaxis

Los tipos función con recibidor pueden interpretarse también en su forma sin punto (y viceversa). El compilador de Kotlin entiende el reemplazo del recibidor por un argumento adicional:

```kotlin
// Con recibidor
String.(Char) -> String

// Equivalente sin recibidor
(String, Char) -> String
```

Esto permite llamar a la misma lambda de dos formas:

```kotlin
println("Mensaje".mapMessage('*'))    // forma con recibidor
println(mapMessage("Mensaje", '*'))   // forma sin recibidor
```

---

## Uso en Funciones de Alcance

Las lambdas con recibidor son la base de las funciones de alcance de Kotlin como `run`, `with` y `apply`, que usan internamente tipos función con recibidor para dar acceso al objeto dentro del bloque sin necesidad de nombrarlo explícitamente.
