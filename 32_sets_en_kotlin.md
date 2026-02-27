# Sets En Kotlin

Un **conjunto o set** es una colección de elementos sin ordenar que no soporta duplicados. Su diseño conceptual se basa en el modelo de los conjuntos matemáticos.

---

## Sets de Solo Lectura

La interfaz genérica `Set<E>` representa los conjuntos de solo lectura en `kotlin.collections`. Extiende de `Collection<E>`:

```kotlin
interface Set<out E> : Collection<E>
```

Para crear un conjunto de solo lectura se usa `setOf()`:

```kotlin
fun main() {
    val positiveNumbers = setOf(1, 2, 3, 4)
    println(positiveNumbers)

    val cities = setOf("Cali", "Armenia", "Cartagena", null)
    println(cities)

    val diamondCardsHand = setOf('A', 1, 2, 3, 'J', 'Q', 'K')
    println(diamondCardsHand)
}
// [1, 2, 3, 4]
// [Cali, Armenia, Cartagena, null]
// [A, 1, 2, 3, J, Q, K]
```

---

## Igualdad de Conjuntos

Dos conjuntos son iguales aunque sus elementos hayan sido incluidos en diferente orden o la inicialización tenga copias:

```kotlin
fun main() {
    val a = setOf(1, 2, 3, 4, 4, 4)
    println(a == setOf(1, 2, 3, 4)) // true
    println(setOf(1, 2, 3) == setOf(2, 3, 1)) // true
}
```

---

## El Método contains()

Para comprobar si un elemento pertenece al conjunto se usa `contains(element)` o el operador `in`:

```kotlin
fun main() {
    val numbersSet = setOf(1, 3, 5, 7, 9, 11)
    println(numbersSet.contains(2)) // false
    println(3 in numbersSet)        // true
    println(numbersSet.containsAll(setOf(1, 3))) // true
}
```

---

## Sets Mutables

Para añadir y remover elementos se implementa la interfaz `MutableSet<E>` usando `mutableSetOf()`:

```kotlin
interface MutableSet<E> : Set<E>, MutableCollection<E>

fun main() {
    val setA = mutableSetOf(1, 6, 7, 10)
    val setB = mutableSetOf<Int>()
    println("A=$setA y B=$setB") // A=[1, 6, 7, 10] y B=[]
}
```

### Añadir Elementos

```kotlin
setB.add(1)  // [1]
setB += 2    // [1, 2]
setB += 2    // [1, 2] (no duplicados)
```

### Remover Elementos

```kotlin
setB.remove(1) // [2]
setB -= 2      // []
setB -= 3      // [] (no efecto)
```

> `add()` y `remove()` retornan `Boolean` indicando si la operación fue exitosa.

---

## Operaciones Entre Conjuntos

### union()

Retorna un conjunto con todos los elementos de ambas colecciones:

```kotlin
fun main() {
    val group1 = setOf(1, 3, 5, 7)
    val group2 = setOf(2, 4, 6, 8)
    println("U = ${group1 union group2}")
}
// U = [1, 3, 5, 7, 2, 4, 6, 8]
```

### intersect()

Retorna solo los elementos presentes en ambas colecciones:

```kotlin
fun main() {
    println("∩= ${setOf(0, 1, 3, 4) intersect setOf(2, 3, 4, 5)}")
}
// ∩= [3, 4]
```

### subtract()

Calcula la diferencia: elimina de A cualquier elemento que esté en B:

```kotlin
fun main() {
    val difference = setOf(10, 11, 12, 13) subtract setOf(9, 10, 11)
    println("A\\B = $difference")
}
// A\B = [12, 13]
```
