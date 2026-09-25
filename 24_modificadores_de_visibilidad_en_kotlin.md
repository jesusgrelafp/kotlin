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

### Analizando el ejemplo paso a paso

- **`open class A`** → `open` es necesaria para que la clase pueda ser **heredada**. Por defecto, en Kotlin todas las clases son `final` (no heredables), a diferencia de otros lenguajes como Java.
- **`public var m1`** → visible desde cualquier lugar donde `A` sea visible. Es el modificador por defecto (casi nunca hace falta escribirlo).
- **`internal var m2`** → visible solo dentro del mismo módulo (mismo proyecto/módulo de compilación).
- **`private fun m3()`** → visible solo dentro de la propia clase `A`. Ni siquiera las subclases pueden verlo.
- **`protected open fun m4()`** → visible desde `A` y sus subclases, pero no desde fuera. Además, `open` indica que este método se puede sobrescribir.

En `class B : A()`, cada miembro se comporta así:

| Miembro | ¿Visible en `B`? | ¿Se puede sobrescribir? | Por qué |
|---|---|---|---|
| `m1` | Sí | No | Es `public`, pero no tiene `open`: se ve, pero no admite `override` |
| `m2` | Sí | No | `internal` lo hace visible en el módulo, pero sin `open` no se puede sobrescribir |
| `m3` | No | — | `private` lo limita exclusivamente a `A` |
| `m4` | Sí | **Sí** | Es `protected` (visible para subclases) **y** `open` (permite `override`) |

**Idea clave:** visibilidad y capacidad de sobrescritura son conceptos **independientes**. La visibilidad controla quién puede *ver/usar* el miembro; `open` controla si se puede *redefinir* en una subclase. Un miembro puede ser visible sin ser sobrescribible (`m1`, `m2`), y solo `m4` cumple ambas condiciones.

Además, al sobrescribir `m4`, `B` sube su visibilidad de `protected` a `public`:
```kotlin
public override fun m4() = m1 + 100
```
Esto está permitido: en Kotlin, al hacer `override` puedes **ampliar** la visibilidad de un miembro heredado, pero nunca restringirla.

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

---

## Detalles Adicionales

### Visibilidad Del Setter

Es posible dar a una propiedad una visibilidad y a su **setter** una más restrictiva, dejando el getter público pero controlando quién puede modificar el valor:

```kotlin
class Contador {
    var valor: Int = 0
        private set   // el setter es privado; el getter sigue siendo public

    fun incrementar() {
        valor++       // solo se puede modificar desde dentro de la clase
    }
}

val c = Contador()
println(c.valor)   // OK, se puede leer
c.incrementar()
// c.valor = 5      // ERROR: el setter es private
```

Esto es muy habitual para exponer un dato de solo lectura hacia fuera mientras la propia clase controla cómo y cuándo cambia.

### `internal`, un poco más de contexto

`internal` está pensado principalmente para **librerías y módulos**: permite que una clase, función o propiedad sea `public` de cara al propio módulo (se puede usar libremente entre sus archivos) pero **quede oculta para quien consuma el módulo compilado** desde fuera (por ejemplo, otro proyecto que añade tu librería como dependencia). Es la forma de exponer una API pública reducida sin tener que marcarlo todo como `private`.
