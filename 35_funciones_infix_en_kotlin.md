# Funciones infix En Kotlin

Las funciones `infix` permiten mejorar la legibilidad de la invocación de funciones entre dos operandos, usando la notación de infijo.

---

## El Modificador infix

La palabra reservada `infix` permite llamar a una función insertando su nombre entre dos operandos, en lugar de usar la llamada regular con punto y paréntesis.

Ejemplo con la función `and()`:

```kotlin
fun main() {
    val a = 20
    print((a >= 0) and (a <= 21))
}

public infix fun and(other: Boolean): Boolean
```

Las siguientes expresiones son equivalentes:

```kotlin
a and b
// es igual a
a.and(b)
```

---

## Requerimientos para Crear una Función infix

Para que la notación infix sea válida, la función debe cumplir:

1. Debe ser una **función miembro** o **función de extensión**
2. Debe recibir **un solo parámetro** (el operando de la derecha)
3. El parámetro **no debe aceptar argumentos variables** ni tener **valor por defecto**

---

## Ejemplo: Detección de Colisión entre Círculos

Clase base:

```kotlin
class Circle(val radius: Float, var x: Float, var y: Float)
```

La colisión se produce cuando la distancia entre centros es menor que la suma de los radios:

```
d(C1, C2) = sqrt((x2-x1)² + (y2-y1)²)
colisión: d < r1 + r2
```

Implementación como función de extensión infix:

```kotlin
private infix fun Circle.collideWith(other: Circle): Boolean {
    val dx = this.x - other.x
    val dy = this.y - other.y
    val distance = sqrt(dx.pow(2) + dy.pow(2))
    return distance < this.radius + other.radius
}
```

Uso:

```kotlin
fun main() {
    val circle1 = Circle(5f, 10f, 10f)
    val circle2 = Circle(3f, 8f, 7f)
    println("¿Colisión?: ${circle1 collideWith circle2}")
}
// ¿Colisión?: true
```

La expresión `c1 collideWith c2` resulta mucho más legible que `c1.collideWith(c2)`.
