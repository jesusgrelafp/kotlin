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

También se puede negar la comprobación con `!in`.

```kotlin
fun main() {
    val input = 150
    when (input) {
        !in 1..99 -> print("$input está fuera de [1..99]")
        else      -> print("$input está dentro de [1..99]")
    }
}
// Salida: 150 está fuera de [1..99]
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

## Combinar condiciones de distinto tipo en una misma rama

No solo se pueden agrupar literales; también se pueden mezclar comprobaciones de tipo, rangos y valores en la misma entrada separándolos con comas.

```kotlin
fun describir(x: Any) = when (x) {
    is Int, is Long -> "Es un número entero"
    in 1.0..10.0    -> "Es un decimal entre 1 y 10"
    "", " "         -> "Está vacío o es un espacio"
    else            -> "Otro tipo"
}
```

---

## Comprobar `null` en una rama

Si el sujeto es de tipo *nullable*, se puede comprobar el caso `null` como una condición más.

```kotlin
fun main() {
    val texto: String? = null
    when (texto) {
        null -> print("No hay texto")
        else -> print("Longitud: ${texto.length}")
    }
}
// Salida: No hay texto
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

No hace falta que las condiciones sean comparaciones directas: cualquier expresión que devuelva `Boolean` es válida, incluidas llamadas a funciones.

```kotlin
fun esPar(n: Int) = n % 2 == 0

fun main() {
    val numero = 8
    when {
        esPar(numero) -> print("Es par")
        numero < 0    -> print("Es negativo")
        else          -> print("Es impar y positivo")
    }
}
// Salida: Es par
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

**Sentencia vs. expresión:** esta obligación solo aplica cuando `when` se usa como **expresión** (su resultado se asigna o se retorna). Como **sentencia** (sin usar su resultado), un `when` no exhaustivo es perfectamente válido: si ninguna rama coincide, simplemente no se ejecuta nada y no hay error de compilación.

```kotlin
fun main() {
    val nota = 9
    when (nota) {   // como sentencia, no exige 'else'
        1 -> print("Insuficiente")
        2 -> print("Deficiente")
    }
    print("Fin")
}
// Salida: Fin   (ninguna rama coincide, pero compila y ejecuta sin error)
```

Si una rama necesita más de una instrucción, se agrupa con llaves `{}`. Cuando `when` se usa como expresión, el valor de la rama es el resultado de la **última línea** del bloque.

```kotlin
val nota = 7
val comentario = when {
    nota >= 5 -> {
        val extra = "¡Bien hecho!"
        "Aprobado. $extra"   // esta es la línea que se devuelve
    }
    else -> "Suspenso"
}
```

---

## `when` con `enum class`

Cuando el sujeto es un `enum`, si se cubren todos los valores posibles, el compilador no exige `else`.

```kotlin
enum class Direccion { NORTE, SUR, ESTE, OESTE }

fun main() {
    val d = Direccion.ESTE
    val mensaje = when (d) {
        Direccion.NORTE -> "Vas hacia arriba"
        Direccion.SUR   -> "Vas hacia abajo"
        Direccion.ESTE  -> "Vas hacia la derecha"
        Direccion.OESTE -> "Vas hacia la izquierda"
    }
    print(mensaje)
}
// Salida: Vas hacia la derecha
```

---

## `when` con `sealed class` (exhaustividad real)

El caso más claro de *exhaustive when*: al usar una `sealed class`, el compilador conoce todos los subtipos posibles y exige que estén todos cubiertos, sin necesidad de `else`. Si añades un nuevo subtipo y olvidas su rama, el código **no compila**, lo que ayuda a detectar errores pronto.

```kotlin
sealed class Resultado
class Exito(val datos: String) : Resultado()
class Error(val mensaje: String) : Resultado()
object Cargando : Resultado()

fun procesar(r: Resultado) = when (r) {
    is Exito -> "Datos: ${r.datos}"
    is Error -> "Error: ${r.mensaje}"
    Cargando -> "Esperando..."
    // No hace falta 'else': todos los subtipos están cubiertos
}
```

---

## Guard conditions: condición extra sobre `is` (Kotlin 2.1+)

Desde Kotlin 2.1 se puede añadir una condición booleana adicional a una rama de comprobación de tipo, usando `is Tipo if condicion ->`. Esto permite distinguir subtipos con matices sin anidar un `if` dentro del cuerpo de la rama.

```kotlin
sealed class Figura
class Circulo(val radio: Double) : Figura()
class Rectangulo(val ancho: Double, val alto: Double) : Figura()

fun describir(f: Figura) = when (f) {
    is Circulo if f.radio > 10 -> "Círculo grande"
    is Circulo                 -> "Círculo pequeño"
    is Rectangulo               -> "Rectángulo"
}
```

> Requiere una versión de Kotlin reciente (2.1 o superior); comprueba la versión del compilador antes de usarlo en el aula.

---

## Sin fall-through (diferencia clave con Java)

A diferencia del `switch` de Java, en Kotlin **cada rama es independiente**: si una condición se cumple, se ejecuta solo esa rama y se sale de la expresión. No existe el arrastre entre ramas que obliga a usar `break` en Java, ni siquiera si dos condiciones podrían cumplirse a la vez — solo se evalúa la primera que coincide, en orden.

```kotlin
val n = 2
when (n) {
    1, 2 -> print("Uno o dos")
    2, 3 -> print("Dos o tres")   // nunca se ejecuta si n=2, aunque también encajaría
}
// Salida: Uno o dos
```
