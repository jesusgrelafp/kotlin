# Argumentos por Defecto y Nombrados en Kotlin

Kotlin permite declarar parámetros con valores por defecto y especificar el nombre de los argumentos en la llamada, aumentando la flexibilidad y legibilidad de las funciones.

---

## Argumentos por defecto

Para asignar un valor por defecto a un parámetro, se usa el operador `=` en su declaración. Si no se pasa el argumento al llamar la función, se usará el valor por defecto.

```kotlin
val customers = arrayOf("Carlos", "Miguel", "Ximena")

fun loadCustomer(limit: Int = 0): String {
    return customers[limit]
}

fun main() {
    println("Cliente:${loadCustomer()}")   // Usa el valor por defecto (0)
    println("Cliente:${loadCustomer(2)}")  // Usa el índice 2
}
// Salida:
// Cliente:Carlos
// Cliente:Ximena
```

### Problema con parámetros por defecto no al final

Si un parámetro con valor por defecto precede a uno sin valor por defecto, no es posible omitir el primero sin provocar un error de compilación, ya que los argumentos siguen un orden posicional.

```kotlin
fun loadCustomer(limit: Int = 0, length: Int): String {
    return customers[limit].take(length)
}

fun main() {
    loadCustomer(3)  // Error: No value passed for parameter 'length'
}
```

La solución es usar **argumentos nombrados**.

---

## Argumentos nombrados

Permiten especificar a qué parámetro corresponde cada argumento usando la sintaxis:

```
nombreParametro = valorArgumento
```

Esto permite omitir parámetros con valor por defecto independientemente de su posición.

```kotlin
val customers = arrayOf("Carlos", "Miguel", "Ximena")

fun loadCustomer(limit: Int = 0, length: Int): String {
    return customers[limit].take(length)
}

fun main() {
    println("Cliente:${loadCustomer(length = 3)}")
}
// Salida: Cliente:Car
```

El compilador obtiene el valor por defecto de `limit` (0) e incorpora correctamente el argumento `length = 3`, retornando los primeros 3 caracteres del cliente en la posición 0.

> Los argumentos nombrados aumentan la flexibilidad al permitir pasar únicamente los parámetros estrictamente necesarios para cada situación.
