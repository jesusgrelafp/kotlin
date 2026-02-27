# Alcance De Funciones En Kotlin

En este tutorial se discute el alcance de funciones en Kotlin y cómo declararlas en nivel superior, a nivel de clase y a nivel local.

---

## Funciones De Nivel Superior

Las funciones de nivel superior pueden ser ejecutadas desde cualquier parte del proyecto. Se declaran en un archivo Kotlin **sin necesidad de una clase explícita** que las contenga.

```kotlin
fun topLevelPrint() = println("Función de nivel superior")

fun main() {
    topLevelPrint()
}
```

**Salida:**
```
Función de nivel superior
```

Desde cualquier otro archivo del proyecto es posible ver y llamar a esta función, lo que evidencia su alcance global.

---

## Funciones Miembro

Son funciones declaradas **a nivel de una clase u objeto**. Su visibilidad queda reducida a la clase a la que pertenecen.

```kotlin
class Print {
    fun memberPrint() = println("Función miembro")
}

fun main() {
    Print().memberPrint()
}
```

**Salida:**
```
Función miembro
```

Se accede a ellas mediante la notación `instancia.metodo()`.

---

## Funciones Locales

Una función local es aquella que se declara **dentro de otra función**. Solo puede ser llamada desde la función contenedora.

```kotlin
fun main() {
    fun localPrint() = println("Función local")
    localPrint()
}
```

**Salida:**
```
Función local
```

---

## Resumen

| Tipo de función   | Dónde se declara            | Desde dónde se puede llamar         |
|-------------------|-----------------------------|--------------------------------------|
| Nivel superior    | Directamente en el archivo  | Desde cualquier parte del proyecto   |
| Miembro           | Dentro de una clase/objeto  | A través de una instancia de la clase|
| Local             | Dentro de otra función      | Solo desde la función contenedora    |
