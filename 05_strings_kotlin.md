# Strings En Kotlin

En este tutorial verás la definición, declaración y uso de Strings en Kotlin con el fin de representar texto como tipo básico en tus aplicaciones.

---

## El Tipo String

La clase `String` es la que representa a los strings en Kotlin con el fin de tratar texto en nuestros programas.

```kotlin
class String : Comparable<String>, CharSequence
```

Cada literal `String` de la forma `"cadena"` es creado como una instancia de la clase. Por lo que solo basta con usar las comillas dobles para encerrar múltiples caracteres que representen el String deseado:

```kotlin
val customerName: String = "Claudia Martinez"
val customerName = "Claudia Martinez" // Puedes omitir el tipo
```

---

## Caracteres De Un String

Debido a que `String` implementa la interfaz `CharSequence`, es posible interpretar el conjunto como una secuencia de elementos `Char`.

Esto te permitirá leer los caracteres en sus posiciones a través de `get()` o su operador equivalente de acceso en corchetes `string[indice]`:

```kotlin
println(customerName[5])
println(customerName.get(5))
```

También es posible recorrerlos a través del bucle `for`:

```kotlin
for (char in customerName) {
    print(char)
}
```

Incluso usar la propiedad de extensión `indices` para obtener el rango de índices:

```kotlin
for (index in customerName.indices) {
    println(customerName[index])
}
```

Si quieres saber el tamaño de la secuencia de caracteres, accede a la propiedad `length`:

```kotlin
println(customerName.length) // 16
```

---

## Concatenar Strings En Kotlin

Para crear la combinación de varios valores en un solo `String`, usa el operador de adición `+` como herramienta de concatenación.

```kotlin
// Concatenación
val a = "José" + " Monteria"
val b = "Cantidad de ahorros: " + 536.4
val c = "Resultado: " + (2 + 4)

var d = "Nueva concatenación"
d += '!' // "Nueva concatenación!"
```

---

## Strings Con Múltiples Líneas

En ocasiones es necesario crear literales de String que posean múltiples líneas y que sean interpretadas en su forma plana (raw strings).

Esto puedes lograrlo usando la sintaxis de triple doble comillas (`"""`) para encerrar el conjunto de caracteres:

```kotlin
fun main() {
    // raw string
    val welcomeText = """
    ¡Bienvenido a la guía de Kotlin!
    En esta serie de tutoriales aprenderás 
    los conceptos básicos sobre el lenguaje
    y las herramientas necesarias para probarlo
    """
    println(welcomeText)
}
```

Como ves, la construcción del String con múltiples líneas conserva la sangría y espacios de origen. Para eliminarlos usa la función `trimMargin()`, la cual usa como referencia el prefijo `|` como delimitador de las márgenes:

```kotlin
fun main() {
    // raw string
    val welcomeText = """
    |¡Bienvenido a la guía de Kotlin!
    |En esta serie de tutoriales aprenderás 
    |los conceptos básicos sobre el lenguaje
    |y las herramientas necesarias para probarlo
    """.trimMargin()
    println(welcomeText)
}
```

Salida:

```
¡Bienvenido a la guía de Kotlin!
En esta serie de tutoriales aprenderás 
los conceptos básicos sobre el lenguaje
y las herramientas necesarias para probarlo
```

---

## Plantillas De Strings En Kotlin

En Kotlin es posible crear expresiones interpoladas sobre Strings, también conocidas como **String Templates**.

La interpolación te permite concatenar literales junto a fragmentos de expresiones antecedidas por el símbolo `$`. Hay dos formas de hacerlo:

- `$id` — donde `id` es un identificador simple
- `${e}` — donde `e` es una expresión válida en Kotlin

**Ejemplo con identificador simple:**

```kotlin
fun main() {
    val playerName = "NKiller"
    println("Tu nuevo nombre es $playerName")
}
```

Salida:

```
Tu nuevo nombre es NKiller
```

**Ejemplo con expresión:**

```kotlin
fun main() {
    println("Tamaño del nick:${playerName.length}")
}
```

Salida:

```
Tamaño del nick:7
```

La expresión `${playerName.length}` es resuelta primero accediendo al entero `7` y luego se convierte a través del método `toString()`.

Este tipo de plantillas te permitirá incluir todo tipo de expresiones como operaciones aritméticas, acceso a métodos, ejecución de funciones, etc.
