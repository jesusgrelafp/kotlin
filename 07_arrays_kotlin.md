# Arrays En Kotlin

En este tutorial discutiremos sobre el uso de Arrays en Kotlin con el fin de representar vectores (arreglos) en nuestras aplicaciones. Verás cómo crearlos, el acceso y modificación de sus elementos, y cómo recorrerlos.

---

## Crear Arrays

Un arreglo es una estructura con valores de datos que están almacenados de forma contigua en memoria. Todos los elementos son referenciados por un mismo nombre y tienen el mismo tipo de dato.

Los elementos estarán indexados tomando como base el `0` y el tamaño declarado del arreglo será fijo.

Kotlin usa la clase genérica `Array<T>` para representar arreglos. Crear instancias con un tipo parametrizado usa los siguientes métodos:

- `arrayOf<T>(vararg elements: T)` — recibe un argumento variable con elementos de tipo `T` y retorna el arreglo que los contiene.
- `arrayOfNulls<T>(size: Int)` — crea un arreglo de tamaño `size` con elementos de tipo `T` e inicializa los valores con `null`.
- `emptyArray<T>()` — crea un arreglo vacío con el tipo `T`.

**Por ejemplo:** Considera que necesitas almacenar el valor de los ingresos de 12 meses del usuario. En vez de crear 12 variables para cada mes, optas por crear un arreglo:

```kotlin
val income = arrayOf<Double>(
    0.5, 2.5, 4.0, 5.0,
    4.5, 6.0, 7.6, 8.0,
    5.0, 6.4, 4.0, 9.1
)
```

> Al igual que cualquier declaración de instancias, puedes omitir el tipo parametrizado `<Double>` porque el compilador de Kotlin puede inferirlo.

**Ejemplo de `emptyArray()`:** Útil cuando necesitas un valor por defecto o inicial antes de rellenar el arreglo más adelante:

```kotlin
fun main() {
    var tags = emptyArray<String>()
    println("Tamaño inicial: ${tags.size}")

    tags = arrayOf("kotlin", "android", "dam")
    println("Tamaño tras asignar: ${tags.size}")
}
```

Salida:

```
Tamaño inicial: 0
Tamaño tras asignar: 3
```

**Ejemplo de `arrayOfNulls()`:** Útil cuando conoces el tamaño del arreglo pero vas a rellenar los valores más adelante:

```kotlin
fun main() {
    val colors = arrayOfNulls<String>(3)
    println(colors.contentToString())

    colors[0] = "Rojo"
    colors[1] = "Verde"
    colors[2] = "Azul"
    println(colors.contentToString())
}
```

Salida:

```
[null, null, null]
[Rojo, Verde, Azul]
```

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

## Arrays De Tipos Primitivos

Cuando `Array<T>` se usa con un tipo numérico (por ejemplo `Array<Double>` o `Array<Int>`), Kotlin lo compila internamente como un array de **objetos** (con *boxing*), lo que supone un coste extra de memoria y rendimiento.

Para evitar ese coste, Kotlin ofrece **arrays especializados** para cada tipo primitivo, que se compilan directamente a los arrays nativos de la JVM (`int[]`, `double[]`, etc.):

| Array especializado | Tipo primitivo | Valor por defecto |
|---|---|---|
| `IntArray` | `Int` | `0` |
| `ByteArray` | `Byte` | `0` |
| `ShortArray` | `Short` | `0` |
| `LongArray` | `Long` | `0L` |
| `FloatArray` | `Float` | `0.0f` |
| `DoubleArray` | `Double` | `0.0` |
| `CharArray` | `Char` | `\u0000` |
| `BooleanArray` | `Boolean` | `false` |

Todos admiten los mismos dos constructores:

```kotlin
val notas = DoubleArray(5)                // [0.0, 0.0, 0.0, 0.0, 0.0]
val cuadrados = IntArray(5) { it * it }    // [0, 1, 4, 9, 16]
```

Y todos tienen también su función `xxxArrayOf()`, equivalente a `arrayOf()` pero con el tipo primitivo ya fijado:

```kotlin
val edades = intArrayOf(23, 45, 12, 8)
val activos = booleanArrayOf(true, false, true)
```

> **Cuidado:** `arrayOf<Double>(5)` **no** es lo mismo que `DoubleArray(5)`. En `arrayOf`, el `5` no indica un tamaño, sino que se interpreta como un elemento del `vararg`, así que `arrayOf<Double>(5.0)` crea un array de **tamaño 1** con el valor `5.0`, no un array de tamaño 5. Para tipos primitivos con un tamaño dado, usa siempre el array especializado (`DoubleArray(5)`) o el constructor `Array(size, init)` visto antes.

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
