# Excepciones en Kotlin

Las excepciones permiten conducir el flujo de un programa a un estado consistente cuando ocurren errores en tiempo de ejecución. Kotlin usa las expresiones `throw` y `try` para lanzarlas y manejarlas.

---

## Lanzar excepciones con `throw`

Se usa la expresión `throw` seguida de la instanciación del tipo de excepción. El tipo debe tener como supertipo la interfaz `Throwable` (igual que en Java).

**Ejemplo — validar que la entrada del usuario no esté vacía:**

```kotlin
fun main() {
    print("Escribe el texto: ")
    val userInput = readLine()
    println("Cantidad de dígitos: ${countDigits(userInput)}")
}

fun countDigits(userInput: String?): Int {
    if (userInput.isNullOrBlank()) {
        throw IllegalArgumentException("Entrada inválida, la palabra no puede estar vacía")
    }
    return userInput.count(Char::isDigit)
}
```

**Salida al no introducir texto:**
```
Escribe el texto:
Exception in thread "main" java.lang.IllegalArgumentException: Entrada inválida...
```

### `throw` como expresión

En Kotlin, `throw` es una **expresión**, lo que permite usarlo directamente dentro de otras expresiones. La función anterior puede reescribirse como cuerpo de expresión única:

```kotlin
fun countDigits(userInput: String?) =
    if (userInput.isNullOrBlank())
        throw IllegalArgumentException("Entrada inválida, la palabra no puede estar vacía")
    else
        userInput.count(Char::isDigit)
```

---

## Manejar excepciones con `try..catch..finally`

```kotlin
try {
    // Código propenso a lanzar excepciones
} catch (e: TipoDeExcepcion) {
    // Manejo del error
} finally {
    // Siempre se ejecuta (liberación de recursos, limpieza)
}
```

**Ejemplo — convertir un String a Double con valor por defecto en caso de error:**

```kotlin
fun main() {
    println("5.3".toDoubleOrDefault(1.0))   // 5.3
    println("5.".toDoubleOrDefault(1.0))    // 5.0
    println(".3".toDoubleOrDefault(1.0))    // 0.3
    println("dos".toDoubleOrDefault(1.0))   // 1.0  ← valor por defecto
}

fun String.toDoubleOrDefault(defaultValue: Double): Double {
    return try {
        toDouble()
    } catch (e: NumberFormatException) {
        defaultValue
    }
}
```

El bloque `catch` captura el `NumberFormatException` que lanza `toDouble()` cuando el formato es inválido y retorna el valor por defecto.

### Versión con cuerpo de expresión

```kotlin
fun String.toDoubleOrDefault(defaultValue: Double) = try {
    toDouble()
} catch (e: NumberFormatException) {
    defaultValue
}
```

---

## Excepciones marcadas (checked exceptions)

Kotlin **no diferencia** entre excepciones marcadas y no marcadas (*checked* y *unchecked*). Las funciones no están obligadas a declarar qué excepciones lanzan (no existe la cláusula `throws` de Java), ni el compilador obliga a capturarlas.

**Ejemplo:** abrir un archivo inexistente no genera un error de compilación en Kotlin:

```kotlin
fun main() {
    val stream = FileInputStream("archivo inválido")  // Compila sin try..catch
}
```

Aunque en tiempo de ejecución lanza:
```
Exception in thread "main" java.io.FileNotFoundException: archivo inválido
```

> Esto no significa ignorar los errores. El manejo de excepciones sigue siendo necesario. La ventaja es que evita la propagación en cadena de cambios entre firmas de funciones cuando se modifican las excepciones.
