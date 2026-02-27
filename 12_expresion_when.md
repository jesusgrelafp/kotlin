# La Expresión `when` en Kotlin

La expresión `when` permite comparar el valor de un argumento (sujeto) contra una lista de entradas con sus respectivas condiciones. Es análoga al `switch` de Java, pero más potente y sin necesidad de `break`.

Las condiciones de cada entrada pueden ser: expresiones, comprobaciones de rangos o comprobaciones de tipos.

---

## `when` como sentencia

```kotlin
when (sujeto) {
    condicion1 -> cuerpo1
    condicion2 -> cuerpo2
    else       -> cuerpoDefault
}
```

**Ejemplo — procesar entrada de usuario:**
```kotlin
fun main() {
    val input = 'y'
    when (input) {
        'y'  -> print("Continuando...")
        'n'  -> print("Cerrando...")
        else -> print("Entrada inválida")
    }
}
// Salida: Continuando...
```

---

## Múltiples valores en una entrada

Se pueden agrupar varios valores en una misma condición separándolos con comas.

```kotlin
fun main() {
    val input = 2
    when (input) {
        1, 2, 3 -> print("Te toca turno nocturno")
        4, 5, 6 -> print("Te toca turno diurno")
    }
}
// Salida: Te toca turno nocturno
```

---

## Usar expresiones como condición

Además de literales, se pueden usar expresiones como conjunciones, comparaciones, operaciones, instanciaciones, etc.

```kotlin
fun main() {
    val input = 100
    when (input) {
        Char.MAX_VALUE.toInt() -> print("Límite superior")
        Char.MIN_VALUE.toInt() -> print("Límite inferior")
        else                   -> print("No es ninguno de los límites")
    }
}
// Salida: No es ninguno de los límites
```

---

## Rangos en `when`

Se usa el operador `in` (o `!in`) para comprobar si el valor pertenece a un rango.

```kotlin
fun main() {
    print("Ingresa el número:")
    val input = readLine()!!.toInt()
    when (input) {
        in 1..49  -> print("$input pertenece a [1..49]")
        in 50..99 -> print("$input pertenece a [50..99]")
        else      -> print("Fuera de los rangos contemplados")
    }
}
// Con input = 40 → Salida: 40 pertenece a [1..49]
```

---

## Comparar tipos con `when`

Se usa el operador `is` para comprobar el tipo. Kotlin aplica **Smart Cast** automáticamente: no es necesario castear la variable tras la comprobación.

```kotlin
fun main() {
    val formResponse: Any = "12"
    when (formResponse) {
        is Int    -> {
            val times = formResponse * 100
            print("Respuesta Entera:$times")
        }
        is String -> {
            val times = formResponse.toInt() * 100
            print("Respuesta String:$times")
        }
    }
}
// Salida: Respuesta String:1200
```

---

## Usar `when` como `if` (sin argumento)

Si no se necesita un valor de comparación, `when` puede escribirse sin argumento para comprobar expresiones booleanas.

```kotlin
fun main() {
    val a = -5
    when {
        a > 0  -> print("Es positivo")
        a == 0 -> print("Es cero")
        else   -> print("Es negativo")
    }
}
```

---

## Declaración de variable en el sujeto

Es posible declarar e inicializar una variable directamente en el argumento del `when`, quedando disponible dentro de su bloque.

```kotlin
fun main() {
    val playerLucky = 0.2
    val bonus = 0.3
    when (val damage: Double = playerLucky + bonus) {
        in 0.0..0.3 -> print("Daño recibido:${damage * 10}")
        in 0.3..0.6 -> print("Daño recibido:${damage * 20}")
        in 0.6..1.0 -> print("Daño recibido:${damage * 30}")
    }
}
// Salida: Daño recibido:10.0
```

---

## `when` como expresión

Al igual que `if`, `when` puede usarse como expresión para retornos y asignaciones.

```kotlin
fun main() {
    val markNumber = 4
    val markText = when (markNumber) {
        1    -> "Insuficiente"
        2    -> "Deficiente"
        3    -> "Aceptable"
        4    -> "Sobresaliente"
        5    -> "Excelente"
        else -> "No permitido"
    }
    print("La calificación es: $markText")
}
// Salida: La calificación es: Sobresaliente
```

> El `else` es obligatorio como expresión, a menos que las ramas cubran todas las posibilidades posibles (*exhaustive when expression*).
