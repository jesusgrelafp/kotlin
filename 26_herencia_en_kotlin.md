# Herencia En Kotlin

En este tutorial se aprende a aplicar herencia en Kotlin entre clases, explorando la clase `Any`, la sintaxis de herencia, y la sobrescritura de métodos y propiedades.

---

## ¿Qué Es Herencia?

La herencia es un mecanismo de POO para diseñar dos o más entidades que son diferentes pero comparten características comunes.

- **Superclase / Clase base / Clase padre:** contiene las características compartidas.
- **Subclase / Clase hija / Clase derivada:** hereda esas características.

---

## La Clase Any

Toda clase en Kotlin hereda implícitamente de `Any` si no se especifica otra superclase. Proporciona tres métodos:

- `equals()` → indica si otro objeto es igual al actual
- `hashCode()` → retorna el código hash del objeto
- `toString()` → retorna la representación en `String` del objeto

```kotlin
class Ejemplo // Hereda de Any

fun main() {
    val ejemplo1 = Ejemplo()
    val ejemplo2 = Ejemplo()
    println(ejemplo1.toString())       // Ejemplo@34a245ab
    println(ejemplo1.hashCode())       // 883049899
    println(ejemplo1.equals(ejemplo2)) // false
}
```

---

## Sintaxis De Herencia

Para habilitar la herencia se usa el modificador `open` en la superclase, y dos puntos (`:`) en la cabecera de la subclase seguido del nombre de la superclase con sus paréntesis:

```kotlin
open class Ancestro
class Descendiente : Ancestro()
```

---

## Constructor Primario En Herencia

Si la superclase tiene constructor primario, se deben pasar sus parámetros en la declaración de herencia:

```kotlin
open class Ancestro(val propiedad: Boolean)
class Descendiente(propiedad: Boolean) : Ancestro(propiedad)
```

---

## Constructor Secundario En Herencia

Si se quiere llamar al constructor desde un constructor secundario de la subclase, se usa `super`:

```kotlin
open class Weapon(val damage: Int, val speed: Double)

class Bow : Weapon {
    constructor(damage: Int, speed: Double) : super(damage, speed)
}
```

---

## Sobrescribir Métodos

Para sobrescribir un método se necesita:
1. Marcar el método en la superclase con `open`
2. Usar `override` en la subclase

```kotlin
open class Character(val name: String) {
    open fun die() = println("Morir")
}

class Mage(name: String) : Character(name) {
    override fun die() = println("Mago muriendo")
}

fun main() {
    val jaina = Mage("Jaina")
    jaina.die() // Mago muriendo
}
```

---

## Sobrescribir Propiedades

De forma similar a los métodos, se usa `override` sobre la propiedad en la subclase.

> Una propiedad `val` en la superclase puede reescribirse como `var` en la subclase, pero no al revés.

```kotlin
open class BaseItem(val name: String) {
    open var quantity = 1
}

class PopularItem(name: String) : BaseItem(name) {
    override var quantity = 6
}

fun main() {
    val notebook = BaseItem("Cuaderno")
    val pencil = PopularItem("Lapicero")
    println("${notebook.name} x ${notebook.quantity}") // Cuaderno x 1
    println("${pencil.name} x ${pencil.quantity}")     // Lapicero x 6
}
```
