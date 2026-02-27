# Tipos Primitivos En Kotlin

Este tutorial te ayudará a explorar los tipos primitivos en Kotlin: enteros, flotantes, booleanos y caracteres. Con el fin de determinar el contenido más adecuado de tus variables y saber sobre sus limitaciones.

---

## Números Enteros

Los siguientes son los tipos que representan números enteros en Kotlin con sus rangos.

| Tipo    | Tamaño en bits | Límite inferior | Límite superior |
|---------|----------------|-----------------|-----------------|
| `Byte`  | 8              | -128            | 127             |
| `Short` | 16             | -32768          | 32767           |
| `Int`   | 32             | -2³¹            | 2³¹-1           |
| `Long`  | 64             | -2⁶³            | 2⁶³-1           |

Al declarar una variable entera, el compilador de Kotlin inferirá su tipo como `Int` si el valor está en su rango. Por lo que si deseas usar un tipo de tamaño menor, explícitamente debes definirlo.

En la inferencia del tipo `Long` usa el sufijo literal `L` para dejarlo claro.

```kotlin
// 1. Tipos enteros
val level: Byte = 50
val health: Short = 150
val missionPoints: Int = 40000
val experience: Long = 45121365412
val monstersExecuted = 9990001522L // La 'L' especifica al tipo Long
```

### Literales Constantes Para Binarios Y Hexadecimales

Si deseas cambiar el sistema numérico de los valores enteros a hexadecimal o binario, usa los literales `0b` y `0x`. El valor que escribas luego de estos prefijos será interpretado en dicho sistema numérico.

En el siguiente ejemplo tienes un pequeño programa que declara dos enteros en ambos sistemas:

```kotlin
fun main() {
    // Literales binarios y hexadecimales
    val bitmapLocation = 0b00100001 // Literal binario 0b ó 0B
    val chestColor = 0xCCC          // Literal hexadecimal 0x ó 0X

    println(bitmapLocation)
    println(chestColor)
}
```

Al correrlo obtendrás la representación en el sistema decimal:

```
33
3276
```

---

## Números Reales

Los números de punto flotante, al igual que en Java, se representan por `Float` y `Double`: precisión simple y doble.

| Tipo     | Tamaño en bits | Bits significativos | Bits del exponente | Dígitos decimales |
|----------|----------------|---------------------|--------------------|-------------------|
| `Float`  | 32             | 24                  | 8                  | 6-7               |
| `Double` | 64             | 53                  | 11                 | 15-16             |

El compilador de Kotlin inferirá el tipo `Double` si no especificas el tipo. En el caso de `Float`, usa los literales constantes `f` o `F` como sufijo para la declaración o inferencia de tipo.

```kotlin
val attackSpeed: Float = 0.5f
val dodgeChance: Double = 0.2
```

En una declaración y asignación en línea de un tipo `Float`, la omisión del literal `f` hará que el compilador arroje este error:

```
The floating-point literal does not conform to the expected type Float
```

### Literales Constantes Para Números Reales

Un literal flotante en Kotlin se puede componer de la parte entera de la base, el punto decimal, la fracción y el exponente base 10 (la letra `e` o `E`, junto a una parte entera decimal).

Es posible omitir la parte entera, al igual que la fracción en conjunto con el punto.

En el siguiente ejemplo puedes ver algunas variaciones con literales reales:

```kotlin
fun main() {
    // Literales reales
    val exp1 = 3.211e2
    val exp2 = .0001e10
    val exp3 = 48e5
    val exp4 = 10e-4

    println(exp1)
    println(exp2)
    println(exp3)
    println(exp4)
}
```

Al correr el programa obtendrás el siguiente resultado:

```
321.1
1000000.0
4800000.0
0.001
```

---

## Caracteres

Un carácter es el almacenamiento de un valor Unicode en una variable tipo `Char`. Su asignación se realiza poniendo cualquier símbolo entre comillas simples (`'`).

```kotlin
fun main() {
    val response: Char = 'Y'
    println(response)
}
```

Estos pueden contener una marca de escape representada por el backslash `\`, permitiéndote acceder a los siguientes caracteres de escape.

### Caracteres De Escape

Un literal de carácter puede contener los siguientes símbolos de escape simple:

| Secuencia | Descripción                                        |
|-----------|----------------------------------------------------|
| `\t`      | Tabulación                                         |
| `\b`      | Retroceso                                          |
| `\r`      | Retorno de carro                                   |
| `\n`      | Salto de línea                                     |
| `\'`      | Apostrofe                                          |
| `\"`      | Comilla doble                                      |
| `\\`      | Backslash                                          |
| `\$`      | Símbolo de dólar                                   |
| `\uXXXX`  | Símbolo Unicode con 4 dígitos hexadecimales        |

**Por ejemplo:** Usar saltos de línea en un mensaje con tres palabras.

```kotlin
fun main() {
    print("Uno\nDos\nTres")
}
```

La secuencia de escape `\n` te permite mostrar el string así:

```
Uno
Dos
Tres
```

---

## Booleanos

En el caso de los valores booleanos, usa el tipo `Boolean`. Tendrás las palabras clave `true` para verdadero y `false` para representar falso.

```kotlin
val globalMapEnable: Boolean = true
```

---

## ¿Qué Sigue?

Con este tutorial te has introducido al uso de tipos primitivos en Kotlin. Ahora podrás determinar el tipo adecuado para tus datos básicos. Lo siguiente es aprender a usar los **operadores** que el lenguaje te brinda.
