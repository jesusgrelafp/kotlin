# Listas En Kotlin

Una **lista** es una colección genérica de elementos que se caracteriza por almacenarlos de forma ordenada, donde pueden existir duplicados (incluso un ítem `null`) y los elementos se indexan con base `0`.

Su diseño está representado por la interfaz genérica `List<E>`, que hereda las operaciones base de `Collection<E>`:

```kotlin
interface List<out E> : Collection<E>
```

---

## Listas de Solo Lectura

Una lista de solo lectura puede ser consultada tras su inicialización, pero no permite cambiar su estado.

Para crearla se usa `listOf()`:

```kotlin
fun main() {
    val oneToFiveList: List<Int> = listOf(1, 2, 3, 4, 5)
    println(oneToFiveList) // [1, 2, 3, 4, 5]
}
```

Si el tipo puede inferirse, se puede omitir el tipo parametrizado:

```kotlin
val oneToFiveList = listOf(1, 2, 3, 4, 5)
```

---

## Miembros de List

| Miembro | Descripción |
|---|---|
| `size` | Cantidad de elementos de la lista |
| `lista[index]` / `get(index)` | Elemento en la posición `index` |
| `indexOf(element)` | Índice de la primera ocurrencia de `element` |
| `lastIndexOf(element)` | Índice de la última ocurrencia de `element` |
| `subList(fromIndex, toIndex)` | Porción de la lista en el rango `[fromIndex, toIndex)` |

```kotlin
fun main() {
    val oneToFiveList: List<Int> = listOf(1, 2, 3, 4, 5)
    println(oneToFiveList.size)            // 5
    println(oneToFiveList.get(1))          // 2
    println(oneToFiveList[2])              // 3
    println(oneToFiveList.indexOf(5))      // 4
    println(oneToFiveList.lastIndexOf(6))  // -1 (no existe)
    println(oneToFiveList.subList(0, 2))   // [1, 2]
}
```

> `subList(0, 2)` retorna `[1, 2]` porque el índice final (`2`) se excluye del resultado.

---

## Listas Mutables

Una lista mutable está representada por `MutableList<E>`, que además de las consultas de `List<E>`, permite añadir, cambiar y remover elementos:

```kotlin
interface MutableList<E> : List<E>, MutableCollection<E>
```

Se crea con `mutableListOf()`. Los métodos disponibles para modificarla son:

| Método | Descripción |
|---|---|
| `add(element)` | Añade un ítem al final de la lista |
| `add(index, element)` | Inserta un ítem en el índice indicado |
| `removeAt(index)` | Elimina el ítem en el índice indicado |
| `lista[index] = element` / `set(index, element)` | Reemplaza el ítem en el índice |

### Ejemplo completo

```kotlin
fun main() {
    val colorsList = mutableListOf("Amarillo", "Azul", "Rojo")
    colorsList.add("Verde")        // [Amarillo, Azul, Rojo, Verde]
    colorsList.add(0, "Blanco")    // [Blanco, Amarillo, Azul, Rojo, Verde]
    colorsList.removeAt(2)         // [Blanco, Amarillo, Rojo, Verde]
    colorsList[1] = "Negro"        // [Blanco, Negro, Rojo, Verde]
    colorsList.sortDescending()
    println(colorsList)            // [Verde, Rojo, Negro, Blanco]
}
```

La función de extensión `sortDescending()` ordena los ítems en forma descendente.

---

> Para más operaciones sobre listas (transformar, filtrar, agrupar, obtener elementos), consultar la guía de **Operaciones Sobre Colecciones En Kotlin**.
