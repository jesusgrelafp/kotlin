# Flujo De Entrada Y Salida En Kotlin

Este tutorial te mostrará cómo realizar operaciones sobre el flujo de entrada y salida en Kotlin, es decir, imprimir datos en la consola y leer datos desde el teclado del usuario.

---

## Mostrar Datos Al Usuario

Usa las funciones `print()` y `println()` del paquete `kotlin.io`, para imprimir el mensaje que desees pasar como parámetro.

Cabe aclarar que internamente son invocaciones respectivas a los métodos `System.out.print()` y `System.out.println()` del JDK.

**Por ejemplo:** Imprimir mensaje sobre incremento de nivel para el jugador.

```kotlin
fun main() {
    val levelUpMessage = "¡Subiste de nivel!"
    println(levelUpMessage)
}
```

Si corres la aplicación, se imprimirá en el flujo de salida:

```
¡Subiste de nivel!
```

La función `print()` imprime el mensaje que pongas sin más. En el caso de `println()`, se agrega un separador de línea para la legibilidad de los mensajes subsecuentes.

**Por ejemplo:** Imprimir dos mensajes al jugador sobre su aumento de nivel y nueva habilidad aprendida.

```kotlin
fun main() {
    val levelUpMessage = "¡Subiste de nivel!"
    val newAbility = "Habilidad Tajo aprendida"
    print(levelUpMessage)
    print(newAbility)
}
```

La salida sería:

```
¡Subiste de nivel!Habilidad Tajo aprendida
```

Si cambias la impresión a `println()`, entonces se agregaría el salto de línea:

```
¡Subiste de nivel!
Habilidad Tajo aprendida
```

---

## Leer Entradas Del Usuario

Lee datos desde el teclado del usuario con la función `readLine()`.

La cual monitorea indefinidamente el flujo de entrada, hasta que se confirme la escritura de bytes con la tecla **ENTRAR**.

El resultado retornado es un `String` anulable.

**Por ejemplo:** Leer el nombre del personaje que usará el jugador.

```kotlin
fun main() {
    print("Ponle un nombre a tu personaje:")
    val pjName = readLine()

    print("¡Bienvenido $pjName!")
}
```

Si lo ejecutas, en la ventana **Run** de IntelliJ IDEA, la aplicación estará esperando por tu entrada y confirmación.

---

## ¿Qué Sigue?

Una vez terminaste esta sección de fundamentos, lo siguiente es adentrarse a las estructuras de programación. Comienza con la **expresión if** como herramienta de bifurcación en tus programas.
