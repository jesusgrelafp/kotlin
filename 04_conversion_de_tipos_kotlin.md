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

### ¿Qué son los 16 bits menos significativos?

Los bits menos significativos son los que están más a la derecha en la representación binaria de un número (los de menor peso), mientras que los más significativos están más a la izquierda (mayor peso). Al truncar de `Int` (32 bits) a `Short` (16 bits), simplemente se descartan los 16 bits más significativos (la mitad izquierda) y se conservan los 16 bits menos significativos (la mitad derecha), reinterpretándolos como un `Short` completo, incluyendo su propio bit de signo.

**Ejemplo con `measure = 4005215`:**

En binario (32 bits):

```
0000 0000 0011 1101 0001 1101 0101 1111
```

Se descartan los 16 bits más significativos (izquierda):

```
0000 0000 0011 1101
```

Y se conservan los 16 bits menos significativos (derecha), que pasan a formar el `Short` resultante:

```
0001 1101 0101 1111
```

Ese valor en decimal es **7519**, que coincide con el resultado de `measure.toShort()`. No se trata de un redondeo, sino de un corte directo de la mitad baja del número original.
