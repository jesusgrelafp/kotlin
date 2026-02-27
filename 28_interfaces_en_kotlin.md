# Interfaces En Kotlin

En este tutorial se explica cómo definir e implementar interfaces en Kotlin para proveer comportamiento adicional a las clases.

---

## Definir Una Interfaz

Las interfaces permiten definir tipos cuyos comportamientos pueden ser **compartidos por varias clases no relacionadas**. Se declaran con la palabra reservada `interface`:

```kotlin
interface Interfaz {
    val p1: Int          // Propiedad abstracta
    val p2: Boolean      // Propiedad regular con accesor
        get() = p1 > 0
    fun m1()             // Método abstracto
    fun m2() {           // Método regular con implementación
        print("Método implementado")
    }
}
```

### Características importantes de las interfaces:

- Pueden contener métodos abstractos y métodos regulares con implementación.
- Pueden contener propiedades abstractas y regulares, pero **sin campos de respaldo**.
- **No permiten** declaración de constructores.
- Sus propiedades y métodos regulares pueden sobrescribirse con `override` **sin necesidad de `open`**, a diferencia de las clases abstractas.
- Una clase puede **implementar múltiples interfaces**.

---

## Implementar Una Interfaz

Se implementa con el símbolo `:` en la cabecera de la clase. Los miembros abstractos deben sobrescribirse con `override`:

```kotlin
class Ejemplo : Interfaz {
    override val p1: Int = 0
    override fun m1() {
        print("Sobrescribiendo método de Interfaz")
    }
}
```

---

## Ejemplo: Interfaz `Explosive`

```kotlin
interface Explosive {
    fun explode()
}

class Box : Explosive {
    override fun explode() = println("¡Kaboom!")
}

fun main() {
    Box().explode() // ¡Kaboom!
}
```

---

## Implementar Múltiples Interfaces

Una clase puede implementar varias interfaces a la vez, separándolas con coma:

```kotlin
interface Incinerable {
    fun incinerate()
}

class Box : Explosive, Incinerable {
    override fun explode() = println("¡Kaboom!")
    override fun incinerate() = println("¡Boosh!")
}
```

---

## Resolver Conflictos De Sobrescritura

Si dos interfaces tienen un método con el mismo nombre, la clase que las implementa **debe sobrescribirlo** para resolver el conflicto. Se puede llamar a la implementación deseada con `super<Tipo>`:

```kotlin
interface Explosive {
    fun explode()
    fun warning() = println("Explosivo")
}

interface Incinerable {
    fun incinerate()
    fun warning() = println("Incinerable")
}

class Box : Explosive, Incinerable {
    override fun explode() = println("¡Kaboom!")
    override fun incinerate() = println("¡Boosh!")
    override fun warning() {
        super<Incinerable>.warning()
        super<Explosive>.warning()
    }
}

fun main() {
    val box = Box()
    box.warning()
    box.explode()
    box.incinerate()
}
```

**Salida:**
```
Incinerable
Explosivo
¡Kaboom!
¡Boosh!
```
