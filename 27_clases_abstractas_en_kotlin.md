# Clases Abstractas En Kotlin

En este tutorial se aprende la declaración de clases abstractas en Kotlin para definir tipos que permitan múltiples implementaciones.

---

## El Modificador `abstract`

Una **clase abstracta** está marcada con `abstract`. Esto:
- **Impide** crear instancias directas de la clase.
- **Permite** crear subclases a partir de ella.

```kotlin
abstract class ClaseAbstracta {
    // Propiedades regulares
    // Propiedades abstractas
    // Métodos abstractos
    // Métodos regulares
}
```

Los miembros también pueden marcarse con `abstract`, lo que significa que **no tienen implementación** y esta será obligatoria en las subclases (usando `override`):

```kotlin
abstract class ClaseAbstracta {
    abstract val propiedadAbstracta: Int
    abstract fun metodoAbstracto()
    fun metodoNoAbstracto() {
        // Cuerpo con implementación
    }
}

class Subclase : ClaseAbstracta() {
    override val propiedadAbstracta: Int = 10
    override fun metodoAbstracto() {
        print(propiedadAbstracta)
    }
}
```

> Una clase abstracta **no necesita** el modificador `open` para permitir herencia. Tampoco sus miembros abstractos. Solo se usa `open` en miembros no abstractos si se desea permitir su sobrescritura.

---

## Ejemplo: Ataques En Un Videojuego

Se modela un sistema de ataques donde cada tipo tiene su propio comportamiento al ejecutarse.

**Clase abstracta base:**

```kotlin
abstract class Attack {
    val baseDamage: Int = 10
    abstract fun execute(): String
}
```

**Subclases con implementaciones específicas:**

```kotlin
class Headbutt : Attack() {
    override fun execute(): String = "¡Cabezazo! ${baseDamage + 1}"
}

class DoubleKick : Attack() {
    override fun execute(): String = "¡Golpe doble! ${baseDamage + 2}"
}

class Fireball : Attack() {
    override fun execute(): String = "¡Bola de fuego! ${baseDamage + 3}"
}
```

**Uso:**

```kotlin
fun main() {
    val attacks = mutableListOf(Headbutt(), DoubleKick(), Fireball())
    attacks.forEach { println(it.execute()) }
}
```

**Salida:**
```
¡Cabezazo! 11
¡Golpe doble! 12
¡Bola de fuego! 13
```

> Si se intenta crear una instancia directa de `Attack`, el compilador lanzará el error:
> ```
> Cannot create an instance of an abstract class
> ```
