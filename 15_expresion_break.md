# La Expresión `break` en Kotlin

`break` es una expresión de salto que solo se permite dentro de bucles. Su objetivo es pasar el control al siguiente punto del programa tras el bucle, finalizándolo de forma anticipada.

---

## `break` simple

En su forma simple, `break` provoca un salto de ruptura en el **bucle más interno** del alcance actual.

**Ejemplo — terminar cuando el usuario escribe "salir":**
```kotlin
fun main() {
    while (true) {
        print("Escribe una palabra:")
        val word = readLine()!!
        if (word == "salir") break
        println("Caracteres:${word.length}")
    }
}
```

**Ejemplo — validar una matriz y detenerse en la primera fila inválida:**
```kotlin
fun main() {
    val matrix = arrayOf(
        intArrayOf(1, 1, 1),
        intArrayOf(0, 1, 0),
        intArrayOf(1, 1, 0),
    )
    for (row in matrix.indices) {
        for (col in matrix[row].indices) {
            if (matrix[row][col] == 0) {
                println("Matriz inválida en [$col,$row]")
                break  // Solo sale del bucle de columnas (el más interno)
            }
        }
    }
}
// Salida:
// Matriz inválida en [0,1]
// Matriz inválida en [2,2]
```

> En bucles anidados, `break` simple solo termina el **bucle más interno**. Por eso se imprimen dos resultados en el ejemplo anterior.

---

## `break` etiquetado

Permite salir de un bucle externo específico. Se define con la sintaxis `break@etiqueta`, donde la etiqueta identifica el bucle con el símbolo `@` como sufijo.

```kotlin
etiqueta@ for (i in 1..5) {
    for (j in 1..7) {
        if (...) break@etiqueta  // Sale del bucle externo etiquetado
    }
}
```

**Ejemplo — detener la búsqueda en la primera aparición de un cero en la matriz:**
```kotlin
fun main() {
    val matrix = arrayOf(
        intArrayOf(1, 1, 1),
        intArrayOf(0, 1, 0),
        intArrayOf(1, 1, 0),
    )
    Loop@ for (row in matrix.indices) {
        for (col in matrix[row].indices) {
            if (matrix[row][col] == 0) {
                println("Matriz inválida en [$col,$row]")
                break@Loop  // Sale del bucle de filas (Loop)
            }
        }
    }
}
// Salida: Matriz inválida en [0,1]
```

Con `break@Loop` se termina completamente la búsqueda al encontrar el primer cero, evitando iteraciones innecesarias.
