# La Expresión `continue` en Kotlin

`continue` es una expresión de salto que solo se permite dentro de bucles. Su funcionalidad es **saltar las sentencias restantes de la iteración actual** y pasar directamente a la siguiente.

---

## `continue` simple

Se especifica con la palabra reservada `continue` para saltar la iteración actual del **bucle más interno**, si existe anidamiento.

```kotlin
while (loopExpression) {
    /* ... */
    if (ifExpression) {
        continue
    }
    /* Sentencias saltadas cuando se cumple ifExpression */
}
```

**Ejemplo — imprimir los múltiplos de 4 del 1 al 20:**
```kotlin
fun main() {
    for (i in 1..20) {
        if (i % 4 != 0) {
            continue  // Salta los números no divisibles por 4
        }
        println(i)
    }
}
// Salida:
// 4
// 8
// 12
// 16
// 20
```

---

## `continue` etiquetado

Al igual que `break`, `continue` puede usarse en forma etiquetada con la sintaxis `continue@etiqueta`. Esto permite saltar a la siguiente iteración de un **bucle externo específico**, en lugar del más interno.

```kotlin
Loop@ for (i in 1..5) {
    for (j in 1..7) {
        if (ifExpression) {
            continue@Loop  // Salta a la siguiente iteración del bucle Loop
        }
        /* Sentencias saltadas */
    }
    /* Sentencias saltadas también */
}
```

**Ejemplo — imprimir parejas de caracteres de "Compose" y "Kotlin" cuya suma ASCII sea ≤ 180:**
```kotlin
fun main() {
    Loop@ for (d in "Compose") {
        for (k in "Kotlin") {
            if (d.toByte() + k.toByte() > 180) {
                continue@Loop  
            }
            print("($k,$d)")
        }
        println()
    }
}
// Salida: (K,C)(o,C)(K,e)
```

Al anotar el bucle externo con `Loop`, `continue@Loop` salta tanto el `print()` de la pareja como el `println()` exterior, descartando el carácter actual de "Compose" y pasando al siguiente.
