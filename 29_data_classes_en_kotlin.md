# Data Classes En Kotlin

En este tutorial se explica cómo usar data classes en Kotlin para facilitar el uso de clases cuya responsabilidad es solo almacenar valores.

---

## El Modificador `data`

El modificador `data` facilita la creación de clases cuyo propósito es **solo almacenar valores**. Al marcarlo, el compilador autogenera los siguientes métodos basándose en las propiedades del constructor primario:

- `equals()`
- `hashCode()`
- `copy()`
- `toString()`
- Métodos `componentN()` por cada propiedad en orden de declaración

```kotlin
data class Rock(
    val width: Int,
    val height: Int,
    val depth: Int,
    val variation: Int = 1
)
```

---

## Excluir Propiedades

El compilador solo usa las propiedades del **constructor primario** para autogenerar los métodos. Para excluir una propiedad, se declara en el cuerpo de la clase:

```kotlin
data class Rock(
    val width: Int,
    val height: Int,
    val depth: Int,
    val variation: Int = 1
) {
    var deformationFactor = 0.0  // No participa en equals, hashCode, toString, copy
}
```

---

## Representación String (`toString`)

El método `toString()` autogenerado retorna una representación con el formato:

```
Clase(propiedad1=valor1, propiedad2=valor2, propiedadN=valorN)
```

```kotlin
fun main() {
    val rock1 = Rock(20, 10, 5)
    println(rock1)
}
```

**Salida:**
```
Rock(width=20, height=10, depth=5, variation=1)
```

---

## Copiar Una Instancia (`copy`)

El método `copy()` copia los valores de un objeto en otro. Se pueden especificar argumentos nombrados para cambiar propiedades concretas:

```kotlin
fun main() {
    val rock1 = Rock(20, 10, 5)
    val rock2 = rock1.copy()                   // Copia exacta
    val rock3 = rock1.copy(variation = 4)      // Copia con variación diferente
    println("Roca 1: $rock1")
    println("Roca 2: $rock2")
}
```

**Salida:**
```
Roca 1: Rock(width=20, height=10, depth=5, variation=1)
Roca 2: Rock(width=20, height=10, depth=5, variation=1)
```

---

## Igualdad De Instancias (`equals`)

El método `equals()` compara el **contenido** de los objetos. Dos objetos son iguales si los valores de sus propiedades son iguales. Se puede usar el operador `==` como atajo:

```kotlin
fun main() {
    val rock1 = Rock(20, 10, 5)
    val rock2 = rock1.copy()
    val rock3 = rock1.copy(variation = 4)
    println("rock1 == rock2: ${rock1 == rock2}") // true
    println("rock2 == rock3: ${rock2 == rock3}") // false
}
```

> Para comprobar igualdad de **referencias en memoria** se usa el operador `===`:
> ```kotlin
> println("rock1 === rock2: ${rock1 === rock2}") // false (objetos distintos)
> ```

---

## Código Hash (`hashCode`)

Dos instancias con la misma semántica de propiedades tendrán el mismo hash:

```kotlin
println("rock1.hashCode(): ${rock1.hashCode()}") // 605586
println("rock2.hashCode(): ${rock2.hashCode()}") // 605586
```

---

## Desestructurar Data Classes

Las data classes generan automáticamente funciones `componentN()` por cada propiedad. Esto habilita la **desestructuración**:

```kotlin
fun main() {
    val rock1 = Rock(20, 10, 5)
    // Usando funciones de componente directamente
    println("width = ${rock1.component1()}")
    println("height = ${rock1.component2()}")
    println("depth = ${rock1.component3()}")
    println("variation = ${rock1.component4()}")
}
```

**Forma desestructurada:**

```kotlin
fun main() {
    val (width, height) = Rock(15, 15, 15)
    println("Desestructurando a width($width) y height($height)")
}
```

El compilador invoca `component1()` y `component2()` internamente para asignar los valores a las variables.
