# Arrays En Kotlin

En este tutorial discutiremos sobre el uso de Arrays en Kotlin con el fin de representar vectores (arreglos) en nuestras aplicaciones. Verás cómo crearlos, el acceso y modificación de sus elementos, y cómo recorrerlos.

---

## Crear Arrays

Un arreglo es una estructura con valores de datos que están almacenados de forma contigua en memoria. Todos los elementos son referenciados por un mismo nombre y tienen el mismo tipo de dato.

Los elementos estarán indexados tomando como base el `0` y el tamaño declarado del arreglo será fijo.

Kotlin usa la clase genérica `Array<T>` para representar arreglos. Crear instancias con un tipo parametrizado usa los siguientes métodos:

- `arrayOf(vararg elements: T)` — recibe un argumento variable con elementos de tipo `T` y retorna el arreglo que los contiene.
- `arrayOfNulls(size: Int)` — crea un arreglo de tamaño `size` con elementos de tipo `T` e inicializa los valores con `null`.
- `emptyArray()` — crea un arreglo vacío con el tipo `T`.

**Por ejemplo:** Considera que necesitas almacenar el valor de los ingresos de 12 meses del usuario. En vez de crear 12 variables para cada mes, optas por crear un arreglo:

```kotlin
val income = arrayOf<Double>(
    0.5, 2.5, 4.0, 5.0,
    4.5, 6.0, 7.6, 8.0,
    5.0, 6.4, 4.0, 9.1
)
```

> Al igual que cualquier declaración de instancias, puedes omitir el tipo parametrizado `<Double>` porque el compilador de Kotlin puede inferirlo.

---

## Usar Constructor Array()

Si deseas crear un array con un tamaño específico y calcular todos sus elementos a partir de una función, usa el constructor `Array(size, init)`.

**Por ejemplo**, crear un array con los números del 1 al 10 con signo negativo:

```kotlin
fun main() {
    val negativeNumbers = Array(10) { -(it + 1) }
    println(negativeNumbers.joinToString())
}
```

Salida:

```
-1, -2, -3, -4, -5, -6, -7, -8, -9, -10
```

El segundo parámetro `init` de `Array()` es del tipo función `Int -> T`, donde el parámetro entero es el índice y el cuerpo la expresión que calcula el valor del elemento. Por esto pasamos la función lambda `{ -(it + 1) }`.

La función `joinToString()` permite crear un `String` legible para imprimir. También puedes usar `contentToString()`:

```kotlin
println(negativeNumbers.contentToString())
// [-1, -2, -3, -4, -5, -6, -7, -8, -9, -10]
```

---

## Acceso A Elementos

La clase `Array` te provee operadores `set()` y `get()` para asignar y obtener valores en los índices. Sin embargo, es preferible usar el **operador de acceso indexado** `[]` para referirte a los elementos.

```kotlin
fun main() {
    val planets = arrayOfNulls<String>(8)
    planets[0] = "Mercurio"
    planets[1] = "Venus"
    planets[2] = "Tierra"
    planets[3] = "Júpiter"
    planets[4] = "Saturno"
    planets[5] = "Urano"
    planets[6] = "Neptuno"
    planets[7] = "Plutón"
    println(planets.contentToString())
}
```

Salida:

```
[Mercurio, Venus, Tierra, Júpiter, Saturno, Urano, Neptuno, Plutón]
```

La tierra como está en la posición 3 sería asignada con `[2]` (índice base 0).

---

## Recorrer Arrays

Una de las formas más convencionales de recorrer arreglos es a través del bucle `for` con el operador `in` junto a la propiedad de extensión `indices`, que contiene el rango válido de los índices del array:

```kotlin
fun main() {
    val planets = arrayOfNulls<String>(8)
    planets[0] = "Mercurio"
    planets[1] = "Venus"
    planets[2] = "Tierra"
    planets[3] = "Júpiter"
    planets[4] = "Saturno"
    planets[5] = "Urano"
    planets[6] = "Neptuno"
    planets[7] = "Plutón"

    for (i in planets.indices) {
        println("${planets[i]} está en la posición ${i + 1}")
    }
}
```

Salida:

```
Mercurio está en la posición 1
Venus está en la posición 2
Tierra está en la posición 3
Júpiter está en la posición 4
Saturno está en la posición 5
Urano está en la posición 6
Neptuno está en la posición 7
Plutón está en la posición 8
```

También es posible usar el atributo `size` del mismo array:

```kotlin
for (i in 0 until planets.size) {
    println("${planets[i]} está en la posición ${i + 1}")
}
```

Otra opción es usar la función de extensión `forEachIndexed()`, la cual recibe como parámetros el índice y el valor:

```kotlin
planets.forEachIndexed { i, v ->
    println("$v está en la posición ${i + 1}")
}
```
