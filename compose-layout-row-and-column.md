# Compose Layout: Row and Column

> Learn how to arrange UI elements horizontally and vertically using Row and Column composables in Jetpack Compose.

*Basics · January 25, 2024 · 10 min read*  
*Fuente: <https://www.jetpackcompose.net/compose-layout-row-and-column>*

## What Are Layouts in Android?

A layout provides an invisible container to hold views or other layouts. We can place a group of views inside layouts. Row and Column are layouts that arrange our views in a linear manner.

## What is Linear Arrangement?

A linear arrangement means placing elements one after another. In this manner, elements are arranged in order, either horizontally or vertically.

**Row** - Arranges views horizontally.

**Column** - Arranges views vertically.

![Row and Column diagram](.gitbook/assets/0d004d_7292d88214d043e68aec8aec58b7b795_mv2.jpg)

## Row

A Row displays each child next to the previous children. It works like a LinearLayout with horizontal orientation.

```kotlin
@Composable
fun SimpleRow(){
    Row {
        Text(text = "Row Text 1", Modifier.background(Color.Red))
        Text(text = "Row Text 2", Modifier.background(Color.White))
        Text(text = "Row Text 3", Modifier.background(Color.Green))
    }
}
```

## Column

A Column displays each child below the previous children. It works like a LinearLayout with vertical orientation.

```kotlin
@Composable
fun SimpleColumn(){
    Column {
        Text(text = "Column Text 1", Modifier.background(Color.Red))
        Text(text = "Column Text 2", Modifier.background(Color.White))
        Text(text = "Column Text 3", Modifier.background(Color.Green))
    }
}
```

I placed these composables inside a column with labels. The full source code link is available at the end of this tutorial.

**Output of both Row and Column:**

![Row and Column output](.gitbook/assets/0d004d_e10bd4a1aead490fac65b2010bbd83d9_mv2.png)

## Alignment

There are nine alignment options that can apply to child UI elements.

## Arrangement

We also have three arrangements that can be applied as vertical and horizontal arrangements:

- SpaceEvenly
- SpaceBetween
- SpaceAround

The **SpaceEvenly** arrangement places child elements across the main axis, including free space before the first and after the last child.

![SpaceEvenly arrangement](.gitbook/assets/0d004d_0425e528f4f24ed3a7a05c9fee7139d0_mv2.jpg)

The **SpaceBetween** arrangement places child elements across the main axis without free space before first and after the last child.

![SpaceBetween arrangement](.gitbook/assets/0d004d_97d662b107bc4db78aa275cae59d1977_mv2.jpg)

The **SpaceAround** arrangement places child elements across the main axis with half of the free space before the first and after the last child.

![SpaceAround arrangement](.gitbook/assets/0d004d_0300ba2e8c304e0698fd6104cf65fc00_mv2.jpg)

## Row Arrangement and Alignment

```kotlin
@Composable
fun RowArrangement(){
    Row(modifier = Modifier.fillMaxWidth(),
        verticalAlignment = Alignment.Top,
        horizontalArrangement = Arrangement.SpaceEvenly) {
        Text(text = " Text 1")
        Text(text = " Text 2")
        Text(text = " Text 3")
    }
}
```

## Column Arrangement and Alignment

```kotlin
@Composable
fun ColumnArrangement(){
    Column(modifier = Modifier.fillMaxHeight().fillMaxWidth(),
        verticalArrangement = Arrangement.SpaceEvenly,
        horizontalAlignment = Alignment.End
    ) {
        Text(text = "Text 1", Modifier.background(Color.Red))
        Text(text = "Text 2", Modifier.background(Color.White))
        Text(text = "Text 3", Modifier.background(Color.Green))
    }
}
```

**Output:**

![Column arrangement output](.gitbook/assets/0d004d_67a1f63a66594e29b732e0cde0ce7f75_mv2.png)

## Source code

[https://github.com/JetpackCompose/Jetpack-Compose-Samples](https://github.com/JetpackCompose/Jetpack-Compose-Samples)
