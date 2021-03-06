# π₯ Unit 2 : Layouts

## Pathway 1 : Get user input in an app Part 1

## π Track 3 : Kotlinμ ν΄λμ€ λ° μμ

### Class hierarchy

+  `Vegetable`μ Kotlinμ ν΄λμ€λ‘ λ§λ€λ©΄ `Legume`μ `Vegetable` ν΄λμ€μ *νμ ν΄λμ€* λλ *μλΈν΄λμ€*λ‘ λ§λ€ μ μμ΅λλ€. μ¦, `Vegetable` ν΄λμ€μ λͺ¨λ  μμ±κ³Ό λ©μλκ° `Legume` ν΄λμ€μ μμ(μ¦, μ¬μ© κ°λ₯ν¨)λ©λλ€.

+ **μμ** : νμ ν΄λμ€κ° μμ ν΄λμ€μ **λͺ¨λ  μμ±κ³Ό λ©μλλ₯Ό ν¬ν¨νκ±°λ μμ**λ°λ κ²½μ°μλλ€. μ΄λ₯Ό ν΅ν΄ **μ½λλ₯Ό κ³΅μ νκ³  μ¬μ¬μ©**ν  μ μμ΄ νλ‘κ·Έλ¨μ λ μ½κ² νμνκ³  μ μ§ν  μ μμ΅λλ€.

  <img src = "https://user-images.githubusercontent.com/31370590/125270605-c823c200-e344-11eb-8748-8fd5840bdbd0.PNG" width = "600" height = "400">

+ μλ₯Ό λ€μ΄ Androidμλ νλ©΄μ μ§μ¬κ°ν μμ­μ λνλ΄κ³  κ·Έλ¦¬κΈ°μ μ΄λ²€νΈ μ²λ¦¬λ₯Ό λ΄λΉνλ `View` ν΄λμ€κ° μμ΅λλ€. `TextView ν΄λμ€`λ `View` ν΄λμ€μ μλΈν΄λμ€μλλ€. μ¦, `TextView`λ `View` ν΄λμ€μ λͺ¨λ  μμ±κ³Ό κΈ°λ₯μ μμλ°κ³  μ¬μ©μμκ² νμ€νΈλ₯Ό νμνλ νΉμ  λ‘μ§μ μΆκ°ν©λλ€.

+ ν λ¨κ³ λ λμκ° `EditText` λ° `Button` ν΄λμ€λ `TextView` ν΄λμ€μ νμ ν΄λμ€μλλ€. `TextView` λ° `View` ν΄λμ€μ λͺ¨λ  μμ±κ³Ό λ©μλλ₯Ό μμλ°κ³  κ³ μ ν νΉμ  λ‘μ§μ μΆκ°ν©λλ€. μλ₯Ό λ€μ΄ `EditText`λ νλ©΄μμ νμ€νΈλ₯Ό μμ ν  μ μλ μμ²΄ κΈ°λ₯μ μΆκ°ν©λλ€.

<br>

### κΈ°λ³Έ Class λ§λ€κΈ°

#### μ£Όνμ ν΄λμ€ κ³μΈ΅ κ΅¬μ‘°

<img src = "https://user-images.githubusercontent.com/31370590/125272109-6f552900-e346-11eb-9dfb-e0d3180cc974.PNG" width = "500" height = "400">

<br>

+ κ΅¬νν  ν΄λμ€
  + `Dwelling`: **λͺ¨λ  μ£Όνμ κ³΅ν΅μΌλ‘ μ μ©**λλ μ λ³΄λ₯Ό λ΄κ³  μλ κ΅¬μ²΄μ μ΄μ§ μμ μ§μ λνλ΄λ κΈ°λ³Έ ν΄λμ€μλλ€.
  + `SquareCabin`: λ°λ₯ λ©΄μ μ΄ μ μ¬κ°νμΈ λλ¬΄λ‘ λ§λ  μ μ¬κ°ν ν΅λλ¬΄μ§μλλ€.
  + `RoundHut`: λ°λ₯ λ©΄μ μ΄ μνμΈ μ§μΌλ‘ λ§λ  λ₯κ·Ό μ€λλ§μ΄κ³  `RoundTower`μ μμ μμμλλ€.
  + `RoundTower`: λ°λ₯ λ©΄μ μ΄ μνμ΄κ³  μΈ΅μ΄ μ¬λ¬ κ°μΈ λλ‘ λ§λ  λ₯κ·Ό νμμλλ€

<br>

+ μΆμ μ£Όν ν΄λμ€ 
  + ***'μΆμ' ν΄λμ€λ μμ ν κ΅¬νλμ§ μμμ μΈμ€ν΄μ€νν  μ μλ ν΄λμ€***μλλ€. μ€μΌμΉλΌκ³  μκ°νλ©΄ λ©λλ€. μ€μΌμΉλ₯Ό ν΅ν΄ λ¬΄μΈκ°μ κ΄ν μμ΄λμ΄μ κ³νμ ν΅ν©νμ§λ§ **κ·Έ λ¬΄μΈκ°λ₯Ό λΉλνκΈ°μλ μΌλ°μ μΌλ‘ μ λ³΄κ° μΆ©λΆνμ§ μμ΅λλ€.** μ€μΌμΉ(μΆμ ν΄λμ€)λ₯Ό μ¬μ©νμ¬ μ²­μ¬μ§(ν΄λμ€)μ λ§λ€κ³  μ²­μ¬μ§μ ν΅ν΄ μ€μ  κ°μ²΄ μΈμ€ν΄μ€λ₯Ό λΉλν©λλ€. 
  + μΌλ°μ μΌλ‘ **μνΌν΄λμ€λ₯Ό λ§λ€μ΄ μ’μ μ μ λͺ¨λ  μλΈν΄λμ€μ κ³΅ν΅μ μΈ μμ±κ³Ό ν¨μλ₯Ό ν¬ν¨νλ€λ κ²**μλλ€. μμ±κ°κ³Ό ν¨μ κ΅¬νμ μ μ μμΌλ©΄ ν΄λμ€λ₯Ό μΆμμΌλ‘ λ§λ­λλ€. μλ₯Ό λ€μ΄ `Vegetables`μλ λͺ¨λ  μ±μμ μΌλ°μ μΈ μ¬λ¬ μμ±μ΄ μμ§λ§ κ΅¬μ²΄μ μ΄μ§ μμ μ±μμ μΈμ€ν΄μ€λ₯Ό λ§λ€ μλ μμ΅λλ€. λͺ¨μμ΄λ μμ λ±μ λͺ¨λ₯΄κΈ° λλ¬Έμλλ€. λ°λΌμ `Vegetable`μ **`κ° μ±μμ κ΄ν κ΅¬μ²΄μ μΈ μΈλΆμ λ³΄μ κ²°μ μ μλΈν΄λμ€μ λ§‘κΈ°λ μΆμ ν΄λμ€**μλλ€. 
  + μΆμ ν΄λμ€ μ μΈμ `abstract` ν€μλλ‘ μμν©λλ€.

<br>

+ `Dwelling` class

  ```kotlin
  abstract class Dwelling(private var residents: Int) {
  
     abstract val buildingMaterial: String
     abstract val capacity: Int
  
     fun hasRoom(): Boolean {
         return residents < capacity
     }
  }
  ```

  + μ΄ `Dwelling` ν΄λμ€μμ **μ£Όνλ§λ€ λ€λ₯Ό μ μλλΌλ λͺ¨λ  μ£Όνμ μ μ©λλ ν­λͺ©**μ μ μν©λλ€. λͺ¨λ  μ£Όνμ κ±΄μΆ μμ¬λ‘ λ§λ€μ΄μ§λλ€. `Dwelling` λ΄μμ κ±΄μΆ μμ¬λ₯Ό λνλ΄λ `String` μ νμ `buildingMaterial` λ³μλ₯Ό λ§λ­λλ€. κ±΄μΆ μμ¬λ λ³κ²½λμ§ μμΌλ―λ‘ `val`μ μ¬μ©νμ¬ λ³κ²½ λΆκ°λ₯ν λ³μλ‘ λ§λ­λλ€.
  + λͺ¨λ  μ£Όνμλ μ£Όνμ κ±°μ£Όνλ μ¬λ¬ `residents`(`capacity` μ΄νμΌ μ μμ)κ° μμΌλ―λ‘ λͺ¨λ  μλΈν΄λμ€κ° μμλ°μ μ¬μ©νλλ‘ `Dwelling` μνΌν΄λμ€μμ `residents` μμ±μ μ μν©λλ€. `residents`λ₯Ό `Dwelling` ν΄λμ€μ μμ±μμ μ λ¬λλ λ§€κ°λ³μλ‘ λ§λ€ μ μμ΅λλ€. `residents` μμ±μ `var`μλλ€. μΈμ€ν΄μ€κ° λ§λ€μ΄μ§ ν κ±°μ£Όμ μκ° λ³κ²½λ  μ μκΈ° λλ¬Έμλλ€. 
    + μ£Όνμ `capacity`μ νμ¬ `residents` μκ° λͺ¨λ μ μλ μνμμ μ£Όνμ λ λ€λ₯Έ κ±°μ£Όμλ₯Ό μν κ³΅κ°μ΄ μλμ§ νμΈνλ `hasRoom()` ν¨μλ₯Ό λ§λ€ μ μμ΅λλ€. `Dwelling` ν΄λμ€μμ `hasRoom()` ν¨μλ₯Ό μ μνκ³  κ΅¬ννλ©΄ λ©λλ€. κ³΅κ°μ΄ μλμ§ κ³μ°νλ κ³΅μμ΄ λͺ¨λ  μ£Όνμ λμΌνκΈ° λλ¬Έμλλ€. `residents` μκ° `capacity`λ³΄λ€ μ μΌλ©΄ `Dwelling`μ κ³΅κ°μ΄ μκ³  ν¨μλ μ΄ λΉκ΅μ κΈ°λ°νμ¬ `true`λ `false`λ₯Ό λ°νν΄μΌ ν©λλ€.

   <br>

### Sub class λ§λ€κΈ°

```kotlin
abstract class Dwelling(private var residents: Int) {
    abstract val buildingMaterial: String
    abstract val capacity: Int

    fun hasRoom(): Boolean {
       return residents < capacity
   }
}

class SquareCabin(residents: Int) : Dwelling(residents) {
    override val buildingMaterial = "Wood"
    override val capacity = 6
}

fun main() {
    val squareCabin = SquareCabin(6)

    println("\nSquare Cabin\n============")
    println("Capacity: ${squareCabin.capacity}")
    println("Material: ${squareCabin.buildingMaterial}")
    println("Has room? ${squareCabin.hasRoom()}")
}
```

+ withλ₯Ό μ¬μ©νμ¬ μ½λ λ¨μν

  ν΄λμ€μ νΉμ  μΈμ€ν΄μ€λ‘ μμνκ³  μ΄ μΈμ€ν΄μ€μ μ¬λ¬ μμ±κ³Ό ν¨μμ μ‘μΈμ€ν΄μΌ νλ€λ©΄ `with` λ¬Έμ μ¬μ©νμ¬ **μ΄ μΈμ€ν΄μ€ κ°μ²΄λ‘ λ€μ μμμ λͺ¨λ μ€ν**νλΌκ³  λνλΌ μ μμ΅λλ€. `with` ν€μλλ‘ μμνκ³  κ΄νΈλ‘ λ¬ΆμΈ μΈμ€ν΄μ€ μ΄λ¦, μ€ννλ €λ μμμ΄ ν¬ν¨λ μ€κ΄νΈκ° μ°¨λ‘λ‘ μ΄μ΄μ§λλ€.

  ```kotlin
  with (instanceName) {
      // all operations to do with instanceName
  }
  ```

  ```kotlin
  with(squareCabin) {
      println("\nSquare Cabin\n============")
      println("Capacity: ${capacity}")
      println("Material: ${buildingMaterial}")
      println("Has room? ${hasRoom()}")
  }
  ```

  <br>

+ RoundHut subclass

  ```kotlin
  fun main() {
      val roundHut = RoundHut(3)
      
      with(roundHut) {
      println("\nRound Hut\n=========")
      println("Material: ${buildingMaterial}")
      println("Capacity: ${capacity}")
      println("Has room? ${hasRoom()}")
      }
  }   
  
  class RoundHut(residents: Int) : Dwelling(residents) {
      override val buildingMaterial = "Straw"
      override val capacity = 4
  }
  ```

  <br>

+ RoundTower subclass

  ```kotlin
  class RoundTower(residents: Int) : RoundHut(residents) {
      override val buildingMaterial = "Stone"
      override val capacity = 4
  }
  ```

  μ΄ μ½λλ₯Ό μ€ννλ©΄ μ€λ₯κ° λ°μνλ€. 

  ```kotlin
  This type is final, so it cannot be inherited from
  ```

  μ΄ μ€λ₯λ `RoundHut` ν΄λμ€λ₯Ό μλΈν΄λμ€λ‘ λΆλ₯νκ±°λ μμν  μ μμμ μλ―Έν©λλ€. **κΈ°λ³Έμ μΌλ‘ Kotlinμμ ν΄λμ€λ `final` ν΄λμ€μ΄λ©° μλΈν΄λμ€λ‘ λΆλ₯ν  μ μμ΅λλ€.** `abstract` ν΄λμ€λ `open` ν€μλλ‘ νμλ ν΄λμ€μμλ§ μμν  μ μμ΅λλ€. λ°λΌμ μμλ  μ μλλ‘ `RoundHut` ν΄λμ€λ₯Ό `open` ν€μλλ‘ νμν΄μΌ ν©λλ€.

  `RoundHut` μ μΈ μμ λΆλΆμ `open` ν€μλλ₯Ό μΆκ°ν©λλ€.

  ```kotlin
  open class RoundHut(residents: Int) : Dwelling(residents) {
     override val buildingMaterial = "Straw"
     override val capacity = 4
  }
  ```

  <br>

  μ¬λ¬ μΈ΅μ΄ μλλ‘ `RoundTower`λ₯Ό μμ νκ³  μΈ΅μμ λ°λΌ μμ© μΈμμ μ‘°μ ν©λλ€.

  ```kotlin
  class RoundTower(
      residents: Int,
      val floors: Int = 2) : RoundHut(residents) {
  
      override val buildingMaterial = "Stone"
      override val capacity = 4 * floors
  }
  ```

<br>

<br>

### κ³μΈ΅ κ΅¬μ‘°μ ν΄λμ€ μμ 

+ Dwelling  ν΄λμ€μμ floorArea() μ μ

  ```kotlin
  abstract class Dwelling(private var residents: Int) {
      abstract val buildingMaterial: String
      abstract val capacity: Int
  
      fun hasRoom(): Boolean {
         return residents < capacity
     }
      
      abstract fun floorArea(): Double
  }
  ```

  + μΆμ ν΄λμ€μμ μ μλ λͺ¨λ  `abstract` λ©μλλ μΆμ ν΄λμ€μ μλΈν΄λμ€μμ κ΅¬νλμ΄μΌ ν©λλ€. μ½λλ₯Ό μ€ννλ €λ©΄ λ¨Όμ  μλΈν΄λμ€μμ `floorArea()`λ₯Ό κ΅¬νν΄μΌ ν©λλ€.

<br>

+ SquareCabinμ floorArea() κ΅¬ν

  ```kotlin
  class SquareCabin(residents: Int, val length: Double) : Dwelling(residents) {
      
      override fun floorArea(): Double {
      return length * length
      }
  }
  ```

<br>

+ RoundHutμ floorArea() κ΅¬ν

  ```kotlin
  open class RoundHut(
     val residents: Int,
     val radius: Double) : Dwelling(residents) {
      
      override fun floorArea(): Double {
      return PI * radius * radius
      }
  }
  ```

<br>

+ RoundTowerμ floorArea() κ΅¬ν

  ```kotlin
  class RoundTower(residents: Int, radius: Double,
      val floors: Int = 2) : RoundHut(residents, radius) {
  
      override val buildingMaterial = "Stone"
      override val capacity = 4 * floors
  
      override fun floorArea(): Double {
          return super.floorArea() * floors
      }
  }
  ```

  <br>

<br>

+ μ΅μ’ μ½λ

  ```kotlin
  /**
  * Program that implements classes for different kinds of dwellings.
  * Shows how to:
  * Create class hierarchy, variables and functions with inheritance,
  * abstract class, overriding, and private vs. public variables.
  */
  
  import kotlin.math.PI
  import kotlin.math.sqrt
  
  fun main() {
     val squareCabin = SquareCabin(6, 50.0)
     val roundHut = RoundHut(3, 10.0)
     val roundTower = RoundTower(4, 15.5)
  
     with(squareCabin) {
         println("\nSquare Cabin\n============")
         println("Capacity: ${capacity}")
         println("Material: ${buildingMaterial}")
         println("Floor area: ${floorArea()}")
     }
  
     with(roundHut) {
         println("\nRound Hut\n=========")
         println("Material: ${buildingMaterial}")
         println("Capacity: ${capacity}")
         println("Floor area: ${floorArea()}")
         println("Has room? ${hasRoom()}")
         getRoom()
         println("Has room? ${hasRoom()}")
         getRoom()
         println("Carpet size: ${calculateMaxCarpetSize()}")
     }
  
     with(roundTower) {
         println("\nRound Tower\n==========")
         println("Material: ${buildingMaterial}")
         println("Capacity: ${capacity}")
         println("Floor area: ${floorArea()}")
         println("Carpet size: ${calculateMaxCarpetSize()}")
     }
  }
  
  /**
  * Defines properties common to all dwellings.
  * All dwellings have floorspace,
  * but its calculation is specific to the subclass.
  * Checking and getting a room are implemented here
  * because they are the same for all Dwelling subclasses.
  *
  * @param residents Current number of residents
  */
  abstract class Dwelling(private var residents: Int) {
     abstract val buildingMaterial: String
     abstract val capacity: Int
  
     /**
      * Calculates the floor area of the dwelling.
      * Implemented by subclasses where shape is determined.
      *
      * @return floor area
      */
     abstract fun floorArea(): Double
  
     /**
      * Checks whether there is room for another resident.
      *
      * @return true if room available, false otherwise
      */
     fun hasRoom(): Boolean {
         return residents < capacity
     }
  
     /**
      * Compares the capacity to the number of residents and
      * if capacity is larger than number of residents,
      * add resident by increasing the number of residents.
      * Print the result.
      */
     fun getRoom() {
         if (capacity > residents) {
             residents++
             println("You got a room!")
         } else {
             println("Sorry, at capacity and no rooms left.")
         }
     }
  
     }
  
  /**
  * A square cabin dwelling.
  *
  *  @param residents Current number of residents
  *  @param length Length
  */
  class SquareCabin(residents: Int, val length: Double) : Dwelling(residents) {
     override val buildingMaterial = "Wood"
     override val capacity = 6
  
     /**
      * Calculates floor area for a square dwelling.
      *
      * @return floor area
      */
     override fun floorArea(): Double {
         return length * length
     }
  
  }
  
  /**
  * Dwelling with a circular floorspace
  *
  * @param residents Current number of residents
  * @param radius Radius
  */
  open class RoundHut(
         val residents: Int, val radius: Double) : Dwelling(residents) {
  
     override val buildingMaterial = "Straw"
     override val capacity = 4
  
     /**
      * Calculates floor area for a round dwelling.
      *
      * @return floor area
      */
     override fun floorArea(): Double {
         return PI * radius * radius
     }
  
     /**
      *  Calculates the max length for a square carpet
      *  that fits the circular floor.
      *
      * @return length of carpet
      */
     fun calculateMaxCarpetSize(): Double {
         val diameter = 2 * radius
         return sqrt(diameter * diameter / 2)
     }
  
  }
  
  /**
  * Round tower with multiple stories.
  *
  * @param residents Current number of residents
  * @param radius Radius
  * @param floors Number of stories
  */
  class RoundTower(
         residents: Int,
         radius: Double,
         val floors: Int = 2) : RoundHut(residents, radius) {
  
     override val buildingMaterial = "Stone"
  
     // Capacity depends on the number of floors.
     override val capacity = floors * 4
  
     /**
      * Calculates the total floor area for a tower dwelling
      * with multiple stories.
      *
      * @return floor area
      */
     override fun floorArea(): Double {
         return super.floorArea() * floors
     }
  }
  ```

<br>

<br>

----

## ν κ³μ°κΈ° app

## π Track 4 : Androidμ XML λ μ΄μμ λ§λ€κΈ°

### XML μ½κΈ° λ° μ΄ν΄

+ μ΄λ―Έ μ΅μν **Layout Editor**λ₯Ό μ¬μ©νλ λμ  UIλ₯Ό μ€λͺνλ **XML**μ μμ νμ¬ μ νλ¦¬μΌμ΄μμ λ μ΄μμμ λΉλν©λλ€. XMLμ *νμ₯μ± λ§ν¬μ μΈμ΄(eXtensible Markup Language)* λ₯Ό μλ―Ένλ©° νμ€νΈ κΈ°λ° λ¬Έμλ₯Ό μ¬μ©νμ¬ λ°μ΄ν°λ₯Ό μ€λͺνλ λ°©λ²μλλ€. XMLμ νμ₯ κ°λ₯νκ³  λ§€μ° μ μ°νλ―λ‘ Android μ±μ UI λ μ΄μμ μ μλ₯Ό λΉλ‘―νμ¬ λ€μν μ©λλ‘ μ¬μ©λ©λλ€. μ±μ λ¬Έμμ΄κ³Ό κ°μ λ€λ₯Έ λ¦¬μμ€λ `strings.xml`μ΄λΌλ XML νμΌμ μ μλλ€κ³  μ΄μ  Codelabμμ μμλ΄€μ΅λλ€.

+ κ° UI μμλ XML νμΌμ XML *μμ*λ‘ ννλ©λλ€. κ° μμλ νκ·Έλ‘ μμνκ³  λλλ©° κ° νκ·Έλ `<`λ‘ μμνκ³  `>`λ‘ λλ©λλ€. **Layout Editor(λμμΈ)**λ₯Ό μ¬μ©νμ¬ UI μμμμ μμ±μ μ€μ ν  μ μλ κ²μ²λΌ XML μμμλ *μμ±*μ΄ μμ μ μμ΅λλ€. κ°λ¨ν λ§ν΄μ μ UI μμμ XMLμ λ€μκ³Ό κ°μ μ μμ΅λλ€. 

  ```kotlin
  <androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android">
  
  </androidx.constraintlayout.widget.ConstraintLayout>
  ```

+ `ConstraintLayout` νκ·Έλ₯Ό λ³΄λ©΄ `TextView`μ κ°μ΄ `ConstraintLayout`λ§μ΄ μλ `androidx.constraintlayout.widget.ConstraintLayout`μ΄λΌκ³  νμλ©λλ€. μ΄λ `ConstraintLayout`μ΄ ν΅μ¬ Android νλ«νΌ μΈμλ μΆκ° κΈ°λ₯μ μ κ³΅νλ μ½λ λΌμ΄λΈλ¬λ¦¬κ° ν¬ν¨λ **Android Jetpackμ μΌλΆ**μ΄κΈ° λλ¬Έμλλ€. Jetpackμλ μ±μ λ μ½κ² λΉλνλ λ° νμ©ν  μ μλ μ μ©ν κΈ°λ₯μ΄ μμ΅λλ€. μ΄ UI κ΅¬μ±μμλ **'androidx'λ‘ μμ**νλ―λ‘ **Jetpackμ μΌλΆ**μΈ κ²μ μ μ μμ΅λλ€.

+ `xmlns`λ **XML λ€μμ€νμ΄μ€**λ₯Ό λνλ΄κ³  κ° μ€μ **μ€ν€λ§**λ μ΄λ¬ν λ¨μ΄μ κ΄λ ¨λ μμ±μ μ΄νλ₯Ό μ μν©λλ€. μλ₯Ό λ€μ΄ `android:` λ€μμ€νμ΄μ€λ Android μμ€νμμ μ μν μμ±μ νμν©λλ€. λ μ΄μμ XMLμ μμ±μ λͺ¨λ μ΄λ¬ν λ€μμ€νμ΄μ€ μ€ νλλ‘ μμν©λλ€. 

+ `ConstraintLayout`μ UI μμμλ `match_parent`λ₯Ό μ€μ ν  μ μμ΅λλ€. 

<br>

### XMLλ‘ λ μ΄μμ λΉλ

+ `RadioGroup`
+ `RadioButton`
+ `Switch`
+ 'start' λ° 'end' μ μ½ μ‘°κ±΄μ μ¬μ©νμ¬ μΌμͺ½μμ μ€λ₯Έμͺ½(LTR) λ° μ€λ₯Έμͺ½μμ μΌμͺ½(RTL) λ°©ν₯ μΈμ΄λ₯Ό λͺ¨λ μ²λ¦¬ν©λλ€.
+ `View`μ λλΉλ₯Ό ν¬ν¨λλ `ConstraintLayout`μ λλΉμ κ°κ² νλ €λ©΄ μμκ³Ό λμ μμ μμμ μμκ³Ό λμΌλ‘ μ ννκ³  λλΉλ₯Ό 0dpλ‘ μ€μ ν©λλ€.

<br>

<br>

## π Track 5: ν κ³μ°

### View Binding

+ `findViewById()` λ°©μμ ν¨κ³Όμ μ΄μ§λ§ μ±μ λ·°λ₯Ό λ λ§μ΄ μΆκ°νκ³  UIκ° λ λ³΅μ‘ν΄μ§μ λ°λΌ `findViewById()`λ₯Ό μ¬μ©νλ κ²μ΄ λ²κ±°λ‘μμ§ μ μμ΅λλ€. Androidλ **View Binding**μ΄λΌλ κΈ°λ₯μ μ κ³΅ν©λλ€. μ¬μ μ μ‘°κΈλ§ λ μμνλ©΄ λ·° κ²°ν©μ ν΅ν΄ UIμ λ·°μμ λ©μλλ₯Ό ν¨μ¬ λ μ½κ³  λΉ λ₯΄κ² νΈμΆν  μ μμ΅λλ€. Gradleμμ μ±μ λ·° κ²°ν©μ μ¬μ© μ€μ νκ³  λͺ κ°μ§ μ½λλ₯Ό λ³κ²½ν΄μΌ ν©λλ€.

+ λ€μμ μ½λλ₯Ό `build.gradle` νμΌμ `android` μΉμμ μΆκ°ν©λλ€. 

  ```kotlin
  buildFeatures {
          viewBinding = true
      }

<br>

### κ²°ν© κ°μ²΄ μ΄κΈ°ν

<img src = "https://user-images.githubusercontent.com/31370590/125413956-9674fa02-f7ac-4de5-a4f0-bdcd9435ece9.PNG " width = "560" height = "400">

+ μ±μ κ° `View`λ§λ€ `findViewById()`λ₯Ό νΈμΆνλ λμ , κ²°ν© κ°μ²΄λ₯Ό ν λ² λ§λ€κ³  μ΄κΈ°νν©λλ€.  μ¦,  `MainActivity`κ° λ·° κ²°ν©μ μ¬μ©νλλ‘ μ€μ ν©λλ€.

  ```kotlin
  class MainActivity : AppCompatActivity() {
  
      lateinit var binding: ActivityMainBinding
  
      override fun onCreate(savedInstanceState: Bundle?) {
          super.onCreate(savedInstanceState)
          binding = ActivityMainBinding.inflate(layoutInflater)
          setContentView(binding.root)
      }
  }
  ```

  + `lateinit var binding: ActivityMainBinding`

    `lateinit` ν€μλλ μλ‘μ΄ ν€μλλ‘, **μ½λκ° λ³μλ₯Ό μ¬μ©νκΈ° μ μ λ¨Όμ  μ΄κΈ°νν  κ²μμ νμΈ**ν΄ μ€λλ€. νλ‘νΌν° μ΄κΈ°νλ₯Ό λ―Έλ£¨λ κ². λ³μλ₯Ό μ΄κΈ°ννμ§ μμΌλ©΄ μ±μ΄ λΉμ μ μ’λ£λ©λλ€.

  <br>

  + `binding = ActivityMainBinding.inflate(layoutInflater)`

     `activity_main.xml` λ μ΄μμμμ `Views`μ μ‘μΈμ€νλ λ° μ¬μ©ν  `binding` κ°μ²΄λ₯Ό μ΄κΈ°νν©λλ€.

  <br>

  + `setContentView(binding.root)`

    νλμ μ½νμΈ  λ·°λ₯Ό μ€μ ν©λλ€. λ€μ μ½λλ λ μ΄μμμ λ¦¬μμ€ IDμΈ `R.layout.activity_main`μ μ λ¬νλ λμ , μ±μ λ·° κ³μΈ΅ κ΅¬μ‘° λ£¨νΈμΈ `binding.root`λ₯Ό μ§μ ν©λλ€.

  <br>

+ μ΄μ  μ±μμ `View`μ λν μ°Έμ‘°κ° νμν κ²½μ° `findViewById()`λ₯Ό νΈμΆνλ λμ  `binding` κ°μ²΄μμ λ·° μ°Έμ‘°λ₯Ό κ°μ Έμ¬ μ μμ΅λλ€. `binding` κ°μ²΄λ IDκ° μλ μ±μ λͺ¨λ  `View`λ₯Ό μν μ°Έμ‘°λ₯Ό μλμΌλ‘ μ μν©λλ€. λ·° κ²°ν©μ μ¬μ©νλ κ²μ΄ ν¨μ¬ λ κ°κ²°ν΄μ `View`λ₯Ό μν μ°Έμ‘°λ₯Ό μ μ§ν  λ³μλ₯Ό λ§λ€ νμμ‘°μ°¨ μμΌλ©° κ²°ν© κ°μ²΄μμ μ§μ  λ·° μ°Έμ‘°λ₯Ό μ¬μ©νκΈ°λ§ νλ©΄ λ©λλ€.

  ```kotlin
  // Old way with findViewById()
  val myButton: Button = findViewById(R.id.my_button)
  myButton.text = "A button"
  
  // Better way with view binding
  val myButton: Button = binding.myButton
  myButton.text = "A button"
  
  // Best way with view binding and no extra variable
  binding.myButton.text = "A button"
  ```

  <br>

> Binding classμ μ΄λ¦μ XML νμΌμ μ΄λ¦μ μΉ΄λ© νκΈ°λ²μΌλ‘ λ³ννκ³  μ΄λ¦ λμ 'Binding'μ μΆκ°νμ¬ μμ±λ©λλ€. λ§μ°¬κ°μ§λ‘ κ° λ·°λ₯Ό μν μ°Έμ‘°λ λ°μ€μ μ­μ νκ³  λ·° μ΄λ¦μ μΉ΄λ© νκΈ°λ²μΌλ‘ λ³ννμ¬ μμ±λ©λλ€. μλ₯Ό λ€μ΄ `activity_main.xml`μ `ActivityMainBinding`μ΄ λκ³  `binding.textView`λ‘ `@id/text_view`μ μ‘μΈμ€ν  μ μμ΅λλ€.

<br>

<br>

### ν κ³μ°

```kotlin
fun calculateTip() {
        val stringInTextField = binding.costOfService.text.toString()
        val cost  =  stringInTextField.toDouble()

        val selectedId = binding.tipOptions.checkedRadioButtonId

        val tipPercentage = when (selectedId) {
            R.id.option_twenty_percent -> 0.20
            R.id.option_eighteen_percent -> 0.18
            else -> 0.15
        }

        var tip = tipPercentage * cost

        val roundUp = binding.roundUpSwitch.isChecked
        if (roundUp) {
            tip = kotlin.math.ceil(tip)
        }

        val formattedTip = NumberFormat.getCurrencyInstance().format(tip)

        binding.tipResult.text = getString(R.string.tip_amount, formattedTip)

    }
```

<br>

<br>

### νμ€νΈ λ° λλ²κ·Έ

+ `calculateTip()` λ©μλμμ μ λ³΄κ° μ±μ ν΅ν΄ μ΄λ»κ² μ΄λνλμ§μ κ° λ¨κ³μμ μ΄λ€ λ¬Έμ κ° λ°μν  μ μμμ§ 


<br>

+ null

  + *Null*μ 'κ° μμ'μ μλ―Ένλ νΉμ κ°μΌλ‘, κ°μ΄ `0.0`μΈ `Double` λλ λ¬Έμ μκ° 0κ°μΈ λΉ `String`(μ¦, `""`)κ³Όλ λ€λ¦λλ€. `Null`μ κ°μ΄ μκ±°λ `Double`μ΄ μκ±°λ `String`μ΄ μμμ μλ―Έν©λλ€. λ§μ λ©μλκ° κ°μ μμνκ³  `null`μ μ²λ¦¬νλ λ°©λ²μ λͺ°λΌμ μ€μ§λ©λλ€. μ¦, μ±μ΄ λΉμ μ μ’λ£λ©λλ€. λ°λΌμ Kotlinμ `null`μ΄ μ¬μ©λλ μμΉλ₯Ό μ ννλ €κ³  ν©λλ€.
  + μ±μ `toDoubleOrNull()`μμ `null`μ΄ λ°νλλμ§ νμΈνμ¬ nullμ΄ λ°νλλ κ²½μ° λ€λ₯Έ λ°©μμΌλ‘ μ²λ¦¬ν  μ μμ΅λλ€. λ°λΌμ μ±μ΄ λΉμ μ μ’λ£λμ§ μμ΅λλ€.
  + `val cost = stringInTextField.toDoubleOrNull()` λ‘ λ³κ²½νκ³ , μ΄ μ½λ μ€ λ€μ `cost`κ° `null`μΈμ§ νμΈνκ³  κ·Έλ λ€λ©΄ λ©μλμμ λ°νλλ λ¬Έμ μΆκ°ν©λλ€. `return` λͺλ Ήμ λλ¨Έμ§ λͺλ Ήμ μ€ννμ§ μκ³  λ©μλλ₯Ό μ’λ£νλ κ²μ μλ―Έν©λλ€. λ©μλκ° κ°μ λ°νν΄μΌ νλ κ²½μ° ννμμμ `return` λͺλ Ήμ μ¬μ©νμ¬ κ° λ°νμ μ§μ ν©λλ€. 

  ```kotlin
  val cost = stringInTextField.toDoubleOrNull()
  
  if (cost == null) {
      return
  }
  ```


<br>

<br>

### Good coding practice

+ μ½λ κ²μ¬

  **Analyze > Inspect Code... > **

  => privateμΌλ‘ μ€μ  κ°λ₯

 



## Quiz/Unit2/Pathway1

1. Which of the following is true about class inheritance?

   => 

   + Class inheritance lets you reuse code and makes your program easier to maintain.
   + Properties and functions of the parent class(es) are available to the child class.
   + You can define additional properties and functions that are specific to subclasses.
   + You can override parent class members in subclasses.



2. Which of the following are true about abstract classes?

   => 

   + They can be extended by subclasses and implementations can be provided for abstract members of the class.
   + They may have abstract properties or abstract functions.
   + They are not fully implemented and cannot be instantiated.



3. The  **constructor**  is called when you create an instance of a class.



4. How do you mark a property to be used only inside its current class?

   =>  Use the `private` keyword.



5. Select all answers that are true for this XML layout when displayed on the screen.

   ```kotlin
   <androidx.constraintlayout.widget.ConstraintLayout
       android:layout_width="match_parent"
       android:layout_height="match_parent">
       <TextView
           android:id="@+id/textViewA"
           android:layout_width="wrap_content"
           android:layout_height="wrap_content"
           android:text="A"
           app:layout_constraintStart_toStartOf="parent"
           app:layout_constraintTop_toTopOf="parent" />
       <TextView
           android:id="@+id/textViewB"
           android:layout_width="wrap_content"
           android:layout_height="wrap_content"
           android:text="B"
           app:layout_constraintEnd_toEndOf="parent"
           app:layout_constraintTop_toTopOf="parent" />
   </androidx.constraintlayout.widget.ConstraintLayout>
   ```

   => 

   + The starting edge of `TextView A` is aligned to the starting edge of the parent view.
   + The tops of `TextView A` and `TextView B` are aligned to top of the parent view.

