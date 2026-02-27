# Modificadores De Visibilidad En Kotlin

Los modificadores de visibilidad permiten **restringir el acceso** a clases, objetos, interfaces, constructores, funciones, propiedades y sus setters.

---

## Modificadores Disponibles

| Modificador  | Descripción                                              |
|--------------|----------------------------------------------------------|
| `private`    | Visible solo en la clase o archivo actual                |
| `protected`  | Visible en la clase y sus subclases                      |
| `internal`   | Visible en el módulo actual                              |
| `public`     | Visible en todas partes (valor por defecto)              |

> Si se omite el modificador, el valor asignado por defecto es `public` junto a `final`.

---

## Declaraciones De Nivel Superior

Cuando una declaración se ubica en un archivo Kotlin (nivel superior):

| Modificador  | Efecto                          |
|--------------|---------------------------------|
| `public`     | Visible en todas partes         |
| `internal`   | Visible en el módulo actual     |
| `protected`  | No disponible                   |
| `private`    | Visible solo en el archivo      |

```kotlin
// Archivo: TopLevel.kt
public val propiedad = "Propiedad"       // Visible en cualquier lugar
private fun funcion() = println("Función") // Visible solo en TopLevel.kt
internal class Clase                      // Visible solo en el módulo "main"
```

---

## Clases E Interfaces

Para los miembros de una clase:

| Modificador  | Efecto                              |
|--------------|-------------------------------------|
| `public`     | Visible en todo lugar               |
| `internal`   | Visible en el módulo                |
| `protected`  | Visible en las subclases            |
| `private`    | Visible solo en la clase actual     |

```kotlin
open class A {
    public var m1 = 10
    internal var m2 = "Propiedad interna"
    private fun m3() = println("Método privado")
    protected open fun m4() = m1 + 10
}

class B : A() {
    // m1 es visible pero no se puede sobrescribir
    // m2 es visible pero no se puede sobrescribir
    // m3 no es visible
    // m4 es visible y se puede sobrescribir
    public override fun m4() = m1 + 100
}
```

> `open` habilita la sobrescritura de un miembro. Es lo contrario a `final`. El modificador `override` aplica la sobrescritura desde la subclase.

---

## Visibilidad De Constructores

Por defecto los constructores son `public`. Para cambiar su visibilidad se usa la palabra `constructor` con el modificador:

```kotlin
class Table(height: Int)                                    // public por defecto
class Eraser internal constructor(val dimen: Int)           // internal
open class Pencil protected constructor(val mark: String)   // protected
class Book private constructor(val pages: Int)              // private
```

> `protected` es equivalente a `private` si la clase es `final`. Si se marca con `open`, será visible para las subclases.
