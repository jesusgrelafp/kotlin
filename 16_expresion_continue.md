# La Expresión `continue` en Kotlin

`continue` es una expresión de salto que solo se permite dentro de bucles. Su funcionalidad es **omitir las sentencias restantes de la iteración actual** y pasar directamente a la siguiente iteración.

---

## `continue` simple

Se especifica con la palabra reservada `continue`. Cuando existen bucles anidados, afecta al **bucle más interno** que contiene la sentencia.

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

Al igual que `break`, `continue` puede utilizarse en forma etiquetada con la sintaxis `continue@etiqueta`. Esto permite indicar explícitamente **el bucle etiquetado cuya siguiente iteración debe iniciarse**.

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

**Ejemplo — omitir una fila completa en una tabla de coordenadas:**

```kotlin
fun main() {
    FilaLoop@ for (i in 1..3) {
        for (j in 1..3) {
            // Si estamos en la fila 2, saltamos por completo al siguiente ciclo del bucle externo
            if (i == 2) {
                continue@FilaLoop
            }
            println("Coordenada: ($i, $j)")
        }
    }
}

// Salida:

// Coordenada: (1, 1)
// Coordenada: (1, 2)
// Coordenada: (1, 3)
// Coordenada: (3, 1)
// Coordenada: (3, 2)
// Coordenada: (3, 3)
```

Al anotar el bucle externo con `FilaLoop`, `continue@FilaLoop` hace que cuando `i == 2` se descarte toda la fila (evitando imprimir `(2,1)`, `(2,2)` y `(2,3)`) y el programa salte directamente a procesar la fila `3`.
