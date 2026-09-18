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

**Combinar condiciones con `&&`, `||` y `!`:**

```kotlin
fun main() {
    val level = 12
    val hasStaff = true
    if (level >= 10 && hasStaff) {
        println("Puedes lanzar el hechizo")
    } else if (level >= 10 || hasStaff) {
        println("Casi lo consigues")
    } else if (!hasStaff) {
        println("Te falta el báculo")
    }
}
// Salida: Puedes lanzar el hechizo
```

> Usa paréntesis para dejar clara la precedencia cuando combines `&&` y `||` en la misma condición, ya que `&&` se evalúa antes que `||`.

**`if` de una sola línea:** si el cuerpo de una rama es una única instrucción, las llaves `{}` son opcionales.

```kotlin
fun main() {
    val level = 12
    if (level >= 45) println("Aprendiste Acrobacia")
    else println("Se requiere nivel 45. Nivel actual $level")
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

> **Kotlin no tiene operador ternario.** Si vienes de Java o C, buscarás `condicion ? a : b`; en Kotlin el equivalente directo es `if (condicion) a else b`, tal como se muestra arriba.

---

## If y else en expresión

Cuando se usa `if` como expresión, el `else` es **obligatorio**. Sin él, el compilador lanza el error:

```
'if' must have both main and 'else' branches if used as an expression
```

**Esto solo aplica cuando `if` se usa como expresión.** Como sentencia (sin usar su resultado), el `else` sigue siendo opcional, igual que vimos con `when`:

```kotlin
fun main() {
    val level = 50
    if (level >= 45) {   // como sentencia, no exige 'else'
        println("Aprendiste Acrobacia")
    }
    println("Fin")
}
// Salida:
// Aprendiste Acrobacia
// Fin
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

> **Advertencia:** Si se omite el valor final en una rama (por ejemplo, se elimina el `6` del `else`, dejando solo `println("...")`), esa rama pasa a valer `Unit`. El compilador infiere entonces el tipo de `cardAttack` como el supertipo común de `Int` y `Unit`, que es `Any` — no da ningún error, así que el fallo pasa desapercibido. Al ejecutar, como se toma la rama `else`, `cardAttack` termina valiendo `Unit` en tiempo de ejecución:

```
// Sin el valor 6 en else:
...
Ataque:kotlin.Unit
```

> Para detectar este error en tiempo de compilación en vez de en tiempo de ejecución, declara la variable explícitamente: `val cardAttack: Int`. Al asignarle un valor de tipo `Any` (o `Unit`), el compilador lanzará `Type mismatch: inferred type is Any but Int was expected`, revelando el fallo de inmediato.

---

## Smart Cast dentro de un `if`

Cuando compruebas el tipo de una variable con `is` dentro de la condición de un `if`, Kotlin aplica **Smart Cast** automáticamente: dentro de esa rama, la variable ya se trata como el tipo comprobado, sin necesidad de castear manualmente.

```kotlin
fun describir(x: Any) {
    if (x is String) {
        // Aquí 'x' ya se trata como String, sin cast explícito
        println("Es un String de longitud ${x.length}")
    } else {
        println("No es un String")
    }
}
// describir("Hola") → Salida: Es un String de longitud 4
```

---

## `if` anidado vs. `else if` encadenado

Anidar un `if` dentro de la rama `else` de otro (`else { if (...) { ... } }`) y usar `else if` en cadena producen el mismo resultado, pero `else if` es preferible porque evita el anidamiento creciente y mejora la legibilidad.

```kotlin
// Anidado (evitar)
fun clasificarAnidado(nota: Int) {
    if (nota >= 9) {
        println("Sobresaliente")
    } else {
        if (nota >= 7) {
            println("Notable")
        } else {
            println("Aprobado o menos")
        }
    }
}

// else if encadenado (preferible)
fun clasificarEncadenado(nota: Int) {
    if (nota >= 9) {
        println("Sobresaliente")
    } else if (nota >= 7) {
        println("Notable")
    } else {
        println("Aprobado o menos")
    }
}
```

---

## Relación con el operador Elvis `?:`

Un patrón muy habitual es usar `if` para dar un valor por defecto cuando algo es `null`:

```kotlin
val a: String? = null
val x = if (a != null) a else "valor por defecto"
```

Kotlin ofrece una forma abreviada de este patrón concreto: el operador Elvis `?:`.

```kotlin
val x = a ?: "valor por defecto"
```

> El operador Elvis se explica en detalle en la página dedicada a tipos nulos (*nullability*).
