# Propiedades En Kotlin

En este tutorial se muestra la declaración de propiedades en Kotlin, el uso de métodos get/set y la visibilidad.

---

## Declaración De Propiedades

Una propiedad en Kotlin es la agrupación de: un **campo**, su **accesor `get`** y su **mutador `set`**.

- `val` → propiedad de **solo lectura** (solo genera `get`)
- `var` → propiedad **mutable** (genera `get` y `set`)

```kotlin
class Customer {
    val customerId: String = "C-100"
    val name: String = "Guillermo Fenix"
    val phone: String = "388-4881"
    var orders: Int = 15
}
```

**Acceso y modificación:**

```kotlin
val customer = Customer()
println(customer.name)      // Acceder
customer.orders = 20        // Modificar (solo var)
```

---

## Getters Y Setters

### Getters Personalizados

Se definen con `get()` para retornar un valor calculado en lugar de almacenar uno fijo:

```kotlin
class Animal(val name: String, var age: Int) {
    val isOlderThanOne: Boolean
        get() = this.age > 1
}
```

Forma simplificada (inferencia de tipo):
```kotlin
val isOlderThanOne
    get() = this.age > 1
```

**Uso:**
```kotlin
val animal = Animal("Chimpi", 2)
print(animal.isOlderThanOne) // true
```

---

### Setters Personalizados

Se definen con `set(value)`. El identificador `field` referencia al valor del campo:

```kotlin
class Animal(val name: String, var age: Int) {
    val isOlderThanOne
        get() = this.age > 1
    var overWeight = false
    var weight = 0.0
        set(value) {
            field = value
            overWeight = value > 100
        }
}
```

**Uso:**
```kotlin
val simone = Animal("Simone", 12)
simone.weight = 156.32
print("¿Sobrepeso?:${if (simone.overWeight) "SI" else "NO"}")
// ¿Sobrepeso?:SI
```

---

## Accesores Por Defecto

Declarar una propiedad genera automáticamente accesores con `field`. Es decir:

```kotlin
class Animal {
    var weight = 0
}
```

Es equivalente a:

```kotlin
class Animal {
    var weight = 0
        get() = field
        set(value) { field = value }
}
```

---

## Visibilidad De Propiedades

Se puede cambiar la visibilidad de los getters y setters usando modificadores de visibilidad:

```kotlin
var overWeight = false
    private set
```

Esto hace que `overWeight` solo pueda ser asignado internamente en la clase, pero leído desde fuera.
