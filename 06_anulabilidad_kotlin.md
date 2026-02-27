# Anulabilidad En Kotlin

En este tutorial aprenderás sobre anulabilidad en Kotlin para usar tipos anulables y no anulables.

---

## Tipos Anulables En Kotlin

Con el mismo marco de las variables de solo lectura y mutables, Kotlin evita que tus tipos acepten el literal constante `null` (ausencia de valor) como regla general.

Si necesitas un tipo que acepte nulos, defínelo como anulable, ubicando un signo de interrogación de cierre (`?`) al final del tipo.

**Por ejemplo:**

```kotlin
fun main() {
    var noAceptaNull: String
    noAceptaNull = null  // Error

    var aceptaNull: String?
    aceptaNull = null   // OK
}
```

La variable `noAceptaNull` es de tipo no anulable, por lo que si intentas asignarle `null` tendrás el error:

```
Null can not be a value of a non-null type String
```

Por el otro lado, `aceptaNull` que ha sido declarado anulable con `String?`, sí permite la asignación del literal.

---

## Inferencia De Tipos No Anulables

El compilador de Kotlin tiene la capacidad de inferir si el tipo será anulable o no, dependiendo del contexto.

Si inicializas una variable con un valor determinado y no declaras el tipo, implícitamente el tipo será no anulable:

```kotlin
// Inferencia
var cardName = "Animal compañero" // :String
// Sucesos...
cardName = null // Error
```

---

## Verificar Igualdad A null

Con el fin de evitar que el flujo de tu programa se vea afectado por la aparición de un valor nulo, usa la expresión `if` para comprobar su existencia.

**Por ejemplo:** Se requiere crear una función que imprima una lista de bestias de un juego. Es posible que no existan valores todavía en la base de datos.

```kotlin
fun showBeastsList(beasts: List<String>?) {
    if (beasts != null && beasts.isNotEmpty()) {
        beasts.forEach { println(it) }
    }
}
```

La solución usa un parámetro anulable de tipo `List<String>?`. Usamos el operador `!=` para especificar la diferencia de `null`.

Debido a que el operador `&&` realiza una operación de cortocircuito (omite las siguientes evaluaciones si la primera expresión es `false`), el compilador infiere que al realizar `beasts.isNotEmpty()`, `beasts` no será nulo y es seguro invocar al método.

---

## Operador De Acceso Seguro

Otra opción para protegerte contra nulidad es usar el **operador de acceso seguro**. Este se compone del signo de pregunta y un punto (`?.`) para el acceso.

```kotlin
cliente?.nombre // Si el [cliente] no es null, acceder a [nombre]
```

Si el miembro existe, entonces se retorna el contenido; de lo contrario se obtendrá `null` del recibidor.

### Asignación De Tipos Anulables

El resultado de variables anulables solo puede ser asignado a otras variables anulables.

```kotlin
val password: String? = null
// Obtener password...
val passwordSize = password?.length
```

En el ejemplo anterior, el compilador de Kotlin deduce el tipo como `Int?` con el fin de soportar un posible valor `null`.

---

## El Operador Elvis

El operador Elvis retorna el primer operando (`a`), si dicho operando es evaluado como `true`; de lo contrario evalúa y retorna su segundo operando (`b`).

```kotlin
c = a ?: b
```

En Kotlin, este operador se reduce para comprobar expresiones anulables. Si el operando de la izquierda es `null` entonces retornará el de la derecha:

```kotlin
val passwordSize = if (password != null) password.length else 0
// Esto equivale a:
val passwordSize = password?.length ?: 0
```

Si `a` no es `null`, entonces retornar `length`; de lo contrario `passwordSize` sería igual a cero.

---

## Operador !!

También es posible manejar la anulabilidad en Kotlin usando el **operador de aserción not null** (`!!`) o *not-null assertion operator*.

Este convierte cualquier valor a un tipo no anulable. Si no se puede, se lanza una excepción del tipo `NullPointerException`.

**Por ejemplo**, el siguiente código produce una NPE debido a que el contador nunca se reasigna con un valor entero:

```kotlin
fun main() {
    val counter: Int? = null
    counter!!.dec() // NPE
    print(counter)
}
```

Al intentar usar `dec()` para disminuir el valor, la excepción se disparará.
