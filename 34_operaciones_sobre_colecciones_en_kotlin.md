# Operaciones Sobre Colecciones En Kotlin

La librería estándar de Kotlin provee funciones de extensión para aplicar operaciones sobre colecciones. A continuación se listan todas las categorías y funciones disponibles.

---

## Filtrar

- `filter` — Filtra elementos según un predicado
- `partition` — Divide la colección en dos listas: los que cumplen y los que no cumplen el predicado
- `any` — Retorna `true` si al menos un elemento cumple el predicado
- `all` — Retorna `true` si todos los elementos cumplen el predicado
- `none` — Retorna `true` si ningún elemento cumple el predicado

---

## Transformar

- `map` — Transforma cada elemento según una función
- `associateBy` — Crea un mapa usando como clave el resultado de una función sobre cada elemento
- `associate` — Crea un mapa a partir de pares generados por una función
- `flatten` — Aplana una colección de colecciones en una sola lista
- `zip` — Combina dos colecciones en una lista de pares
- `joinToString()` — Une los elementos en una cadena de texto

---

## Agrupación

- `groupBy` — Agrupa los elementos en un mapa según una clave calculada
- `groupingBy` — Crea un objeto `Grouping` para operaciones de agrupación diferidas

---

## Agregados

- `count` — Cuenta los elementos (opcionalmente con predicado)
- `minOrNull` — Retorna el elemento mínimo o `null` si está vacía
- `maxOrNull` — Retorna el elemento máximo o `null` si está vacía
- `sum` — Suma los elementos numéricos
- `average` — Calcula la media de los elementos
- `reduce` — Acumula los elementos aplicando una operación binaria de izquierda a derecha
- `fold` — Igual que `reduce` pero con un valor inicial

---

## Obtener un Solo Elemento

- `find` — Retorna el primer elemento que cumple el predicado o `null`
- `elementAt` — Retorna el elemento en la posición indicada
- `contains` — Comprueba si un elemento está en la colección
- `random` — Retorna un elemento aleatorio

---

## Obtener Partes de una Colección

- `slice` — Retorna una sublista con los índices especificados
- `take` — Retorna los primeros N elementos
- `drop` — Elimina los primeros N elementos y retorna el resto
- `chunked` — Divide la colección en trozos de tamaño N
- `windowed` — Genera ventanas deslizantes de tamaño N

---

## Ordenar

- `sorted` — Ordena los elementos en orden natural
- `reversed` — Invierte el orden de los elementos
- `shuffled()` — Mezcla aleatoriamente los elementos

---

> Esta página está en construcción. Algunas funciones pueden tener documentación adicional en los artículos individuales de la guía.
