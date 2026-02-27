# Desestructuración En Kotlin

En este tutorial se aprende el uso de la desestructuración en Kotlin para desempacar un valor compuesto en múltiples variables a través de las funciones de componentes (`componentN()`).

---

## Declaraciones De Desestructuración

Kotlin permite crear **múltiples variables a la vez** a partir de un valor compuesto. Esta sintaxis se llama **declaración de desestructuración**:

```kotlin
fun main() {
    val account = "Paypal" to 50.4
    val (name, balance) = account
    println("Cuenta: $name")
    println("Saldo: $balance")
}
```

---

## Funciones De Componentes

La desestructuración funciona gracias a las funciones `componentN()`. Internamente, el compilador las invoca para declarar e inicializar las variables:

```kotlin
fun main() {
    val account = "Paypal" to 50.4
    val name = account.component1()
    val balance = account.component2()
}
```

La posición de la variable corresponde al índice `N` de `componentN()`.

---

## Sintaxis De Guion Bajo Para Variables Sin Usar

Si no se necesita algún valor de la desestructuración, se usa `_` para omitirlo (el compilador no llamará a esa función de componente):

```kotlin
fun main() {
    val center = Triple(2, 0, 4)
    val (_, y, _) = center
    println(y) // 0
}
```

---

## Desestructuración En Bucles `for`

Se puede desestructurar la variable de iteración en un bucle `for`. La función `withIndex()` retorna un iterable de `IndexedValue` con funciones de componentes para el índice y el valor:

```kotlin
fun main() {
    val numbers = intArrayOf(1, 5, 4, 3, 0, 7)
    for ((index, number) in numbers.withIndex()) {
        if ((index + 1) % 2 == 0)
            println(number)
    }
}
```

---

## Desestructuración En Clases De Datos

Las `data class` generan automáticamente funciones `componentN()` por sus propiedades del constructor, lo que habilita su desestructuración directamente:

```kotlin
data class Troll(val health: Int, val speed: Double)

fun main() {
    val (health, speed) = Troll(150, 0.5)
    println("El troll tiene $health puntos de vida y se mueve a $speed")
}
```

### Desestructuración en clases normales (sin `data`)

Se pueden añadir funciones de operador con la convención `componentN()` para habilitar la desestructuración en cualquier clase:

```kotlin
class Troll(val health: Int, val speed: Double) {
    operator fun component1() = health
    operator fun component2() = speed
}

fun main() {
    val (health, speed) = Troll(150, 0.5)
    println("El troll tiene $health puntos de vida y se mueve a $speed")
}
```

---

## Desestructuración En Mapas

La librería estándar de Kotlin añade extensiones `component1()` y `component2()` a `Map.Entry`, lo que permite desestructurar las entradas de un mapa en un bucle `for`:

```kotlin
fun main() {
    val shampoosAndTreatmentTypes = mapOf(
        "Buticaba" to "Liso",
        "Pinorelo" to "Crespo",
        "Curucuru" to "Ondulado",
        "Mertabé" to "Caspa"
    )
    for ((shampoo, treatment) in shampoosAndTreatmentTypes) {
        println("El shampoo $shampoo es para el tratamiento $treatment")
    }
}
```

---

## Desestructuración En Lambdas

Los parámetros de una lambda también admiten desestructuración, permitiendo usar las variables directamente en el cuerpo:

```kotlin
fun main() {
    val shampoosAndTreatmentTypes = mapOf(
        "Buticaba" to "Liso",
        "Pinorelo" to "Crespo",
        "Curucuru" to "Ondulado",
        "Mertabé" to "Caspa"
    )
    shampoosAndTreatmentTypes.forEach { (shampoo, treatment) ->
        println("El shampoo $shampoo es para el tratamiento $treatment")
    }
}
```

`forEach()` recibe una lambda cuyo contexto es cada `Map.Entry<K, V>`, lo que permite desestructurar clave y valor directamente en los parámetros.
