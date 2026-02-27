# Funciones De Orden Superior En Kotlin

Una **función de orden superior** es una función que puede recibir como argumento una o más funciones y/o retornar una función como resultado.

---

## Tomar Funciones Como Argumentos

Para recibir funciones como parámetros, se declara el tipo función en la firma:

```kotlin
// Pasar función como argumento de otra función
fun recibirFuncion(parametro1: (String) -> Int, parametro2: Double) {
    val numero: Int = parametro1("Arg")
    print(numero)
}
```

### Ejemplo: juego de cartas

```kotlin
fun playEffectCard(cardCost1: Int, cardCost2: Int, onSuccess: () -> Unit) {
    if (cardCost1 > cardCost2) {
        onSuccess()
    } else {
        println("Sin efectos")
    }
}

fun main() {
    val warriorCardCost = 1
    val randomDeckCardCost = 4
    playEffectCard(warriorCardCost, randomDeckCardCost) { print("Aumentar armadura por 10") }
}
// Sin efectos
```

---

## Pasar Referencia de Función

En lugar de un lambda, se puede pasar una referencia de función existente usando `::`:

```kotlin
fun increaseArmor() {
    print("Aumentar armadura por 10")
}

fun main() {
    val warriorCardCost = 1
    val randomDeckCardCost = 4
    playEffectCard(warriorCardCost, randomDeckCardCost, ::increaseArmor)
}
```

---

## Retornar Funciones Desde Funciones

El tipo función se declara como tipo de retorno en la firma. Se usa `return` para devolver un literal de función o referencia:

```kotlin
// Retornar función desde otra función
fun retornarFuncion(parametro1: Int): () -> Unit {
    return { println(parametro1) }
}
```

### Ejemplo: conversor de unidades

```kotlin
import Dimension.*

enum class Dimension {
    CM, INCH, FOOT, YARD
}

fun getConversion(dimension: Dimension): (Double) -> Double {
    return when (dimension) {
        CM   -> { mts -> mts * 100 }
        INCH -> { mts -> mts * 39.37 }
        FOOT -> { mts -> mts * 3.281 }
        YARD -> { mts -> mts * 1.094 }
    }
}

fun main() {
    val meters = 20.0
    print(getConversion(FOOT)(meters))
}
// 65.62
```

> Como `getConversion()` retorna una función, se pueden encadenar los paréntesis para invocarla directamente: `getConversion(FOOT)(meters)`.
