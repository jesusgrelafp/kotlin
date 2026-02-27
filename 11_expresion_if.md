# La Expresión `if` en Kotlin

La expresión `if` evalúa una condición booleana para bifurcar el flujo de ejecución de tu programa.

---

## If como sentencia

La estructura de control `if` conduce el flujo de tu aplicación basándose en la evaluación de una expresión que produzca un resultado booleano.

```kotlin
if (expresion) {
    // Acciones si se cumple
} else if (expresion2) {
    // Acciones si se cumple
} else {
    // Acciones si nada se cumple
}
```

Usa `else` para procesar el resultado adverso y `else if` para agregar evaluaciones adicionales.

**Ejemplo — verificar si el jugador puede aprender una habilidad:**
```kotlin
fun main() {
    val level = 12
    if (level >= 45) {
        println("Aprendiste Acrobacia")
    } else {
        println("Se requiere nivel 45. Nivel actual $level")
    }
}
// Salida: Se requiere nivel 45. Nivel actual 12
```

---

## If como expresión

A diferencia de Java, `if` es una **expresión primaria** en Kotlin: al evaluar una condición produce un valor que puede usarse en el retorno de una función o en la asignación a una variable.

**Forma tradicional (sentencia):**
```kotlin
fun main() {
    val enemyHeroHealth = 16
    val cardAttack: Int
    if (enemyHeroHealth <= 15) {
        cardAttack = 9
    } else {
        cardAttack = 6
    }
    println("Ataque:$cardAttack")
}
```

**Forma compacta (expresión):**
```kotlin
val cardAttack = if (enemyHeroHealth <= 15) 9 else 6
println("Ataque:$cardAttack")
// Salida: Ataque:6
```

---

## If y else en expresión

Cuando se usa `if` como expresión, el `else` es **obligatorio**. Sin él, el compilador lanza el error:

```
'if' must have both main and 'else' branches if used as an expression
```

---

## Usar ramas como bloques

Las ramas `if` y `else` pueden convertirse en bloques usando llaves, permitiendo múltiples líneas. La **última expresión** del bloque es el valor resultante.

```kotlin
fun main() {
    val enemyHeroHealth = 16
    val cardAttack = if (enemyHeroHealth <= 15) {
        println("Grrrrrrrr!!")
        9
    } else {
        println("...")
        6
    }
    println("Ataque:$cardAttack")
}
// Salida:
// ...
// Ataque:6
```

> **Advertencia:** Si se omite el valor final en una rama (por ejemplo, se elimina el `6` del `else`), el compilador infiere el tipo como `Any`, ya que `println()` retorna `Unit`. Para garantizar el tipo entero, declara la variable explícitamente: `val cardAttack: Int`.

```
// Sin el valor 6 en else:
Ataque:kotlin.Unit
```
