# Conversión De Tipos En Kotlin

En este tutorial verás cómo realizar conversión de tipos en Kotlin de manera explícita. Lo que te permitirá interpretar el contenido de tus variables numéricas de acuerdo al contexto.

---

## Conversión Explícita

Las conversiones explícitas son exigidas por el compilador cuando intentas asignar un tipo de dato numérico que difiere de sus familiares.

**Por ejemplo:** Intentar inicializar una variable `Int` con un tipo `Short`:

```kotlin
val level: Short = 75
val first: Int = level
```

Del ejemplo anterior esperarías una conversión implícita de tipo, ya que `Short` es un entero más pequeño que `Int`. Sin embargo, no es el caso.

En Kotlin los tipos pequeños no son subtipos de los grandes. Por ello el compilador arrojará el siguiente error:

```
Type mismatch: inferred type is Short but Int was expected
```

Para realizar la conversión explícita en Kotlin del escenario anterior, usa el método `toInt()`:

```kotlin
val level: Short = 75
val first: Int = level.toInt()
```

> **Nota:** Adicionalmente, IntelliJ IDEA te ayuda a encontrar la solución si haces click en la bombilla roja y seleccionas **Convert expression to 'Int'**.

---

## Métodos De Conversión

Si exploras la clase `Number` de Kotlin, verás que cada tipo primitivo que herede de ella tiene los siguientes métodos de conversión:

- `toDouble()`
- `toFloat()`
- `toLong()`
- `toInt()`
- `toChar()`
- `toShort()`
- `toByte()`

Debido a la diferencia de tamaño de bits en cada tipo, las conversiones aplicarán truncados o redondeos necesarios cuando el tamaño difiera.

**Ejemplo:** Imprimir el resultado de la conversión explícita de un número entero que exceda el rango de `Short`:

```kotlin
fun main() {
    // Redondeo y truncado en conversiones explícitas
    val measure = 4005215
    println("toShort():${measure.toShort()}")
}
```

La salida de la aplicación será:

```
toShort():7519
```

Al no pertenecer al rango `Short.MIN_VALUE` y `Short.MAX_VALUE`, se usa el truncado con los 16 bits menos significativos del entero.
