# Constructores En Kotlin

En este tutorial se aprende el uso de constructores en Kotlin para crear instancias de una clase e inicializar sus propiedades. Existen constructores **primarios** y **secundarios**.

---

## ¿Qué Es Un Constructor?

Un constructor es una **función especial** que se usa para inicializar el contenido de las nuevas instancias de una clase. A diferencia de otros lenguajes, en Kotlin no se usa `new`:

```kotlin
class Player

val player1 = Player()
```

Si no se provee un constructor, el compilador genera uno **sin parámetros por defecto**.

---

## Constructor Primario

El constructor primario forma parte de la **cabecera de la clase**. Al declarar `val` o `var` antes de un parámetro, se crea automáticamente una propiedad.

```kotlin
// Con la palabra reservada constructor
class ClaseEjemplo constructor(val propiedad1: Tipo, var propiedad2: Tipo)

// Forma simplificada (sin anotaciones ni modificadores)
class ClaseEjemplo(val propiedad1: Tipo, var propiedad2: Tipo)
```

**Ejemplo:**

```kotlin
class Weapon(val attack: Int, val speed: Double)

fun main() {
    val weapon1 = Weapon(3, 0.5)
    println("Arma 1 (ataque:${weapon1.attack}, velocidad: ${weapon1.speed})")
}
```

**Salida:**
```
Arma 1 (ataque:3, velocidad: 0.5)
```

---

## Bloques De Inicialización (`init`)

Permiten expandir la lógica de inicialización del constructor primario:

```kotlin
class Weapon(attack: Int, speed: Double) {
    val attack: Int
    val speed: Double
    init {
        this.attack = attack
        this.speed = speed
    }
}
```

Se usa `this` para distinguir propiedades de parámetros con el mismo nombre.

---

## Visibilidad Del Constructor

Se puede cambiar la visibilidad del constructor usando modificadores (`public`, `internal`, `protected`, `private`) junto a la palabra `constructor`:

```kotlin
class Item internal constructor(name: String)
```

---

## Constructores Secundarios

Se usan cuando la lista de argumentos del constructor primario no es suficiente para todos los casos. Se declaran con `constructor` dentro de la clase.

Si existe un constructor primario, el secundario debe delegarle con `this`:

```kotlin
class Clase {
    constructor(param1: Tipo, param2: Tipo) : this(/* parámetros */) {
        // Cuerpo
    }
}
```

**Ejemplo con constructor primario y secundario:**

```kotlin
class Contact(var name: String) {
    var id: String
    init {
        id = UUID.randomUUID().toString()
    }
    constructor(id: String, name: String) : this(name) {
        this.id = id
    }
}
```

Instanciación:
```kotlin
Contact("Erika")
Contact("C-1", "Mauricio")
```

---

## Ejemplo Con Dos Constructores Secundarios

Cuando no se necesita la lógica del primario en todos los casos, es mejor usar dos constructores secundarios:

```kotlin
class Contact {
    var id: String
    var name: String
    constructor(name: String) {
        this.name = name
        id = UUID.randomUUID().toString()
    }
    constructor(id: String, name: String) {
        this.id = id
        this.name = name
    }
}
```

```kotlin
val contacto1 = Contact("Erika")
val contacto2 = Contact("C-1", "Mauricio")
```
