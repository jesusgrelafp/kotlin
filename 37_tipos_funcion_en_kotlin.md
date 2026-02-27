# Tipos Función En Kotlin

El **tipo función** (FT) es el tipo de una variable o parámetro al que se le ha asignado (o puede asignar) una función. También es el tipo para un argumento o resultado de retorno de una función de orden superior.

Esta capacidad de usar funciones como valores es posible gracias a la interfaz `kotlin.Function` de Kotlin.

---

## Sintaxis de Tipos Función

La forma base se compone de los tipos de los argumentos entre paréntesis, el operador `->` y el tipo de retorno:

```
FT(A1, ..., An) -> R
```

Ejemplos:

```kotlin
(String, String) -> String  // dos String como entrada, un String como salida
(Int) -> Unit               // un Int como entrada, sin retorno particular
() -> Double                // sin parámetros, retorna un Double
```

---

## Almacenar Lambda en Variable

Las instancias de tipo función pueden almacenarse en variables. La forma más común es usar lambdas.

```kotlin
// Con inferencia de tipo (el compilador deduce el tipo función)
val nombreConFormato = { nombre: String, apellido: String -> "$nombre $apellido" }

// Con tipo explícito
val nombreConFormato: (String, String) -> String = { nombre: String, apellido: String -> "$nombre $apellido" }
```

---

## Invocar una Instancia de Tipo Función

Se puede llamar como una función normal o usando el operador `invoke()`:

```kotlin
fun main() {
    val nombreCompleto = { nombre: String, apellido: String -> "$nombre $apellido" }
    println(nombreCompleto("Laura", "Min"))           // llamada normal
    println(nombreCompleto.invoke("Carlos", "Xhan"))  // con invoke()
}
// Laura Min
// Carlos Xhan
```

Almacenar lambdas en variables es útil para posponer su ejecución, componer lambdas o usarlas en funciones de orden superior.

---

## Tipos Función Anulables

Los tipos función también pueden ser anulables. La sintaxis es envolver el tipo entre paréntesis y añadir `?`:

```kotlin
(()->Int)?        // tipo función anulable sin parámetros
((Int) -> Int)?   // tipo función anulable con un parámetro Int
```

### Ejemplo

```kotlin
fun main() {
    val payment = 10
    val getStars: ((Int) -> Int)? =
        if (payment > 0) { cost: Int -> cost * 10 } else null

    // Verificación explícita antes de invocar
    if (getStars != null) {
        print("Estrellas recibidas: ${getStars(10)}")
    }
}
// Estrellas recibidas: 100
```

Si `payment` fuera `0`, `getStars` sería `null` y no se ejecutaría nada.

### Llamada con operador de acceso seguro

```kotlin
getStars?.invoke(10)
```

Se usa `invoke()` para habilitar el operador `?.` sobre el tipo función anulable.
