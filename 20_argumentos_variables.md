# Funciones con Argumentos Variables en Kotlin

Kotlin permite declarar funciones que acepten un número ilimitado de valores del mismo tipo mediante el modificador `vararg`.

---

## Sintaxis

```kotlin
fun nombreFuncion(vararg parametro: Tipo) {
    /* ... */
}
```

Se aplica el modificador `vararg` al parámetro que debe aceptar un número variable de valores.

> **Restricción:** solo puede haber **un único parámetro** `vararg` por función. Si se intenta agregar más de uno, el compilador marcará error.

---

## Ejemplo

Determinar cuántos caracteres tiene la palabra más larga entre una lista de n elementos:

```kotlin
fun maxLength(vararg words: String): Int {
    var max = 0
    for (word in words) {
        if (word.length > max) {
            max = word.length
        }
    }
    return max
}

fun main() {
    val max = maxLength("Carro", "Manzana", "Bosque", "Avión")
    print("La palabra más larga tiene $max caracteres")
}
// Salida: La palabra más larga tiene 7 caracteres
```

La función puede llamarse con cualquier número de argumentos:

```kotlin
maxLength()                          // 0 argumentos
maxLength("Uno")                     // 1 argumento
maxLength("Uno", "Dos")              // 2 argumentos
maxLength("Uno", "Dos", "Tres")      // 3 argumentos
// ...
```

Internamente, el parámetro `vararg` es tratado como un **array** del tipo declarado, por lo que se puede iterar sobre sus elementos o usar funciones de la librería estándar sobre él.

---

## El operador Spread (`*`)

Si ya tienes un array declarado y quieres pasarlo como argumento a una función `vararg`, usa el **operador spread** (`*`) como prefijo del argumento.

```kotlin
fun main() {
    val words = arrayOf("Carro", "Manzana", "Bosque", "Avión")
    print("La palabra más larga tiene ${maxLength(*words)} caracteres")
}
// Salida: La palabra más larga tiene 7 caracteres
```

Sin el operador `*`, el compilador interpretaría el array como un único argumento en lugar de expandir sus elementos.
