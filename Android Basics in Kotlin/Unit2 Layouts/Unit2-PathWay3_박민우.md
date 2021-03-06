# ๐ฅ Unit 2 : Layouts

## Pathway 3 : Display a scrollable list

## ๐ Track 2 : Kotlin์์ ๋ชฉ๋ก ์ฌ์ฉ

### List

+ List : ํน์  ์์๊ฐ ์๋ ํญ๋ชฉ์ ๋ชจ์

  + `List` : ์ฝ๊ธฐ ์ ์ฉ List๋ก, ๋ง๋  ํ ์์ ํ  ์ ์๋ค.

  + `MutableList` : ๋ณ๊ฒฝ ๊ฐ๋ฅํ List๋ก, ๋ง๋  ํ ์์ ํ  ์ ์๋ค. ์ฆ, ์์๋ฅผ ์ถ๊ฐ, ์ญ์ , ์๋ฐ์ดํธํ  ์ ์๋ค.

  + ```kotlin
    val numbers: List<Int> = listOf(1, 2, 3, 4, 5, 6)
    ```

  + ๋ณ์ ์ ํ์ ํ ๋น ์ฐ์ฐ์(=) ์ค๋ฅธ์ชฝ์ ์๋ ๊ฐ์ ๊ธฐ๋ฐํ์ฌ ์ถ์ธกํ๊ฑฐ๋ ์ถ๋ก ํ  ์ ์์ผ๋ฉด **๋ณ์์ ๋ฐ์ดํฐ ์ ํ์ ์๋ตํ  ์ ์๋ค.**  => `val numbers = listOf(1, 2, 3, 4, 5, 6)`

  + ```kotlin
    println("List: $numbers")   		// List: [1, 2, 3, 4, 5, 6]
    println("Size: ${numbers.size}") 	// Size: 6
    ```

  + List์ ์์ ์ ๊ทผ => `numbers[0]` or `numbers.get(0)`

    ```kotlin
    println("First element: ${numbers[0]}") // First element: 1
    println("First: ${numbers.first()}")	// First: 1
    println("Last: ${numbers.last()}")	   	// Last: 6
    ```

  + `contains()` : List์ ํน์  item์ด ์๋์ง ํ์ธ

  + `reversed()` : ์์๊ฐ ์ญ์์ผ๋ก ์๋ ์ ๋ชฉ๋ก์ ๋ฐํ

  + `sorted()` : ์์๊ฐ ์ค๋ฆ์ฐจ์์ผ๋ก ์ ๋ ฌ๋ ์ ๋ชฉ๋ก์ ๋ฐํ    

<br>

+ Mutable List : ๋ณ๊ฒฝ๊ฐ๋ฅํ List

  + `mutableListOf()`๋ฅผ ํธ์ถํ์ฌ ์์ฑ => `val entrees = mutableListOf<dayatype>()`

    ```kotlin
    val entrees = mutableListOf()
    // Error => Not enough information to infer type variable T
    // ๋ชฉ๋ก์ ์ด๋ค ์ ํ(datatype)์ itme์ด ์ฌ์ง๋ฅผ ์ถ๋ก ํ  ์ ์๊ธฐ ๋๋ฌธ์
    
    val entrees = mutableListOf<String>() // ๋ณ๊ฒฝ๊ฐ๋ฅํ String ์ ํ์ ๋ชฉ๋ก์ ๋ง๋ ๋ค.
    val entrees: MutableList<String> = mutableListOf()
    ```

    > **You can use `val`** for a mutable list because the **`entrees` variable contains a *reference* to the list**, and that **reference doesn't change** even if the contents of the list do.

  + `add()` : ์์ ์ถ๊ฐ, List์ ์์๊ฐ ์ฑ๊ณต์ ์ผ๋ก ์ถ๊ฐ๋๋ฉด `true`๋ฅผ ๋ฐํํ๊ณ  ์ถ๊ฐ๋์ง ์์ผ๋ฉด `false`๋ฅผ ๋ฐํํฉ๋๋ค. => `entrees.add("noodles")`

  + `addAll()` : List์ ์์ ์ฌ๋ฌ๊ฐ ์ถ๊ฐ => `entrees.addAll(moreItems)`

  + `entrees.remove("rice")` : List์์ ํด๋น ์์ ์ญ์ , ์ญ์ ์ ์ฑ๊ณตํ๋ฉด `true`๋ฅผ ๋ฐํ

  + `entrees.removeAt(0)` : 1๋ฒ์งธ ์์๋ฅผ ์ญ์ 

  + `entrees.clear()` : ์ ์ฒด List ์ญ์ 

  + `entrees.isEmpty()`
  
  + `entrees.size()` 

<br>

<br>

### List ๋ฐ๋ณต

+ `while`๋ฌธ

  ```kotlin
  val guestsPerFamily = listOf(2, 4, 1, 3)
  var totalGuests = 0
  var index = 0
  while (index < guestsPerFamily.size) { // index = 0, 1, 2, 3
      totalGuests += guestsPerFamily[index]
      index++
  }
  println("Total Guest Count: $totalGuests")
  ```

<br>

+ `for`๋ฌธ

  ```kotlin
  for (number in numberList) {
     // For each element in the list, execute this code block
  }
  ```

  `number` ๋ณ์๋ `numberList`์ ์ฒซ ๋ฒ์งธ ์์์ ๊ฐ๊ฒ ์ค์ ๋๊ณ  ์ฝ๋ ๋ธ๋ก์ด ์คํ๋ฉ๋๋ค. ๊ทธ๋ฌ๋ฉด `number` ๋ณ์๊ฐ ์๋์ผ๋ก `numberList`์ ๋ค์ ์์๊ฐ ๋๋๋ก ์๋ฐ์ดํธ๋๊ณ  ์ฝ๋ ๋ธ๋ก์ด ๋ค์ ์คํ๋ฉ๋๋ค. ์ด ์์์ `numberList`๊ฐ ๋๋  ๋๊น์ง ๋ชฉ๋ก์ ๊ฐ ์์์ ๋ฐ๋ณต๋ฉ๋๋ค. 

<br>

<br>

### ํด๋์ค ๊ตฌํ

+ toString() ๋ฉ์๋ ์ฌ์ ์

  + **๊ฐ์ฒด ์ธ์คํด์ค๋ฅผ ์ถ๋ ฅํ๋ฉด ๊ฐ์ฒด์ `toString()` ๋ฉ์๋๊ฐ ํธ์ถ**๋ฉ๋๋ค. Kotlin์์๋ ๋ชจ๋  ํด๋์ค๊ฐ ์๋์ผ๋ก `toString()` ๋ฉ์๋๋ฅผ ์์ํฉ๋๋ค. ์ด ๋ฉ์๋์ ๊ธฐ๋ณธ ๊ตฌํ์์๋ **์ธ์คํด์ค์ ๋ฉ๋ชจ๋ฆฌ ์ฃผ์๊ฐ ์๋ ๊ฐ์ฒด ์ ํ**์ ๋ฐํํฉ๋๋ค. 

    ```kotlin
    open class Item(val name: String, val price: Int)
    
    class Noodles : Item("Noodles", 10)
    class Vegetables : Item("Vegetables", 5)
    
    fun main() {
        val noodles = Noodles()
        val vegetables = Vegetables()
        println(noodles)
        println(vegetables)
    }
    
    
    // print result
    Noodles@5451c3a8
    Vegetables@76ed5528
    ```
  
  + ์ข ๋ ์๋ฏธ ์๊ณ  ์ฌ์ฉ์ ์นํ์ ์ธ ๋ด์ฉ์ ๋ฐํํ๋๋ก `toString()`์ ์ฌ์ ์ํด์ผ ํฉ๋๋ค.
  
  + ```kotlin
    class Noodles : Item("Noodles", 10) {
       override fun toString(): String {
           return name // ์์ ํด๋์ค Item์์ name์ ์์๋ฐ์
       }
    }
    ```

<br>

+ `vararg`

  + Kotlin์์ `vararg` ์์ ์๋ฅผ ์ฌ์ฉํ๋ฉด **๋์ผํ ์ ํ์ ๊ฐ๋ณ์ ์ธ ์ธ์ ์**๋ฅผ ํจ์๋ ์์ฑ์์ ์ ๋ฌํ  ์ ์์ต๋๋ค. ์ด๋ ๊ฒ ํ๋ฉด ๋ชฉ๋ก ๋์  ๊ฐ๋ณ ๋ฌธ์์ด๋ก ๋ค์ํ ์ฑ์๋ฅผ ์ ๊ณตํ  ์ ์์ต๋๋ค. 

  + ```kotlin
    class Vegetables(vararg val toppings: String) : Item("Vegetables", 5) {
        
    // ์๋ ์ฝ๋
    class Vegetables(val toppings: List<String>) : Item("Vegetables", 5) 
    ```
    
  + ๋งค๊ฐ๋ณ์ ํ๋๋ง `vararg`๋ก ํ์ํ  ์ ์์ผ๋ฉฐ ์ด ํ๋๋ ์ผ๋ฐ์ ์ผ๋ก ๋ชฉ๋ก์ ๋ง์ง๋ง ๋งค๊ฐ๋ณ์์๋๋ค.

<br>

+ toString() ๋ฉ์๋ ์ฌ์ ์ 

  ```kotlin
  class Vegetables(vararg val toppings: String) : Item("Vegetables", 5) {
      override fun toString(): String {
      if (toppings.isEmpty()) {
          return "$name Chef's Choice"
      } else {
          return name + " " + toppings.joinToString()
      }
  }
  }
  ```

  + ์ด์  `Vegetables` ํด๋์ค์ `toString()` ๋ฉ์๋๋ฅผ ์์ ํ์ฌ `Vegetables Cabbage, Sprouts, Onion` ํ์์ ํ ํ๋ ์ธ๊ธํ๋ `String`์ ๋ฐํํ๋๋ก ํฉ๋๋ค. 

  + ํญ๋ชฉ ์ด๋ฆ(`Vegetables`)์ผ๋ก ์์ํด, **`joinToString()` ๋ฉ์๋๋ฅผ ์ฌ์ฉํ์ฌ ๋ชจ๋  ํ ํ์ ๋จ์ผ ๋ฌธ์์ด๋ก ๊ฒฐํฉ**ํ๊ณ , ์ฌ์ด์ ๊ณต๋ฐฑ์ด ์๋ `+` ์ฐ์ฐ์๋ฅผ ์ฌ์ฉํ์ฌ ๋ ๋ถ๋ถ์ ํจ๊ป ์ถ๊ฐํฉ๋๋ค

    > ์ผํ ์ธ์ ๋ค๋ฅธ ๊ตฌ๋ถ์๋ฅผ ์ง์ ํ๋ ค๋ฉด ์ํ๋ ๊ตฌ๋ถ์ ๋ฌธ์์ด์ `joinToString()` ๋ฉ์๋์ ์ธ์๋ก ์ ๋ฌํ์ธ์. ์: ๊ณต๋ฐฑ์ผ๋ก ๊ฐ ํญ๋ชฉ์ ๊ตฌ๋ถํ๋ `joinToString(" ")`

  + ์ ๋ฌ๋ ํ ํ์ด ์๋ค๋ฉด `Vegetables Chef's Choice`๋ฅผ ๋ฐํํ๋ค. 

<br>

+ ๋น๋ ํจํด

  ๋น๋ ํจํด์ ๋จ๊ณ๋ณ ์ ๊ทผ ๋ฐฉ์์ผ๋ก ๋ณต์กํ ๊ฐ์ฒด๋ฅผ ๋น๋ํ  ์ ์๋ ํ๋ก๊ทธ๋๋ฐ์ ๋์์ธ ํจํด์๋๋ค.

  ```kotlin
  fun addItem(newItem: Item): Order {
      itemList.add(newItem)
      return this
  }
  
  fun addAll(newItems: List<Item>): Order {
      itemList.addAll(newItems)
      return this
  }
  ```

  + `Order` ํด๋์ค์ `addItem()` ๋ฐ `addAll()` ๋ฉ์๋์์ `Unit`(๋๋ ์๋ฌด๊ฒ๋ ์์)์ ๋ฐํํ๋ ๋์  ***๋ณ๊ฒฝ๋ `Order`๋ฅผ ๋ฐํ***(`return this`๋ฅผ ํตํด)ํฉ๋๋ค. Kotlin์ ํค์๋ `this`๋ฅผ ์ ๊ณตํ์ฌ **ํ์ฌ ๊ฐ์ฒด ์ธ์คํด์ค๋ฅผ ์ฐธ์กฐ**ํฉ๋๋ค. `addItem()` ๋ฐ `addAll()` ๋ฉ์๋ ๋ด์์ `this`๋ฅผ ๋ฐํํ์ฌ ํ์ฌ `Order`๋ฅผ ๋ฐํํฉ๋๋ค.

  + `main()` ํจ์์์ ์ด์  ๋ค์ ์ฝ๋์ ๊ฐ์ด ***ํธ์ถ์ ํจ๊ป ์ฐ๊ฒฐ***ํ  ์ ์์ต๋๋ค. ์ด ์ฝ๋๋ ์ `Order`๋ฅผ ๋ง๋ค๊ณ  ๋น๋ ํจํด์ ํ์ฉํฉ๋๋ค.

    ```kotlin
    val order4 = Order(4).addItem(Noodles()).addItem(Vegetables("Cabbage", "Onion"))
    ordersList.add(order4)
    ```

    `Order(4)`๊ฐ `Order` ์ธ์คํด์ค๋ฅผ ๋ฐํํ ํ ์ด ์ธ์คํด์ค์์ `addItem(Noodles())`๋ฅผ ํธ์ถํ  ์ ์์ต๋๋ค. `addItem()` ๋ฉ์๋๊ฐ ๋์ผํ `Order` ์ธ์คํด์ค(์ ์ํ)๋ฅผ ๋ฐํํ๋ฉด ๋ค์ ์ด ์ธ์คํด์ค์์ ์ฑ์๋ก `addItem()`์ ํธ์ถํ  ์ ์์ต๋๋ค. ๋ฐํ๋ `Order` ๊ฒฐ๊ณผ๋ `order4` ๋ณ์์ ์ ์ฅ๋  ์ ์์ต๋๋ค.

  + ์ค์ ๋ก ์ฃผ๋ฌธ์ ๋ณ์์ ์ ์ฅํ์ง ์์๋ ๋๋ค.

    ```kotlin
    ordersList.add(
        Order(5)
            .addItem(Noodles())
            .addItem(Noodles())
            .addItem(Vegetables("Spinach")))
    ```

  => ์ด๋ฌํ ํธ์ถ์ ์ฐ๊ฒฐํ๋ ๊ฒ์ด ํ์๋ ์๋์ง๋ง ํจ์์ ๋ฐํ ๊ฐ์ ํ์ฉํ๋ ์ผ๋ฐ์ ์ด๊ณ  ๊ถ์ฅ๋๋ ๋ฐฉ๋ฒ์ด๋ค.

<br>

### Solution code

```kotlin
open class Item(val name: String, val price: Int)

class Noodles : Item("Noodles", 10) {
    override fun toString(): String {
        return name
    }
}

class Vegetables(vararg val toppings: String) : Item("Vegetables", 5) {
    override fun toString(): String {
        if (toppings.isEmpty()) {
            return "$name Chef's Choice"
        } else {
            return name + " " + toppings.joinToString()
        }
    }
}

class Order(val orderNumber: Int) {
    private val itemList = mutableListOf<Item>()

    fun addItem(newItem: Item): Order {
        itemList.add(newItem)
        return this
    }

    fun addAll(newItems: List<Item>): Order {
        itemList.addAll(newItems)
        return this
    }

    fun print() {
        println("Order #${orderNumber}")
        var total = 0
        for (item in itemList) {
            println("${item}: $${item.price}")
            total += item.price
        }
        println("Total: $${total}")
    }
}

fun main() {
    val ordersList = mutableListOf<Order>()

    // Add an item to an order
    val order1 = Order(1)
    order1.addItem(Noodles())
    ordersList.add(order1)

    // Add multiple items individually
    val order2 = Order(2)
    order2.addItem(Noodles())
    order2.addItem(Vegetables())
    ordersList.add(order2)

    // Add a list of items at one time
    val order3 = Order(3)
    val items = listOf(Noodles(), Vegetables("Carrots", "Beans", "Celery"))
    order3.addAll(items)
    ordersList.add(order3)

    // Use builder pattern
    val order4 = Order(4)
        .addItem(Noodles())
        .addItem(Vegetables("Cabbage", "Onion"))
    ordersList.add(order4)

    // Create and add order directly
    ordersList.add(
        Order(5)
            .addItem(Noodles())
            .addItem(Noodles())
            .addItem(Vegetables("Spinach"))
    )

    // Print out each order
    for (order in ordersList) {
        order.print()
        println()
    }
}
```

<br>

<br>

-----

## ๐ Track 3 : RecyclerView

+ Android๋ ๋ชฉ๋ก์ด ์๋ ์ฑ์ ๋น๋ํ  ์ ์๋๋ก `RecyclerView`๋ฅผ ์ ๊ณตํฉ๋๋ค. `RecyclerView`๋ ํ๋ฉด์์ ์คํฌ๋กค๋ ๋ทฐ๋ฅผ ์ฌ์ฌ์ฉํ๊ฑฐ๋ ์ฌํ์ฉํ์ฌ ๋ชฉ๋ก์ด ํฐ ๊ฒฝ์ฐ์๋ ๋งค์ฐ ํจ์จ์ ์ผ๋ก ์๋ํ๋๋ก ์ค๊ณ๋์์ต๋๋ค. ํ๋ฉด์์ ๋ชฉ๋ก ํญ๋ชฉ์ด ์คํฌ๋กค๋๋ฉด `RecyclerView`๋ ํ์ํ  ๋ค์ ๋ชฉ๋ก ํญ๋ชฉ์ ์ด ๋ทฐ๋ฅผ ์ฌ์ฌ์ฉํฉ๋๋ค. ๋ค์ ๋งํด์, ํญ๋ชฉ์ด ํ๋ฉด์ ์คํฌ๋กค๋๋ ์๋ก์ด ์ฝํ์ธ ๋ก ์ฑ์์ง๋๋ค. ์ด `RecyclerView` ๋์์ ์ฒ๋ฆฌ ์๊ฐ์ ํฌ๊ฒ ๋จ์ถํ๊ณ  ๋ชฉ๋ก์ด ๋ ์ํํ๊ฒ ์คํฌ๋กค๋๋๋ก ๋์์ค๋๋ค.    



###  ์ ํจํค์ง ๋ง๋ค๊ธฐ

+ ์ฝ๋๋ฅผ ๋ผ๋ฆฌ์ ์ผ๋ก ๊ตฌ์ฑํ๋ฉด ๋ค๋ฅธ ๊ฐ๋ฐ์๋ค๋ ์ฝ๋๋ฅผ ์ดํดํ๊ณ  ์ ์ง๊ด๋ฆฌํ๊ณ  ํ์ฅํ  ์ ์์ต๋๋ค. ์๋ฅ๋ฅผ ํ์ผ๊ณผ ํด๋๋ก ์ ๋ฆฌํ๋ ๊ฒ๊ณผ ๋์ผํ ๋ฐฉ๋ฒ์ผ๋ก ์ฝ๋๋ฅผ ํ์ผ ๋ฐ ํจํค์ง๋ก ๊ตฌ์ฑํ  ์ ์์ต๋๋ค.
+ Android ์คํ๋์ค์ **Project** ์ฐฝ(**Android**)์์ **app > java** ์๋์ ์๋ ์ ํ๋ก์ ํธ ํ์ผ์ ์ดํด๋ณด๊ณ  Affirmations ์ฑ์ ์ฐพ์ต๋๋ค. ํจํค์ง ์ธ ๊ฐ, ์ฆ ์ฝ๋์ฉ ํจํค์ง ํ ๊ฐ(**com.example.affirmations**)์ ํ์คํธ ํ์ผ์ฉ ํจํค์ง ๋ ๊ฐ(**com.example.affirmations (androidTest)** ๋ฐ **com.example.affirmations (test)**)๊ฐ ํ์๋ฉ๋๋ค.
+ ๋ค์ ๋ ๊ฐ์ง ๋ฐฉ๋ฒ์ผ๋ก ํจํค์ง๋ฅผ ์ฌ์ฉํ  ์ ์์ต๋๋ค.
  + ์ฝ๋์ ์ฌ๋ฌ ๋ถ๋ถ๋ณ๋ก ์๋ก ๋ค๋ฅธ ํจํค์ง๋ฅผ ๋ง๋ญ๋๋ค. ์๋ฅผ ๋ค์ด, ๊ฐ๋ฐ์๋ **๋ฐ์ดํฐ ์์์ ์ฌ์ฉํ๋ ํด๋์ค**์ **UI**๋ฅผ **์๋ก ๋ค๋ฅธ ํจํค์ง๋ก ๋น๋ํ๋ ํด๋์ค๋ก ๊ตฌ๋ถ**ํ๋ ๊ฒฝ์ฐ๊ฐ ๋ง์ต๋๋ค.
  + ์ฝ๋์ ์๋ ๋ค๋ฅธ ํจํค์ง์ ์ฝ๋๋ฅผ ์ฌ์ฉํฉ๋๋ค. ๋ค๋ฅธ ํจํค์ง์ ํด๋์ค๋ฅผ ์ฌ์ฉํ๋ ค๋ฉด ๋น๋ ์์คํ์ ์ข์ ํญ๋ชฉ์ ํด๋์ค๋ฅผ ์ ์ํด์ผ ํฉ๋๋ค. ๋ํ ์ ๊ทํ๋ ์ด๋ฆ(์: `android.widget.TextView`) ๋์  ์ถ์ฝ ์ด๋ฆ(์: `TextView`)์ ์ฌ์ฉํ  ์ ์๋๋ก ํด๋์ค๋ฅผ ์ฝ๋์ `import`ํ๋ ๊ฒ๋ ํ์ค ๊ดํ์๋๋ค. ์๋ฅผ ๋ค์ด ํด๋์ค์ `sqrt`(`import kotlin.math.sqrt`) ๋ฐ `View`(`import android.view.View`) ๊ฐ์ `import` ๋ฌธ์ ์ด๋ฏธ ์ฌ์ฉํ ๊ฒฝ์ฐ๋ฅผ ์๋ก ๋ค ์ ์์ต๋๋ค.
+ Affirmations ์ฑ์์ Android ํด๋์ค์ Kotlin ํด๋์ค๋ฅผ ๊ฐ์ ธ์ค๋ ๊ฒ ์ธ์๋ ์ฑ์ ์ฌ๋ฌ ํจํค์ง๋ก ๊ตฌ์ฑํฉ๋๋ค. **์ฑ์ ํด๋์ค๊ฐ ๋ง์ง ์๋๋ผ๋ ํจํค์ง๋ฅผ ์ฌ์ฉํ์ฌ ๊ธฐ๋ฅ๋ณ๋ก ํด๋์ค๋ฅผ ๊ทธ๋ฃนํํ๋ ๊ฒ์ด ์ข์ต๋๋ค.**   





### ํจํค์ง ์ด๋ฆ ์ ํ๊ธฐ

+ ํจํค์ง ์ด๋ฆ์ ์ผ๋ฐ์ ์ผ๋ก ์ผ๋ฐ์์ ๊ตฌ์ฒด์ ์ธ ์์๋ก ๊ตฌ์ฑ๋๋ฉฐ ์ด๋ฆ์ ๊ฐ ๋ถ๋ถ์ ์๋ฌธ์๋ก ํ๊ธฐํ๊ณ  ๋ง์นจํ๋ก ๊ตฌ๋ถํฉ๋๋ค. ์ค์: ๋ง์นจํ๋ ์ด๋ฆ์ ์ผ๋ถ์ผ ๋ฟ์ด๋ฉฐ ์ฝ๋ ๋ด์ ๊ณ์ธต ๊ตฌ์กฐ๋ฅผ ๋ํ๋ด๊ฑฐ๋ ํด๋ ๊ตฌ์กฐ๋ฅผ ์ง์ํ์ง ์์ต๋๋ค.
+ ์ธํฐ๋ท ๋๋ฉ์ธ์ ์ ์ญ์ ์ผ๋ก ๊ณ ์ ํ๋ฏ๋ก, **์ด๋ฆ ์ฒซ ๋ถ๋ถ์ ๊ฐ๋ฐ์์ ๋๋ฉ์ธ์ด๋ ๋น์ฆ๋์ค์ ๋๋ฉ์ธ์ ์ฌ์ฉํ๋ ๊ฒ์ด ๊ท์น**์๋๋ค.
+ ํจํค์ง ์ด๋ฆ์ ์ ํํ์ฌ ํจํค์ง์ ํฌํจ๋ ๋ด์ฉ ๋ฐ ํจํค์ง ๊ฐ์ ๊ด๊ณ๋ฅผ ํ์ํ  ์ ์์ต๋๋ค.
+ ์ด๋ฐ ์ฝ๋์ ์๋ก, `com.example` ๋ค์์ ์ฑ ์ด๋ฆ์ ์ฌ์ฉํ๋ ๊ฒ์ด ์ผ๋ฐ์ ์๋๋ค.   





### Affirmation ๋ฐ์ดํฐ ํด๋์ค ๋ง๋ค๊ธฐ

`Affirmation.kt`

```kotlin
package com.example.affirmations.model

data class Affirmation(val stringResourceId: Int)
```



### ๋ฐ์ดํฐ ์์ค๊ฐ ๋๋ ํด๋์ค ๋ง๋ค๊ธฐ

`Datasource.kt`

```kotlin
package com.example.affirmations.data

import com.example.affirmations.R
import com.example.affirmations.model.Affirmation

class Datasource { // ์ด ํด๋์ค๋ ๊ฐ์ฒด๋ฅผ ํธ์ถํ๊ธฐ ์ํด ๋ง๋  ํด๋์ค๊ฐ ์๋๋ผ, ๋ญ๋๊น loadAffirmations๋ฅผ ํธ์ถํ๊ธฐ ์ํ class?

    fun loadAffirmations(): List<Affirmation> {
        return listOf<Affirmation>(
            Affirmation(R.string.affirmation1),
            Affirmation(R.string.affirmation2),
            Affirmation(R.string.affirmation3),
            Affirmation(R.string.affirmation4),
            Affirmation(R.string.affirmation5),
            Affirmation(R.string.affirmation6),
            Affirmation(R.string.affirmation7),
            Affirmation(R.string.affirmation8),
            Affirmation(R.string.affirmation9),
            Affirmation(R.string.affirmation10)
        )
    }
}
```





### ์ฑ์ RecyclerView ์ถ๊ฐํ๊ธฐ

<img src = "https://user-images.githubusercontent.com/31370590/125922681-8fc4d14b-2785-45a7-a84a-121edd87b17d.PNG" width = "400" height = "300">

+ **item** - ํ์ํ  ๋ชฉ๋ก์ ๋จ์ผ ๋ฐ์ดํฐ ํญ๋ชฉ์๋๋ค. ์ฑ์ `Affirmation` ๊ฐ์ฒด ํ๋๋ฅผ ๋ํ๋๋๋ค.
+ **์ด๋ํฐ** - `RecyclerView`์์ ํ์ํ  ์ ์๋๋ก ๋ฐ์ดํฐ๋ฅผ ๊ฐ์ ธ์ ์ค๋นํฉ๋๋ค.
+ **ViewHolder** - affirmations๋ฅผ ํ์ํ๊ธฐ ์ํด ์ฌ์ฉํ๊ฑฐ๋ ์ฌ์ฌ์ฉํ  `RecyclerView`์ฉ ๋ทฐ์ ํ์๋๋ค.
+ **RecyclerView** - ํ๋ฉด์ ํ์๋๋ ๋ทฐ์๋๋ค.



### RecyclerView

+ activity_main.xml ํ์ผ์์ `FrameLayout`์ผ๋ก ์ค์ ํ๊ณ , `RecyclerView` ๋ฐฐ์น
+ ํ ๋ ์ด์์์ ํ์ ๋ทฐ ์ฌ๋ฌ ๊ฐ๋ฅผ ๋ฐฐ์นํ๋ ค๋ฉด `ConstraintLayout`์ด ๊ฐ์ฅ ์ ํฉํ๊ณ  ์ ์ฐํ์ง๋ง, ๋ ์ด์์์ ๋จ์ผ ํ์ ๋ทฐ `RecyclerView`๋ง ์์ผ๋ฏ๋ก, ๋จ์ผ ํ์ ๋ทฐ๋ฅผ ๋ณด์ ํ๋ ๋ฐ ์ฌ์ฉํด์ผ ํ๋ ๋ ๊ฐ๋จํ `ViewGroup`์ธ `FrameLayout`์ผ๋ก ์ ํํ  ์ ์์ต๋๋ค.
+ `RecyclerView`์ `layout_width` ์์ฑ๊ณผ `layout_height` ์์ฑ์ `match_parent`๋ก ๋ณ๊ฒฝ

+ `RecyclerView` ์์ ๋ด๋ถ์ ๋ค์๊ณผ ๊ฐ์ด `LinearLayoutManager`๋ฅผ `RecyclerView`์ ๋ ์ด์์ ๊ด๋ฆฌ์ ์์ฑ์ผ๋ก ์ถ๊ฐํฉ๋๋ค. 

  => `app:layoutManager="LinearLayoutManager"`

+ ํ๋ฉด๋ณด๋ค ๊ธด ํญ๋ชฉ์ ์ธ๋ก ๋ชฉ๋ก์ ์คํฌ๋กคํ  ์ ์์ผ๋ ค๋ฉด ์ธ๋ก ์คํฌ๋กค๋ฐ๋ฅผ ์ถ๊ฐํด์ผ ํฉ๋๋ค.

  => `android:scrollbars="vertical"`



### RecyclerView์ฉ Adapter ๊ตฌํํ๊ธฐ

+ `Datasource`์์ ๋ฐ์ดํฐ๋ฅผ ๊ฐ์ ธ์ ๊ฐ `Affirmation`์ `RecyclerView`์ ํญ๋ชฉ์ผ๋ก ํ์ํ  ์ ์๋๋ก ํ์์ ์ง์ ํด์ค์ผ ํ๋ค. 
+ ***Adapter*** is a design pattern that adapts the data into something that can be used by `RecyclerView`.
+ ์ฌ๊ธฐ์๋, `RecyclerView`์ ํ์ํ  ์ ์๋๋ก `loadAffirmations()`์์ ๋ฐํ๋ ๋ชฉ๋ก์์ `Affirmation` ์ธ์คํด์ค๋ฅผ ๊ฐ์ ธ์ list item view๋ก ์ ํํ๋ ์ด๋ํฐ๊ฐ ํ์ํฉ๋๋ค

+ ์ฑ์ ์คํํ๋ฉด `RecyclerView`๊ฐ ์ด๋ํฐ๋ฅผ ์ฌ์ฉํ์ฌ ํ๋ฉด์ ๋ฐ์ดํฐ๋ฅผ ํ์ํ๋ ๋ฐฉ๋ฒ์ ํ์ํฉ๋๋ค. 
+ ์ฑ์ ์คํํ๋ฉด `RecyclerView`๊ฐ ์ด๋ํฐ๋ฅผ ์ฌ์ฉํ์ฌ ํ๋ฉด์ ๋ฐ์ดํฐ๋ฅผ ํ์ํ๋ ๋ฐฉ๋ฒ์ ํ์ํฉ๋๋ค. `RecyclerView`๋ ๋ชฉ๋ก์ ์ฒซ ๋ฒ์งธ ๋ฐ์ดํฐ ํญ๋ชฉ์ ์ํ ์ ๋ชฉ๋ก ํญ๋ชฉ ๋ทฐ๋ฅผ ๋ง๋ค๋๋ก ์ด๋ํฐ์ ์์ฒญํฉ๋๋ค. ๋ทฐ๊ฐ ์์ฑ๋ ํ์๋ ํญ๋ชฉ์ ๊ทธ๋ฆฌ๊ธฐ ์ํ ๋ฐ์ดํฐ๋ฅผ ์ ๊ณตํ๋๋ก ์ด๋ํฐ์ ์์ฒญํฉ๋๋ค. ์ด ํ๋ก์ธ์ค๋ `RecyclerView`์ ํ๋ฉด์ ์ฑ์ธ ๋ทฐ๊ฐ ๋ ์ด์ ํ์ํ์ง ์์ ๋๊น์ง ๋ฐ๋ณต๋ฉ๋๋ค.   



###  Adapter ๋ง๋ค๊ธฐ

`ItemAdapter.kt`

```kotlin
class ItemAdapter(private val context: Context, private val dataset: List<Affirmation>) {

}
```

+ `ItemAdapter`์๋ ๋ฌธ์์ด ๋ฆฌ์์ค๋ฅผ ํ์ธํ๋ ๋ฐฉ๋ฒ์ ๊ดํ ์ ๋ณด๊ฐ ํ์ํฉ๋๋ค. ์ด๋ฌํ ์ ๋ณด์ ๊ธฐํ ์ฑ ๊ด๋ จ ์ ๋ณด๋ `ItemAdapter` ์ธ์คํด์ค์ ์ ๋ฌํ  ์ ์๋ `Context` ๊ฐ์ฒด ์ธ์คํด์ค์ ์ ์ฅ๋ฉ๋๋ค. 



### ViewHolder

+ `RecyclerView`๋ ํญ๋ชฉ ๋ทฐ์ ์ง์  ์ํธ์์ฉํ์ง ์๋ ๋์  `ViewHolders`๋ฅผ ์ฒ๋ฆฌํฉ๋๋ค. `ViewHolder`๋ `RecyclerView`์ ๋จ์ผ ๋ชฉ๋ก ํญ๋ชฉ ๋ทฐ๋ฅผ ๋ํ๋ด๋ฉฐ ๊ฐ๋ฅํ ๊ฒฝ์ฐ ์ฌ์ฌ์ฉํ  ์ ์์ต๋๋ค. `ViewHolder` ์ธ์คํด์ค๋ ๋ชฉ๋ก ํญ๋ชฉ ๋ ์ด์์ ์์ ๊ฐ๋ณ ๋ทฐ์ ์ฐธ์กฐ๋ฅผ ๋ณด์ ํฉ๋๋ค(๋ฐ๋ผ์ ์ด๋ฆ์ด '๋ทฐ ํ๋'์). ์ด๋ ๊ฒ ํ๋ฉด ์๋ก์ด ๋ฐ์ดํฐ๋ก ๋ชฉ๋ก ํญ๋ชฉ ๋ทฐ๋ฅผ ๋ ์ฝ๊ฒ ์๋ฐ์ดํธํ  ์ ์์ต๋๋ค. 



### Adapter ๋ฐ ViewHolder ์ฝ๋

```kotlin
/**
 * Adapter for the [RecyclerView] in [MainActivity]. Displays [Affirmation] data object.
 */
class ItemAdapter(
    private val context: Context,
    private val dataset: List<Affirmation>
) : RecyclerView.Adapter<ItemAdapter.ItemViewHolder>() {

    // Provide a reference to the views for each data item
    // Complex data items may need more than one view per item, and
    // you provide access to all the views for a data item in a view holder.
    // Each data item is just an Affirmation object.
    class ItemViewHolder(private val view: View) : RecyclerView.ViewHolder(view) {
        val textView: TextView = view.findViewById(R.id.item_title)
    }

    /**
     * Create new views (invoked by the layout manager)
     */
    override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): ItemViewHolder {
        // create a new view
        val adapterLayout = LayoutInflater.from(parent.context)
            .inflate(R.layout.list_item, parent, false)

        return ItemViewHolder(adapterLayout)
    }

    /**
     * Replace the contents of a view (invoked by the layout manager)
     */
    override fun onBindViewHolder(holder: ItemViewHolder, position: Int) {
        val item = dataset[position]
        holder.textView.text = context.resources.getString(item.stringResourceId)

    }

    /**
     * Return the size of your dataset (invoked by the layout manager)
     */
    override fun getItemCount() = dataset.size
}
```

+ `getItemCount()` =>  ๋ฐ์ดํฐ ์ธํธ์ ํฌ๊ธฐ๋ฅผ ๋ฐํ

  ```kotlin
  override fun getItemCount(): Int {
      return dataset.size
  }

+ `onCreateViewHolder()`

  `RecyclerView`์ ์ ๋ทฐ ํ๋๋ฅผ ๋ง๋ค๊ธฐ ์ํด ๋ ์ด์์ ๊ด๋ฆฌ์๊ฐ ํธ์ถํฉ๋๋ค(์ฌ์ฌ์ฉํ  ์ ์๋ ๊ธฐ์กด ๋ทฐ ํ๋๊ฐ ์๋ ๊ฒฝ์ฐ). ๋ทฐ ํ๋๋ ๋จ์ผ ๋ชฉ๋ก ํญ๋ชฉ ๋ทฐ๋ฅผ ๋ํ๋๋๋ค.

  + `parent` ๋งค๊ฐ๋ณ์: ์ ๋ชฉ๋ก ํญ๋ชฉ ๋ทฐ๊ฐ ํ์ ์์๋ก ์ฌ์ฉ๋์ด ์ฐ๊ฒฐ๋๋ ๋ทฐ ๊ทธ๋ฃน์๋๋ค. ์์ ์์๋ `RecyclerView`์๋๋ค.
  + `viewType` ๋งค๊ฐ๋ณ์: ๋์ผํ `RecyclerView`์ ํญ๋ชฉ ๋ทฐ ์ ํ์ด ์ฌ๋ฌ ๊ฐ ์์ ๋ ์ค์ํด์ง๋๋ค. `RecyclerView` ๋ด์ ๋ค๋ฅธ ๋ชฉ๋ก ํญ๋ชฉ ๋ ์ด์์์ด ํ์๋๋ค๋ฉด ๋ค๋ฅธ ํญ๋ชฉ ๋ทฐ ์ ํ์ด ์๋ ๊ฒ์๋๋ค. ๋์ผํ ํญ๋ชฉ ๋ทฐ ์ ํ์ ๊ฐ์ง ๋ทฐ๋ง ์ฌํ์ฉํ  ์ ์์ต๋๋ค. ์ด ๊ฒฝ์ฐ์๋ ๋ชฉ๋ก ํญ๋ชฉ ๋ ์ด์์์ด ํ๋๋ง ์๊ณ  ํญ๋ชฉ ๋ทฐ ์ ํ์ด ํ๋์ด๋ฏ๋ก ์ด ๋งค๊ฐ๋ณ์์ ๊ดํด ๊ฑฑ์ ํ  ํ์๊ฐ ์์ต๋๋ค.

  ```kotlin
   override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): ItemViewHolder {
          // create a new view
          val adapterLayout = LayoutInflater.from(parent.context)
              .inflate(R.layout.list_item, parent, false)
  
          return ItemViewHolder(adapterLayout)
      }
  ```

+ `onBindViewHolder()`

  ๋ชฉ๋ก ํญ๋ชฉ ๋ทฐ์ ์ฝํ์ธ ๋ฅผ ๋ฐ๊พธ๊ธฐ ์ํด ๋ ์ด์์ ๊ด๋ฆฌ์๊ฐ ํธ์ถํฉ๋๋ค.
  
  ```kotlin
  override fun onBindViewHolder(holder: ItemViewHolder, position: Int) {
      val item = dataset[position]
      holder.textView.text =  context.resources.getString(item.stringResourceId)
  }
  ```
  
  



### RecyclerView๋ฅผ ์ฌ์ฉํ๋๋ก MainActivity ์์ 

```kotlin
class MainActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        // Initialize data.
        val myDataset = Datasource().loadAffirmations()

        val recyclerView = findViewById<RecyclerView>(R.id.recycler_view)
        recyclerView.adapter = ItemAdapter(this, myDataset)

        // Use this setting to improve performance if you know that changes
        // in content do not change the layout size of the RecyclerView
        recyclerView.setHasFixedSize(true)
    }
}
```







## ๐ Quiz/Unit2/Pathway3

1. ์๋ ์ฝ๋๋ฅผ ์คํํ๊ธฐ ์ ์ simpleList๋ฅผ **๋ณ๊ฒฝ๊ฐ๋ฅํ**๋ชฉ๋ก์ผ๋ก ์ด๊ธฐํํด์ผ ํฉ๋๋ค.

   ```kotlin
   println(simpleList)
   simpleList.add(-5)
   simpleList.remove(4)
   println(simpleList)
   ```



2. ๋ค์ ์ค ์ฌ๋ฐ๋ฅธ ์ค๋ช์ ๋ฌด์์ธ๊ฐ์?

   => 

   + `val list = listOf(1, 2, 5)`
   + `val oddNumbers = mutableListOf("1", "9", "15")`
   + `val words: List<String> = listOf("jump", "run", "skip")`



3. `RecyclerView`์ ์ด๋ํฐ๊ฐ ํ์ํ ์ด์ ๋ ๋ฌด์์ธ๊ฐ์?

   => ์ `ViewHolders`๋ฅผ ๋ง๋ค๊ณ  ๋ฐ์ดํฐ๋ฅผ ๋ฐ์ธ๋ฉ



4. ๋ค์ ์ค `RecyclerView` ์ฌ์ฉ์ ์ด์ ์ ๋ฌด์์ธ๊ฐ์?

   => 

   + `RecyclerView`๋ ๊ธฐ๋ณธ ์ ๊ณต ๋ ์ด์์ ๊ด๋ฆฌ์์ ํจ๊ป ์ ๊ณต๋ฉ๋๋ค.
   + `RecyclerView`๋ฅผ ์ฌ์ฉํ๋ฉด ์ฒ๋ฆฌ ์๊ฐ์ ์ ์ฝํ์ฌ ๋ชฉ๋ก์ ๋์ฑ ๋ถ๋๋ฝ๊ฒ ์คํฌ๋กคํ  ์ ์์ต๋๋ค.

   + `RecyclerView`๋ ํ๋ฉด ๋ฐ์ผ๋ก ์คํฌ๋กค๋ ๋ทฐ๋ฅผ ๋ค์ ์ฌ์ฉํ์ฌ ๋ชฉ๋ก์ ํจ์จ์ฑ์ ๋์ด๋๋ก ์ค๊ณ๋์์ต๋๋ค.



5. ๋ค์ ์ค ํจํค์ง์ ๊ด๋ จํด ๋ง๋ ์ค๋ช์ ๋ฌด์์ธ๊ฐ์?

   => 

   + ํจํค์ง๋ฅผ ์ฌ์ฉํ์ฌ ์ฝ๋๋ฅผ ๊ตฌ์ฑํ  ์ ์์ต๋๋ค.
   + ๋ค๋ฅธ ํจํค์ง์ ํด๋์ค๋ฅผ ์ฌ์ฉํ๋ ค๋ฉด ์ฝ๋์์ ๋ช์์ ์ผ๋ก ๊ฐ์ ธ์์ผ ํฉ๋๋ค.
   + ํจํค์ง๋ฅผ ์ฌ์ฉํ์ฌ ๊ธฐ๋ฅ๋ณ๋ก ํด๋์ค๋ฅผ ๊ทธ๋ฃนํํ๋ ๊ฒ์ด ์ข์ต๋๋ค.



6. ์๋ง์ ์ ํ์ ๋ฆฌ์์ค ID๊ฐ ์์ฑ์์ ์ ๋ฌ๋๋๋ก ํ๋ ค๋ฉด ์ด๋ป๊ฒ ํด์ผ ํ๋์?

   => ๋ฆฌ์์ค ์ฃผ์์ ์ฌ์ฉํฉ๋๋ค



7. ์๋ ์ฝ๋์์ **```num in numbers```**์(๋) for ๋ฃจํ์ ์์ฑํ์ฌ ๋ฐํ๋ ์ถ๋ ฅ์ด ํ ์ค์ ์ซ์๊ฐ ํ๋์ฉ ์ถ๋ ฅ๋ 1~3์ ์ซ์ ๋ชฉ๋ก์ด ๋๋๋ก ํด์ผ ํฉ๋๋ค. 

   ```kotlin
   val numbers = listOf(1, 2, 3)
   for (_______) {
     println(num)
   }
   ```

 => ์๋ฌด๋ฆฌ ์๊ฐํด๋ ๋น์นธ์ num in numbers๊ฐ ๋ค์ด๊ฐ์ผ ํ๋๋ฐ ์ ํ๋ ธ๋์ง ๋ชจ๋ฅด๊ฒ ๋ค.
