# Variables En Kotlin

En este tutorial aprenderás a declarar y usar variables en Kotlin para almacenar datos en memoria. Verás que existen variables de solo lectura (read-only) y mutables, además de la inferencia que el compilador de Kotlin realiza.

---

## ¿Qué Es Una Variable?

Una variable es una posición en memoria que contiene un valor asociado a un nombre. Su contenido se especifica por el tipo de dato que le especifiques al compilador.

En Kotlin el cambio del valor de una variable a lo largo del flujo del programa, depende del identificador usado como verás a continuación.

---

## Variables De Solo Lectura

Una variable de solo lectura (read-only) es una variable que no puede ser reasignada.

Para declararlas, usa la palabra reservada `val` y especifica su tipo de dato a su derecha con dos puntos (`:`).

```kotlin
val xPos: Int = 1 // Asignación junto a declaración
val yPos: Int     // Declaración
yPos = 5          // Asignación
```

El valor que les asignes en su declaración no podrás cambiarlo posteriormente. Si lo intentas el compilador te mostrará este error:

```
Val cannot be reassigned
```

En IntelliJ IDEA el compilador te lo advertirá justo en la escritura.

Puedes interpretar las variables de solo lectura como la correspondencia al modificador `final` de Java.

### Errores comunes

Si no defines el tipo ni asignas un valor a la variable en la declaración, obtendrás este error:

```
This variable must either have a type annotation or be initialized
```

En el caso de que cuentes con declaración con tipo, pero intentes usarla en una sentencia sin haberla inicializado:

```kotlin
val enemyHealth: Int

println(enemyHealth)
```

El error que te arrojará sería este:

```
Variable 'enemyHealth' must be initialized
```

---

## Variables Mutables

Este tipo de variables las declaras con la palabra reservada `var`. Te permiten modificar su valor cuando lo desees.

Si haces que la variable del ejemplo de la sección anterior sea mutable, ya no tendrás el error y se asignará el nuevo valor:

```kotlin
fun main() {
    // Variables mutables
    var xPos: Int = 1
    val yPos: Int = 5
    xPos = 2
    println("Coordenada actual del jugador: ($xPos, $yPos)")
}
```

Si corres la aplicación obtendrás como salida:

```
Coordenada actual del jugador: (2, 5)
```

> **Nota:** El operador `$` que ves al interior del string de `println()` permite insertar el valor de la variable referenciada. Esto se verá más en detalle en el tutorial de Strings.

---

## Inferencia De Tipos

En Kotlin puedes omitir los tipos de las variables en su declaración, ya que el compilador puede inferirlos de acuerdo al valor de su asignación.

```kotlin
val playerName = "Oliver"  // Se infiere :String
val playerHealth = 75      // Se infiere :Int
val playerLucky = 0.2      // Se infiere :Double
```

Pero que el compilador te apoye con la asignación del tipo, no significa que nunca los especifiques o que no respetes el contenido.

Por ejemplo, intentar asignar un tipo de naturaleza distinta:

```kotlin
var playerSpeed = 12
playerSpeed = "Lento" // Error
```

El compilador arrojará el siguiente error, ya que estás asignando una cadena a lo que el compilador había inferido como entero:

```
Type mismatch: inferred type is String but Int was expected
```

En la medida que puedas, busca usar `val` en vez de `var`, ya que facilitará el enfoque funcional en tu aplicación, el cual es más fácil de entender y soportar.

---

## ¿Qué Sigue?

Ya aprendiste sobre el tipo de variables en Kotlin y cómo el compilador infiere tipos por ti. Ahora podrás ver los **tipos primitivos** que existen para declarar variables.
