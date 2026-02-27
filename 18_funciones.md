# Funciones en Kotlin

Una función es un conjunto de instrucciones que realizan una tarea específica, empaquetadas como unidad. Kotlin permite aplicar estilos de programación funcional, por lo que las funciones son una herramienta indispensable.

---

## Sintaxis de declaración

```kotlin
fun nombreFuncion(parametro: Tipo): TipoRetorno {
    // cuerpo
    return valor
}
```

La declaración comienza con la palabra clave `fun` y se compone de:

- **Nombre** — identifica el propósito de la función.
- **Lista de parámetros** — datos de entrada con formato `nombre: Tipo`, separados por comas.
- **Tipo de retorno** — tipo del dato que devuelve. Obligatorio en funciones con cuerpo de bloque.
- **Cuerpo** — sentencias que realizan la tarea. Se usa `return` para devolver el valor.

**Ejemplo:**
```kotlin
fun square(x: Int): Int {
    return x * x
}
```

---

## Llamar una función

```kotlin
fun square(x: Int): Int {
    return x * x
}

fun main() {
    print(square(2))  // Salida: 4
}
```

---

## Funciones con cuerpo de expresión

Si la función retorna una sola expresión, se puede reducir su sintaxis colocando la expresión tras el signo `=`, en la misma línea que la firma. El compilador **infiere el tipo de retorno** automáticamente.

```kotlin
fun model(x: Int, y: Int, z: Int) = 3 * x - 2 * y + z * z

fun main() {
    println("f(1,0,5)= ${model(1, 0, 5)}")
}
// Salida: f(1,0,5)= 28
```

> IntelliJ IDEA puede realizar la conversión a *single-expression body* automáticamente desde las acciones emergentes de la función.

---

## Retorno tipo `Unit`

`Unit` es el equivalente a `void` en Java: indica que la función no retorna un valor significativo. Puede **omitirse** de la declaración, ya que el compilador lo infiere como excepción a la regla general.

```kotlin
// Con Unit explícito
fun isVowel(c: Char): Unit {
    when (c) {
        'a', 'e', 'i', 'o', 'u' -> println("$c es una vocal")
        else -> println("$c no es una vocal")
    }
}

// Unit omitido (equivalente)
fun isVowel(c: Char) {
    when (c) {
        'a', 'e', 'i', 'o', 'u' -> println("$c es una vocal")
        else -> println("$c no es una vocal")
    }
}

fun main() {
    isVowel('v')
}
// Salida: v no es una vocal
```
