# Mapas En Kotlin

Un **mapa** es una colección que almacena sus elementos (entradas) en forma de pares clave-valor. A cada clave le corresponde un solo valor y será única, como si fuera un identificador.

---

## Crear Mapas de Solo Lectura

La interfaz que representa los mapas en Kotlin es `Map<K,V>`, donde `K` es el tipo de las claves y `V` el de los valores:

```kotlin
interface Map<K, out V>
```

Para crear un mapa de solo lectura se usa `mapOf()`:

```kotlin
fun main() {
    val userSettings: Map<String, String> = mapOf(
        "name" to "Catrina",
        "language" to "Español",
        "logo" to "logo.png",
        "website" to "www.site.com"
    )
    println("$userSettings")
    // {name=Catrina, language=Español, logo=logo.png, website=www.site.com}
}
```

Las entradas se crean con la función infix `to()`, que genera instancias de `Pair`:

```kotlin
infix fun <A, B> A.to(that: B): Pair<A, B>
```

También es posible crear el par con `Pair("name", "Catrina")`.

---

## Operaciones de Lectura

| Propiedad/Método | Descripción |
|---|---|
| `entries` | `Set<Entry<K,V>>` de todos los pares clave-valor |
| `keys` | `Set<K>` de todas las claves |
| `values` | `Collection<V>` de todos los valores |
| `size` | Número de entradas |
| `mapa[clave]` / `get(clave)` | Obtiene el valor por clave (retorna `null` si no existe) |
| `getOrDefault(key, default)` | Obtiene el valor o retorna el valor por defecto |
| `isEmpty()` | `true` si el mapa no tiene entradas |
| `containsKey(key)` / `key in map` | `true` si la clave existe |
| `containsValue(value)` | `true` si el valor existe |

```kotlin
println(userSettings["logo"])                          // logo.png
println(userSettings.get("web"))                       // null
println(userSettings.getOrDefault("email", "Sin email")) // Sin email
println(userSettings.isEmpty())                        // false
println("name" in userSettings)                        // true
println("Español" in userSettings.values)              // true
```

---

## Crear Mapas Mutables

Los mapas mutables permiten añadir, actualizar y remover entradas. Se implementan con `MutableMap<K,V>`:

```kotlin
interface MutableMap<K, V> : Map<K, V>
```

Se crean con `mutableMapOf()`:

```kotlin
fun main() {
    val booksMap = mutableMapOf(
        "Sinsajo" to 2010,
        "Yo, Robot" to 1950,
        "Crimen y castigo" to 1935,
        "Cien años de soledad" to 1991
    )
}
```

### Añadir y Actualizar Entradas

```kotlin
booksMap.put("La máquina del tiempo", 1890)
booksMap["La máquina del tiempo"] = 1895  // forma recomendada
```

### Remover Entradas

```kotlin
booksMap.remove("Sinsajo")
// Variante: solo remueve si el valor actual coincide
println(booksMap.remove("Cien años de soledad", 2015)) // false
```

---

## Recorrer un Mapa

Se puede desestructurar cada entrada en un bucle `for`:

```kotlin
fun main() {
    val operationsMap = mapOf(
        "Suma" to '+',
        "Resta" to '-',
        "Multiplicación" to 'x',
        "División" to '÷'
    )
    for ((operation, symbol) in operationsMap) {
        println("$operation -> $symbol")
    }
}
// Suma -> +
// Resta -> -
// Multiplicación -> x
// División -> ÷
```

También con `forEach` y desestructuración en el lambda:

```kotlin
operationsMap.forEach { (k, v) -> println("$k -> $v") }
```
