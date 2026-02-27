# Clases En Kotlin

En este tutorial se aprende sobre el concepto, la declaración e instanciación de clases en Kotlin.

---

## Declaración De Una Clase

Las clases son el componente medular del paradigma de **POO (Programación Orientada a Objetos)**. Representan entidades o conceptos dentro de un modelo predefinido.

En Kotlin, una clase es una **agrupación de propiedades (atributos) y funciones (métodos) miembro**, que actúa como plantilla para la instanciación de objetos.

La declaración se compone de:
- Nombre de la clase
- Cabecera (opcional)
- Cuerpo (opcional)

```kotlin
class Supervisor {
    /** Cuerpo de clase **/
}
```

La cabecera puede incluir modificadores, parámetros, constructor primario, herencia y restricciones de tipo. En su forma mínima:

```kotlin
class Supervisor
```

---

## Ejemplo De Declaración De Clase

**Problema:** Modelar un avión que se mueve en dos dimensiones dentro del límite `[300, 300]`, con posición inicial `[0, 0]`.

**Solución:**

```kotlin
class Plane {
    var x: Int = 0
        private set
    var y: Int = 0
        private set

    fun moveLeft() {
        x -= if (x == 0) 0 else 1
    }
    fun moveRight() {
        x += if (x == 300) 0 else 1
    }
    fun moveUp() {
        y -= if (y == 0) 0 else 1
    }
    fun moveDown() {
        y += if (y == 300) 0 else 1
    }
}
```

- Las propiedades `x` e `y` son mutables con `var` pero con setter privado para controlar su modificación.
- Cada método es una función miembro sin retorno que altera los ejes con una expresión `if`.

---

## Crear Instancias De Clases

Para crear una instancia se usa una **llamada regular al constructor** (sin la palabra `new`):

```kotlin
val plane = Plane()
```

Acceso a propiedades mediante notación de punto:

```kotlin
plane.x
```

**Ejemplo completo:**

```kotlin
fun main() {
    val plane = Plane()
    plane.moveRight()
    plane.moveRight()
    plane.moveDown()
    plane.moveUp()
    plane.moveLeft()
    println("Posición actual del avión: (${plane.x},${plane.y})")
}
```

**Salida:**
```
Posición actual del avión: (1,0)
```
