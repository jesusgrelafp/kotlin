# Lambdas En Kotlin

Una **función lambda** es un literal de función que puede ser usado como expresión: una función que no está ligada a un identificador y que se puede usar como valor.

---

## Sintaxis de Lambdas

La sintaxis de un literal lambda va al interior de llaves `{}` y se compone de:

- **Lista de parámetros** — opcional; cada parámetro es una declaración de variable
- **Operador de flecha `->`** — se omite si no hay lista de parámetros
- **Cuerpo del lambda** — sentencias tras el operador de flecha

```kotlin
// Función regular
fun sumarDos(s: Int) = s + 2

// Equivalente como lambda
{s: Int -> s + 2}
```

---

## Lambda Como Argumento

Las lambdas permiten pasar funciones como argumentos de otras funciones (funciones de orden superior).

```kotlin
fun main() {
    val kCount = "kotlin.kts".count({ char: Char -> char == 'k' })
    print("Total 'k': $eCount")
}
// Total 'k': 2
```

---

## Simplificaciones de Sintaxis

### Omitir paréntesis

Si el lambda es el último argumento, las llaves pueden ir fuera del paréntesis:

```kotlin
val kCount = "kotlin.kts".count() { char: Char -> char == 'k' }
```

Si los paréntesis quedan vacíos, se omiten completamente:

```kotlin
val kCount = "kotlin.kts".count { char: Char -> char == 'k' }
```

### Omitir el tipo del parámetro

Si el compilador puede inferir el tipo, se puede omitir:

```kotlin
val kCount = "kotlin.kts".count { char -> char == 'k' }
```

### El identificador `it`

Cuando el lambda tiene un único argumento y no se necesita renombrarlo, se puede usar `it`:

```kotlin
val kCount = "kotlin.kts".count { it == 'k' }
```

---

## Lambdas con Múltiples Líneas

El cuerpo del lambda puede tener varias líneas. La **última expresión** es el valor de retorno:

```kotlin
fun main() {
    val kCount = "kotlin.kts".count {
        println("Carácter $it")
        it == 'k'
    }
    print("Total 'k': $kCount")
}
// Carácter k
// Carácter o
// Carácter t
// Carácter l
// ...
// Total 'k': 2
```
