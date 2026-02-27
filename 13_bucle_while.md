# Bucle `while` en Kotlin

El bucle `while` ejecuta su cuerpo repetidamente mientras una condición sea `true`, o hasta que se evalúe una expresión de salto.

---

## Sintaxis

Las sentencias del bucle se componen de una **expresión condicional** (subtipo de `kotlin.Boolean`) y un **cuerpo** de cero o más sentencias.

```kotlin
while (condition) {
    /* ... */
}
```

**Ejemplo — sumatoria del 1 al 10:**
```kotlin
fun main() {
    var sum = 0
    var i = 1
    while (i <= 10) {
        sum += i++
    }
    println("Sumatoria:$sum")
}
// Salida: Sumatoria:55
```

Para cuerpos de una sola sentencia se pueden omitir las llaves:
```kotlin
while (i <= 10) sum += i++
```

---

## Bucle `do..while`

La condición se evalúa **después** de ejecutar el cuerpo, lo que garantiza que el cuerpo se ejecute **al menos una vez** sin importar la condición inicial.

```kotlin
do {
    /* ... */
} while (condicion)
```

**Ejemplo — preguntar la capital de Colombia hasta acertar:**
```kotlin
fun main() {
    do {
        println("¿Cuál es la capital de Colombia?:")
        println("a. La Paz")
        println("b. Buenos Aires")
        println("c. La Habana")
        println("d. Bogotá")
        print("Respuesta:")
        val option = readLine()!!
        val again = option != "d"
        if (again) {
            println("¡Incorrecto!\n")
        } else {
            println("¡Felicitaciones!\n")
        }
    } while (again)
}
```

La primera pregunta se muestra sin evaluar la condición. El proceso se repite hasta que `again` sea `false`, es decir, hasta que el usuario responda `"d"`.
