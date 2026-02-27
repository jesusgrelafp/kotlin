# Paquetes en Kotlin

Los paquetes permiten organizar estructuralmente las declaraciones de un programa (clases, funciones, propiedades, objetos, etc.) y controlar su visibilidad entre archivos.

---

## Declaración de paquetes

La declaración va al inicio del archivo fuente con la sentencia `package` seguida del nombre del paquete.

```kotlin
// Archivo: Ghost.kt
package game.ghosts

class Ghost() {
    var x = 0
    var y = 0
    fun move() {
        x++
        y++
    }
}
```

```kotlin
// Archivo: Main.kt
package game.main

fun main() {
    // Bucle del juego
}
```

> En Kotlin **no es obligatorio** hacer coincidir la estructura de directorios con las directivas de paquetes. Sin embargo, en proyectos con interoperabilidad Kotlin-Java es recomendable hacerlo.

---

## Importaciones

Para usar una entidad de otro paquete se usa la palabra clave `import` seguida del nombre completo (paquete + elemento).

### Importación simple

```kotlin
package game.main
import game.ghosts.Ghost

fun main() {
    val ghost1 = Ghost()
}
```

### Importación completamente calificada (sin `import`)

```kotlin
fun main() {
    val ghost1 = game.ghosts.Ghost()
}
```

### Importar todo el contenido de un paquete

```kotlin
import game.ghosts.*  // Importa todas las entidades de ghosts
```

### Importar constantes de una enum class

Si el movimiento de los fantasmas está dictaminado por una `enum class`:

```kotlin
enum class Direction {
    UP, DOWN, LEFT, RIGHT
}
```

Se puede importar directamente sus constantes para evitar el acceso calificado:

```kotlin
import game.ghosts.Ghost.Direction.*

fun move() {
    val randomDirection = Direction.values().random()
    when (randomDirection) {
        UP    -> ++y
        DOWN  -> --y
        LEFT  -> --x
        RIGHT -> ++x
    }
}
```

---

## Resolver conflictos de importación

Cuando dos clases de paquetes distintos tienen el mismo nombre, el compilador exige una importación calificada para la segunda. Para evitarlo, se usa un **alias de importación** con la palabra clave `as`.

**Sin alias (conflicto):**
```kotlin
import game.ghosts.Random

fun main() {
    val randomGhost = Random()
    val randomNumber = kotlin.random.Random.nextInt()  // Calificado a la fuerza
}
```

**Con alias (solución):**
```kotlin
import kotlin.random.Random
import game.ghosts.Random as RandomGhost

fun main() {
    val randomGhost = RandomGhost()
    val randomNumber = Random.nextInt()
}
```

El alias `RandomGhost` desambigua el conflicto entre `game.ghosts.Random` y `kotlin.random.Random`.
