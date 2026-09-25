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

### `val` vs `var` en el constructor

- **`val`** genera solo un **getter**: la propiedad es de solo lectura, no se puede reasignar tras la creación del objeto. Es la opción recomendada por defecto (inmutabilidad).
- **`var`** genera **getter y setter**: la propiedad se puede modificar después de crear el objeto.
- Si un parámetro del constructor **no lleva ni `val` ni `var`**, no se convierte en propiedad de la clase: solo existe dentro del propio constructor (por ejemplo, para usarlo en un bloque `init`) y no es accesible como `objeto.parametro`.

```kotlin
class Persona(val nombre: String)

val p = Persona("Ana")
p.nombre         // OK, se puede leer
p.nombre = "Luis" // ERROR de compilación, "nombre" es val
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

### Qué está pasando realmente en el ejemplo

- `attack` y `speed` en la cabecera de la clase (sin `val`/`var`) son solo **parámetros** del constructor, no propiedades.
- Las propiedades `val attack: Int` y `val speed: Double` se declaran aparte, sin valor inicial (Kotlin lo permite si se promete inicializarlas en un `init`).
- Dentro del `init`, `attack` (sin `this`) se refiere al **parámetro**, mientras que `this.attack` se refiere a la **propiedad de la clase**. Como comparten nombre, el parámetro "tapa" a la propiedad (shadowing), y `this` desambigua.
- Un `init` se ejecuta en el mismo orden en que aparece en el código, entre las declaraciones de propiedades.

### ¿Cuándo usar este patrón en vez de `val`/`var` directamente?

Para el ejemplo de `Weapon` sin lógica extra, es más simple escribir:

```kotlin
class Weapon(val attack: Int, val speed: Double)
```

El patrón con `init` y parámetros "sueltos" tiene sentido cuando hace falta **validar o transformar** el valor antes de asignarlo:

```kotlin
class Weapon(attack: Int, speed: Double) {
    val attack: Int
    val speed: Double
    init {
        require(attack >= 0) { "El ataque no puede ser negativo" }
        this.attack = attack
        this.speed = speed
    }
}
```

---

## Visibilidad Del Constructor

Se puede cambiar la visibilidad del constructor usando modificadores (`public`, `internal`, `protected`, `private`) junto a la palabra `constructor`:

```kotlin
class Item internal constructor(name: String)
```

### Los 4 modificadores

- **`public`** (por defecto): visible desde cualquier parte donde la clase sea visible.
- **`internal`**: solo accesible dentro del mismo módulo (mismo proyecto/módulo de compilación). Fuera del módulo, aunque la clase sea pública, no se puede instanciar directamente.
- **`protected`**: solo accesible desde la propia clase y sus subclases.
- **`private`**: solo accesible dentro de la propia clase. Se usa para forzar que la creación de objetos pase por otro mecanismo, como un método de fábrica.

**Nota:** si se aplica un modificador de visibilidad al constructor primario, es obligatorio escribir explícitamente la palabra `constructor`.

### Ejemplo de uso: constructor privado + factory

```kotlin
class Item private constructor(val name: String) {
    companion object {
        fun crear(name: String): Item {
            require(name.isNotBlank()) { "El nombre no puede estar vacío" }
            return Item(name)
        }
    }
}

val item = Item.crear("Espada") // OK
val item2 = Item("Espada")      // ERROR: constructor privado
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

### Por qué existen y la regla de delegación

El constructor primario está en la cabecera de la clase y es único. Los constructores secundarios permiten ofrecer **varias formas de crear un objeto** con distintas combinaciones de parámetros. Si la clase tiene constructor primario, **todo** constructor secundario está obligado a llamarlo, directa o indirectamente, mediante `: this(...)` — Kotlin no permite "saltarse" el primario, ya que ahí se inicializan las propiedades declaradas en la cabecera.

### Orden de ejecución (lo más importante a tener claro)

Cuando se instancia un objeto a través de un constructor secundario, el orden es siempre:

1. Se ejecuta primero la delegación `: this(...)`, es decir, el **constructor primario**.
2. Como parte de esa ejecución, se disparan las **propiedades y bloques `init`**, en el orden en que aparecen en el cuerpo de la clase.
3. **Al final**, se ejecuta el **cuerpo del constructor secundario**.

Esto significa que cualquier lógica en un `init` se ejecuta siempre antes que el cuerpo de un constructor secundario, y este último puede sobrescribir valores que el `init` ya haya fijado.

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

Trazando qué ocurre en cada caso:

- **`Contact("Erika")`** → llama directamente al constructor primario: `name = "Erika"`, y el `init` genera un UUID aleatorio para `id`.
- **`Contact("C-1", "Mauricio")`** → llama al constructor secundario, que primero delega en el primario vía `: this(name)` (fija `name = "Mauricio"` y el `init` genera igualmente un UUID temporal para `id`); después, ya en el cuerpo del secundario, `this.id = id` **sobrescribe** ese UUID con el valor `"C-1"` recibido como parámetro.

Es decir, en el segundo caso el UUID aleatorio se llega a generar pero se descarta de inmediato: así de estricto es el orden primario+init → cuerpo del secundario.

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
