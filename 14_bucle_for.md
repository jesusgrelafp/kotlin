# Bucle `for` en Kotlin

El bucle `for` itera sobre cualquier objeto que provea un iterador (`iterator()`). Es similar al `foreach` de otros lenguajes. Se puede usar con rangos, arreglos, listas y strings.

---

## Sintaxis

La sentencia se compone de una **declaración de variable**, una **expresión contenedora** (operador `in` + datos estructurados) y el **cuerpo del bucle**.

```kotlin
for (variable in coleccion) {
    // cuerpo
}
```

**Ejemplo — contar del 1 al 5:**
```kotlin
fun main() {
    for (i in 1..5) {
        println("Contando $i")
    }
}
// Salida:
// Contando 1
// Contando 2
// Contando 3
// Contando 4
// Contando 5
```

Al ser una sola sentencia, se pueden omitir las llaves:
```kotlin
for (i in 1..5) println("Contando $i")
```

---

## Recorrer un rango

```kotlin
fun main() {
    // Iteración regular
    for (char in 'a'..'f') print(char)          // abcdef
    println()

    // Con avance de 2 (step)
    for (char in 'a'..'f' step 2) print(char)   // ace
    println()

    // En reversa
    for (char in 'f' downTo 'a') print(char)    // fedcba
    println()

    // Excluyendo el límite superior (until)
    for (char in 'a' until 'f') print(char)     // abcde
}
```

---

## Recorrer un array

Para iterar sobre un arreglo se usan los índices mediante la propiedad `indices`.

```kotlin
fun main() {
    val champions = arrayOf("Teemo", "Ahri", "Vayne", "Brand", "Kindred")
    for (i in champions.indices) {
        println("[$i, ${champions[i]}]")
    }
}
// Salida:
// [0, Teemo]
// [1, Ahri]
// [2, Vayne]
// [3, Brand]
// [4, Kindred]
```

### Con `withIndex()` y desestructuración

El método `withIndex()` retorna elementos `IndexedValue` que pueden recibirse como una declaración de desestructuración `(indice, valor)`.

```kotlin
fun main() {
    val champions = arrayOf("Teemo", "Ahri", "Vayne", "Brand", "Kindred")
    for ((i, v) in champions.withIndex()) {
        println("[$i, $v]")
    }
}
```

---

## Recorrer un String

El bucle `for` puede iterar sobre un string carácter a carácter.

```kotlin
fun main() {
    for (c in "Kotlin") {
        println(c)
    }
}
// Salida:
// K
// o
// t
// l
// i
// n
```
