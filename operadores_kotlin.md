# Operadores En Kotlin

En este tutorial, aprenderás acerca de los operadores en Kotlin y cómo usarlos para crear expresiones con variables.

---

## Operadores De Signo

Comenzamos con los operadores unarios que representan la propiedad de un número de ser negativo (`-`) o positivo (`+`).

| Operador | Expresión | Función equivalente |
|----------|-----------|---------------------|
| `+`      | `+a`      | `a.unaryPlus()`     |
| `-`      | `-a`      | `a.unaryMinus()`    |

**Ejemplo:** Negar una variable con el valor de -3:

```kotlin
fun main() {
    val a = -3
    println("a=${-a}")
}
```

Salida:

```
a=3
```

---

## Operadores Aritméticos

Te permiten expresar operaciones aritméticas entre dos operandos.

| Operador | Operación      | Expresión | Función Equivalente |
|----------|----------------|-----------|---------------------|
| `+`      | Suma           | `a + b`   | `a.plus(b)`         |
| `-`      | Resta          | `a - b`   | `a.minus(b)`        |
| `*`      | Multiplicación | `a * b`   | `a.times(b)`        |
| `/`      | División       | `a / b`   | `a.div(b)`          |
| `%`      | Residuo        | `a % b`   | `a.rem(b)`          |

**Ejemplo:** Imprimir el resultado de todas las operaciones aritméticas con los números 10 y 20:

```kotlin
fun main() {
    val a = 10
    val b = 20
    println("($a + $b)= ${a + b}")
    println("($a - $b)= ${a - b}")
    println("($a x $b)= ${a * b}")
    println("($a / $b)= ${a / b}")
    println("($a % $b)= ${a % b}")
}
```

Salida:

```
(10 + 20)= 30
(10 - 20)= -10
(10 x 20)= 200
(10 / 20)= 0
(10 % 20)= 10
```

> Al dividir dos enteros, se conserva la parte entera como resultado y se descartan los decimales.

---

## Operadores De Asignación Compuesta

Estos operadores son la combinación entre el operador de asignación y los operadores aritméticos. Por ejemplo, para acumular el valor de `b` en `a`:

```kotlin
a += b // a = a + b
```

| Operador | Expresión simplificada | Expresión Completa | Función Equivalente     |
|----------|------------------------|--------------------|-------------------------|
| `+=`     | `a += b`               | `a = a + b`        | `a.plusAssign(b)`       |
| `-=`     | `a -= b`               | `a = a - b`        | `a.minusAssign(b)`      |
| `*=`     | `a *= b`               | `a = a * b`        | `a.timesAssign(b)`      |
| `/=`     | `a /= b`               | `a = a / b`        | `a.divAssign(b)`        |
| `%=`     | `a %= b`               | `a = a % b`        | `a.remAssign(b)`        |

**Ejemplo:** Aplicar todos los operadores de asignación compuesta con un operando de 5 sobre un valor de 100:

```kotlin
fun main() {
    var a = 100
    val b = 5
    a += b
    println("+= $a")
    a -= b
    println("-= $a")
    a *= b
    println("*= $a")
    a /= b
    println("/= $a")
    a %= b
    println("%= $a")
}
```

Salida:

```
+= 105
-= 100
*= 500
/= 100
%= 0
```

---

## Operadores De Incremento Y Decremento

El operador de incremento (`++`) incrementa en la unidad al operando. El operador de decremento (`--`) disminuye en la unidad al operando.

El resultado depende de si el operador es **prefijo** o **sufijo**:

- **Prefijo:** Se realiza el incremento sobre la variable y luego es usada en la expresión.
- **Sufijo:** Se usa la variable en la expresión y luego se aplica el incremento.

**Ejemplo:**

```kotlin
fun main() {
    var a = 2
    println("De $a a ${++a}")
    println("De $a a ${a--}")
    println("Valor final > $a")
}
```

Salida:

```
De 2 a 3
De 3 a 3
Valor final > 2
```

Aunque el valor es disminuido en la segunda impresión, este no se hace efectivo sino hasta que se termina la línea. Por eso el resultado final es `2` en la tercera impresión.

---

## Operadores Relacionales

Los operadores relacionales permiten verificar enunciados de igualdad y desigualdad. El tipo de dato resultante es `Boolean`.

| Operador | Enunciado                | Expresión | Función Equivalente                         |
|----------|--------------------------|-----------|---------------------------------------------|
| `==`     | a es igual a b           | `a == b`  | `a?.equals(b) ?: (b === null)`              |
| `!=`     | a es diferente de b      | `a != b`  | `!(a?.equals(b) ?: (b === null))`           |
| `<`      | a es menor que b         | `a < b`   | `a.compareTo(b) < 0`                        |
| `>`      | a es mayor que b         | `a > b`   | `a.compareTo(b) > 0`                        |
| `<=`     | a es menor o igual que b | `a <= b`  | `a.compareTo(b) <= 0`                       |
| `>=`     | a es mayor o igual que b | `a >= b`  | `a.compareTo(b) >= 0`                       |

**Ejemplo:** Usar los operadores relacionales entre los números 17 y 20:

```kotlin
fun main() {
    val a = 17
    val b = 20
    println("$a es igual a $b: ${a == b}")
    println("$a es diferente a $b: ${a != b}")
    println("$a es menor que $b: ${a < b}")
    println("$a es mayor que $b: ${a > b}")
    println("$a es menor o igual que $b: ${a <= b}")
    println("$a es mayor o igual que $b: ${a >= b}")
}
```

Salida:

```
17 es igual a 20: false
17 es diferente a 20: true
17 es menor que 20: true
17 es mayor que 20: false
17 es menor o igual que 20: true
17 es mayor o igual que 20: false
```

---

## Operadores Lógicos

Los operadores lógicos te permiten crear expresiones de lógica proposicional.

| Operador | Descripción                                                    | Expresión |
|----------|----------------------------------------------------------------|-----------|
| `&&`     | Conjunción (and): `true` si `a` y `b` son `true`              | `a && b`  |
| `\|\|`   | Disyunción (or): `true` si `a` o `b` son `true`               | `a \|\| b`|
| `!`      | Negación (not): `false` si `a` es `true`, o viceversa         | `!a`      |

**Ejemplo:** Usar las proposiciones «5 mayor que 0» y «5 es par»:

```kotlin
fun main() {
    val input = 5
    var res: Boolean
    val greaterThanZero = input > 0
    val isEven = input % 2 == 0

    res = greaterThanZero && isEven
    println("Es mayor que cero y par: $res")

    res = greaterThanZero || isEven
    println("Es mayor que cero o par: $res")

    res = greaterThanZero && !isEven
    println("Es mayor que cero e impar: $res")
}
```

---

## Operadores A Nivel De Bits

Kotlin provee funciones para los tipos primitivos enteros que actúan como operadores a nivel de bits.

| Función  | Descripción                                   | Expresión  |
|----------|-----------------------------------------------|------------|
| `and()`  | and bit a bit                                 | `a and b`  |
| `or()`   | or bit a bit                                  | `a or b`   |
| `xor()`  | xor bit a bit                                 | `a xor b`  |
| `inv()`  | not bit a bit                                 | `a.inv()`  |
| `shl()`  | Desplazamiento de bits a la izquierda         | `a shl b`  |
| `shr()`  | Desplazamiento de bits a la derecha           | `a shr b`  |
| `ushr()` | Desplazamiento de bits a la derecha sin signo | `a ushr b` |

**Ejemplo:** Operar a nivel de bits los números enteros 5 y 7:

```kotlin
fun main() {
    val a = 5
    val b = 7
    println("a and b: ${a and b}")
    println("a or b: ${a or b}")
    println("a xor b: ${a xor b}")
    println("a.inv(): ${a.inv()}")
    println("a shl b: ${a shl b}")
    println("a shr b: ${a shr b}")
    println("a ushr b: ${a ushr b}")
}
```

Salida:

```
a and b: 5
a or b: 7
a xor b: 2
a.inv(): -6
a shl b: 640
a shr b: 0
a ushr b: 0
```

---

## ¿Qué Sigue?

Una vez discutido el uso de operadores en Kotlin, el siguiente paso es aprender sobre la **conversión de tipos** en el lenguaje.
