# ๐ฅ Unit 1 : Kotlin basics

## PATHWAY 4 : Add a button to an app

<br>

## ๐ Track 1 : Classes and object instances in Kotlin 

###  ํ์ตํ  ๋ด์ฉ

+ ํ๋ก๊ทธ๋๋งคํฑ ๋ฐฉ์์ผ๋ก ๋๋ค ์ซ์๋ฅผ ์์ฑํ์ฌ ์ฃผ์ฌ์ ๊ตด๋ฆฌ๊ธฐ๋ฅผ ์๋ฎฌ๋ ์ด์ํ๋ ๋ฐฉ๋ฒ
+ ๋ณ์์ ๋ฉ์๋๋ก `Dice` ํด๋์ค๋ฅผ ๋ง๋ค์ด ์ฝ๋๋ฅผ ๊ตฌ์กฐํํ๋ ๋ฐฉ๋ฒ
+ ํด๋์ค์ ๊ฐ์ฒด ์ธ์คํด์ค๋ฅผ ๋ง๋ค๊ณ  ๋ณ์๋ฅผ ์์ ํ๋ฉฐ ๋ฉ์๋๋ฅผ ํธ์ถํ๋ ๋ฐฉ๋ฒ

<br>

### ๋๋ค ์ซ์ ๊ตด๋ฆฌ๊ธฐ

+  `IntRange`๋ ๋ ๋ค๋ฅธ ๋ฐ์ดํฐ ์ ํ์ผ๋ก, ์์์ ๋ถํฐ ๋์ ๊น์ง ์ ์์ ๋ฒ์๋ฅผ ๋ํ๋๋๋ค. `1..6`์ Kotlin ๋ฒ์์ธ ๊ฒ์ ์ ์ ์์ต๋๋ค. ์์ ์ซ์, ์  ๋ ๊ฐ, ๋ ์ซ์๊ฐ ์์๋๋ก ์๊ธฐ ๋๋ฌธ์๋๋ค(์ฌ์ด์ ๊ณต๋ฐฑ ์์). ์ ์ ๋ฒ์์ ๋ค๋ฅธ ์๋ก๋ ์ซ์ 2~5์ `2..5`, ์ซ์ 100~200์ `100..200`์ด ์์ต๋๋ค.

+ `main()` ๋ด์์ ๋ณ์๋ฅผ `randomNumber`๋ผ๋ `val`๋ก ์ ์ํ๊ณ ,   **`randomNumber`๊ฐ `diceRange` ๋ฒ์์์ `random()`๋ฅผ ํธ์ถํ ๊ฒฐ๊ณผ ๊ฐ์ ๊ฐ๋๋ก** ํฉ๋๋ค.

```kotlin
fun main() {
    val diceRange = 1..6
    val randomNumber = diceRange.random()
    // ๋ฒ์์์ ํจ์๋ฅผ ์ง์  ํธ์ถํด๋ ๋ฉ๋๋ค(์: `(1..6).random()`).
    
    println("Random number : ${randomNumber}")
}
```

<br>

### Dice class ๋ง๋ค๊ธฐ

```kotlin
fun main() {
    val myFirstDice = Dice()
    println(myFirstDice.sides)
    myFirstDice.roll()
}

class Dice {
    var sides = 6

    fun roll() {
        val randomNumber = (1..6).random()
        println(randomNumber)
    }
}
```

<br>

### ์ฃผ์ฌ์ ๊ตด๋ฆฌ๊ธฐ ๊ฐ ๋ฐํ, ์ฃผ์ฌ์์ ๋ฉด ์ ๋ณ๊ฒฝ

```kotlin
fun main() {
    val myFirstDice = Dice()
    val diceRoll = myFirstDice.roll()
    println("Your ${myFirstDice.sides} sided dice rolled ${diceRoll}!")

    myFirstDice.sides = 20
    println("Your ${myFirstDice.sides} sided dice rolled ${myFirstDice.roll()}!")
}

class Dice {
    var sides = 6

    fun roll(): Int {
        val randomNumber = (1..sides).random()
        return randomNumber
    }
}
```

<br>

### ์ฃผ์ฌ์ ๋ง์ถค์ค์ 

```kotlin
fun main() {
    val myFirstDice = Dice(6)
    val diceRoll = myFirstDice.roll()
    println("Your ${myFirstDice.numSides} sided dice rolled ${diceRoll}!")

    val mySecondDice = Dice(20)
    println("Your ${mySecondDice.numSides} sided dice rolled ${mySecondDice.roll()}!")
}

class Dice (val numSides: Int) {
    fun roll(): Int {
        val randomNumber = (1..numSides).random()
        return randomNumber
        // return (1..numSides).random() 
    }
}
```

<br>

### ์์ฝ

+ `IntRange`์์ `random()` ํจ์๋ฅผ ํธ์ถํ์ฌ ๋๋ค ์ซ์๋ฅผ ์์ฑํฉ๋๋ค. `(1..6).random()`
+ ํด๋์ค๋ ๊ฐ์ฒด์ ์ฒญ์ฌ์ง๊ณผ ๊ฐ์ต๋๋ค. ๋ณ์์ ํจ์๋ก ๊ตฌํ๋ ์์ฑ๊ณผ ๋์์ ํฌํจํ  ์ ์์ต๋๋ค.
+ ํด๋์ค ์ธ์คํด์ค๋ ์ฃผ์ฌ์์ ๊ฐ์ ์ค์  ๊ฐ์ฒด๋ฅผ ๋ํ๋ด๋ ๊ฒฝ์ฐ๊ฐ ๋ง์ต๋๋ค. ๊ฐ์ฒด์์ ์์์ ํธ์ถํ๊ณ  ์์ฑ์ ๋ณ๊ฒฝํ  ์ ์์ต๋๋ค.
+ ์ธ์คํด์ค๋ฅผ ๋ง๋ค ๋ ๊ฐ์ ํด๋์ค์ ์ ๊ณตํ  ์ ์์ต๋๋ค. ์๋ฅผ ๋ค์ด `class Dice(val numSides: Int)` ๋ค์์ `Dice(6)`๋ก ์ธ์คํด์ค๋ฅผ ๋ง๋ญ๋๋ค.
+ ํจ์์์ ๋ฌด์ธ๊ฐ๋ฅผ ๋ฐํํ  ์ ์์ต๋๋ค. ํจ์ ์ ์์์ ๋ฐํํ  ๋ฐ์ดํฐ ์ ํ์ ์ง์ ํ๊ณ  ํจ์ ๋ณธ๋ฌธ์์ `return` ๋ฌธ์ ์ฌ์ฉํ์ฌ ๋ฌด์ธ๊ฐ๋ฅผ ๋ฐํํฉ๋๋ค. ์: `fun example(): Int { return 5 }`

<br>

## ๐ Track 2 : Create an interactive Dice Roller app

### ์ฑ ๋ ์ด์์ ๋ง๋ค๊ธฐ

+ ๋๊ตฌ ์์ด์ฝ์ด ์๋ **text** ์์ฑ์ ๊ฐ๋ฐ์๋ง์ ์ํ '๋๊ตฌ ํ์คํธ' ์์ฑ์๋๋ค.  `TextView`์์ ๋๊ตฌ ํ์คํธ๋ฅผ '1'๋ก ์ค์ ํฉ๋๋ค(์ฃผ์ฌ์ ๊ตด๋ฆฌ๊ธฐ ๊ฐ 1์ด ์๋ค๊ณ  ๊ฐ์ ํจ). '1'์ Android ์คํ๋์ค ๋ด **Design Editor**์๋ง ํ์๋๊ณ  ์ค์  ๊ธฐ๊ธฐ ๋๋ ์๋ฎฌ๋ ์ดํฐ์์ ์ฑ์ ์คํํ  ๋๋ ํ์๋์ง ์์ต๋๋ค

<br>

### Activity ๋ง๋ค๊ธฐ

+ `Activity`๋ ์ฑ์ด UI๋ฅผ ๊ทธ๋ฆฌ๋ ์ฐฝ์ ์ ๊ณตํฉ๋๋ค. ์ผ๋ฐ์ ์ผ๋ก `Activity`๋ ์คํ๋๋ ์ฑ์ ์ ์ฒด ํ๋ฉด์ ์ฐจ์งํฉ๋๋ค. ๋ชจ๋  ์ฑ์๋ ํ๋์ด ํ๋ ์ด์ ์์ต๋๋ค. **์ต์์ ์์ค ๋๋ ์ฒซ ๋ฒ์งธ Activity**์ ์ข์ข `MainActivity`๋ผ๊ณ  ํ๊ณ  ํ๋ก์ ํธ ํํ๋ฆฟ์์ ์ ๊ณตํฉ๋๋ค. ์๋ฅผ ๋ค์ด ์ฌ์ฉ์๊ฐ ๊ธฐ๊ธฐ์์ ์ฑ ๋ชฉ๋ก์ ์คํฌ๋กคํ์ฌ 'Dice Roller' ์ฑ ์์ด์ฝ์ ํญํ๋ฉด Android ์์คํ์ ์ฑ์ `MainActivity`๋ฅผ ์์ํฉ๋๋ค.

```kotlin
package com.example.diceroller

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle

class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
    }
}
```

<br>

+ ์์ ๋ชจ๋  Kotlin ํ๋ก๊ทธ๋จ์๋ `main()` ํจ์๊ฐ ์์ด์ผ ํ๋ค๊ณ  ์์๋ดค์ต๋๋ค. Android ์ฑ์ ๋ค๋ฅด๊ฒ ์๋ํฉ๋๋ค. `main()` ํจ์๋ฅผ ํธ์ถํ๋ ๋์  **Android ์์คํ์ ์ฑ์ด ์ฒ์ ์ด๋ฆด ๋ `MainActivity`์ `onCreate()` ๋ฉ์๋๋ฅผ ํธ์ถ**ํฉ๋๋ค.

<br>

+ **File > New Project Settings > Setting for New Project... > Other Settings > Auto Import**๋ก ์ด๋ํฉ๋๋ค.  **unambigous imports** ์ค์ ์ Android ์คํ๋์ค์ ์ฌ์ฉํ  ๋ฌธ์ ๊ฒฐ์ ํ  ์ ์๋ ํ import ๋ฌธ์ ์๋์ผ๋ก ์ถ๊ฐํ๋ผ๊ณ  ์ง์ํฉ๋๋ค. **optimize imports** ์ค์ ์ Android ์คํ๋์ค์ ์ฝ๋์์ ์ฌ์ฉ๋์ง ์๋ ๊ฐ์ ธ์ค๊ธฐ๋ฅผ ์ญ์ ํ๋ผ๊ณ  ์ง์ํฉ๋๋ค

<br>

### Button์ ์ํธ์์ฉ์ ์ผ๋ก ๋ง๋ค๊ธฐ

```kotlin
class MainActivity : AppCompatActivity() {

   override fun onCreate(savedInstanceState: Bundle?) {
       super.onCreate(savedInstanceState)
       setContentView(R.layout.activity_main)

       val rollButton: Button = findViewById(R.id.button)
       rollButton.setOnClickListener {
           val toast = Toast.makeText(this, "Dice Rolled!", Toast.LENGTH_SHORT)
           toast.show()
       }
   }
}
```

<br>

+ `val rollButton: Button = findViewById(R.id.button)`

  `findViewById()` method finds the `Button` in the layout.

  `R.id.button` is the resource ID for the `Button`, which is a unique identifier for it.

  The code saves a *reference* to the `Button` object in a variable called `rollButton`, not the `Button` object itself.

  > Android๋ ์๋์ผ๋ก **์ฑ์ ๋ฆฌ์์ค์ ID ๋ฒํธ๋ฅผ ํ ๋น**ํฉ๋๋ค. ์๋ฅผ ๋ค์ด **Roll** ๋ฒํผ์๋ ๋ฆฌ์์ค ID๊ฐ ์๊ณ  ๋ฒํผ ํ์คํธ์ ๋ฌธ์์ด์๋ ๋ฆฌ์์ค ID๊ฐ ์์ต๋๋ค. ๋ฆฌ์์ค ID์ ํ์์ `R.<type>.<name>`์๋๋ค(์: `R.string.roll`). `View` ID์ ๊ฒฝ์ฐ `<type>`์ด `id`์๋๋ค(์: `R.id.button`).

<br>

+ ```
   rollButton.setOnClickListener {
             val resultTextView: TextView = findViewById(R.id.textView)
             resultTextView.text = "6"
          }
  ```

  ์ด๋ ๊ฒ `rollButton.setOnClickListener`ํจ์์ ์ฝ๋๋ฅผ ๋ฐ๊ฟ, **Button์ ํด๋ฆญํ  ๋ TextView๋ฅผ ์๋ฐ์ดํธ** ํ  ์ ์๋ค.   

<br>

### ์ฃผ์ฌ์ ๊ตด๋ฆฌ๊ธฐ ๋ก์ง ์ถ๊ฐ

```kotlin
class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val rollButton: Button = findViewById(R.id.button)
        rollButton.setOnClickListener {
           rollDice()
        }
    }

    private fun rollDice() {
       val dice = Dice(6)
        val diceRoll = dice.roll()
        val resultTextView: TextView = findViewById(R.id.textView)
        resultTextView.text = diceRoll.toString()
    }
}

class Dice(private val numSides: Int) { 
    fun roll(): Int {
        return (1..numSides).random()
    }
}
```

<br>

### Good coding practices

+ `Control+A` + `Ctrl+Alt+L` => ๊ณต๋ฐฑ, ๋ค์ฌ์ฐ๊ธฐ ๊ฐ๊ฒฉ ๋ฑ์ ์ฝ๋ ์์ ์ง์ ์ด ์๋ฐ์ดํธ๋๋ค. 

+ class์ ์ฃผ์ ์์

  ```kotlin
  /**
  * This activity allows the user to roll a dice and view the result
  * on the screen.
  */
  class MainActivity : AppCompatActivity() {
  ```

+ method์ ์ฃผ์ ์์

  ```kotlin
  /**
  * Roll the dice and update the screen with the result.
  */
  private fun rollDice() {
  ```

<br>


## ๐ Track 3 : Add conditional behavior in kotlin

### Decision making in your code

+ ์ ์์ ๊ฒฝ์ฐ `Int` ๋ฐ์ดํฐ ์ ํ์ด ์๊ณ  ๋ฒ์์ ๊ฒฝ์ฐ `IntRange`๊ฐ ์๋ ๊ฒ์ฒ๋ผ `true` ๋ฐ `false`์ ๊ฒฝ์ฐ์๋ `Boolean`์ด๋ผ๋ ๋ฐ์ดํฐ ์ ํ์ด ์์ต๋๋ค. ์ด ๊ณผ์ ์ ๋ท๋ถ๋ถ์์ `Boolean` ์ ํ ๋ณ์๋ฅผ ๋ค๋ฃน๋๋ค. 


  ```kotlin
  fun main() {
      val myFirstDice = Dice(6)
      val rollResult = myFirstDice.roll()
      val luckyNumber = 4
  
      if (rollResult == luckyNumber) {
          println("You win!")
      } else if (rollResult == 1) {
          println("So sorry! You rolled a 1. Try again!")
      } else if (rollResult == 2) {
          println("Sadly, you rolled a 2. Try again!")
      } else if (rollResult == 3) {
          println("Unfortunately, you rolled a 3. Try again!")
      } else if (rollResult == 4) {
          println("No luck! You rolled a 4. Try again!")
      } else if (rollResult == 5) {
          println("Don't cry! You rolled a 5. Try again!")
      } else {
          println("Apologies! you rolled a 6. Try again!")
      }
  }
  ```

  > if-else ์ฝ๋ ๋ธ๋ก์์ `else` ๋ฌธ ํ๋์ ํจ๊ป `if` ๋ฌธ ํ๋๋ง ๋ณด์ ํ  ์ ์์ง๋ง ๊ทธ ์ฌ์ด์๋ ํ์ํ ๋งํผ `else if` ๋ฌธ์ ๋ณด์ ํ  ์ ์์ต๋๋ค.

<br>

### when ๋ฌธ ์ฌ์ฉ

```kotlin
fun main() {
    val myFirstDice = Dice(6)
    val rollResult = myFirstDice.roll()
    val luckyNumber = 4

    when (rollResult) {
        luckyNumber -> println("You won!")
        1 -> println("So sorry! You rolled a 1. Try again!")
        2 -> println("Sadly, you rolled a 2. Try again!")
        3 -> println("Unfortunately, you rolled a 3. Try again!")
        4 -> println("No luck! You rolled a 4. Try again!")
        5 -> println("Don't cry! You rolled a 5. Try again!")
        6 -> println("Apologies! you rolled a 6. Try again!")
    }
}
```

+ `rollResult`๊ฐ `luckyNumber`์ด๋ฉด `"You win!"` ๋ฉ์์ง๋ฅผ ์ถ๋ ฅํฉ๋๋ค. 

<br>

## ๐ Track 4 : Add images to the Dice Roller app

```kotlin
val drawableResource = when (diceRoll) {
   1 -> R.drawable.dice_1
   2 -> R.drawable.dice_2
   3 -> R.drawable.dice_3
   4 -> R.drawable.dice_4
   5 -> R.drawable.dice_5
   6 -> R.drawable.dice_6
}

diceImage.setImageResource(drawableResource)
```

```kotlin
private fun rollDice() {
        // Create new Dice object with 6 sides and roll the dice
        val dice = Dice(6)
        val diceRoll = dice.roll()

        // Find the ImageView in the layout
        val diceImage: ImageView = findViewById(R.id.imageView)

        // Determine which drawable resource ID to use based on the dice roll
        val drawableResource = when (diceRoll) {
            1 -> R.drawable.dice_1
            2 -> R.drawable.dice_2
            3 -> R.drawable.dice_3
            4 -> R.drawable.dice_4
            5 -> R.drawable.dice_5
            else -> R.drawable.dice_6
        }

        // Update the ImageView with the correct drawable resource ID
        diceImage.setImageResource(drawableResource)

        // Update the content description
        diceImage.contentDescription = diceRoll.toString()
    }
```

+ `setImageResource()`๋ฅผ ์ฌ์ฉํ์ฌ `ImageView`์ ํ์๋๋ ์ด๋ฏธ์ง๋ฅผ ๋ณ๊ฒฝํ๋ค.  

+ `if / else` ํํ์์ด๋ `when` ํํ์๊ณผ ๊ฐ์ ์ ์ด ํ๋ฆ ๋ฌธ์ ์ฌ์ฉํ์ฌ ์ฑ์์ ๋ค์ํ ์ฌ๋ก๋ฅผ ์ฒ๋ฆฌํฉ๋๋ค(์: ์ฌ๋ฌ ์ํฉ์์ ๋ค์ํ ์ด๋ฏธ์ง ํ์).

<br>

## ๐ Track 5 : lemonade App

#### ๋ฆฌ์์ค ์ ๊ทผํ๋ ๋ฒ

+ drawble resource
  `lemonImage?.setImageResource(R.drawable.lemon_tree)`

+ string resource

  `textAction.setText(R.string.lemon_select)`

<br>

#### ๋ฌธ์์ด ์์ ์ง์ 

๋ฌธ์์ด์ ์์์ ์ง์ ํด์ผ ํ  ๊ฒฝ์ฐ, ๋ค์ ์์์ ๊ฐ์ด ๋ฌธ์์ด ๋ฆฌ์์ค์ ์์ ์ธ์๋ฅผ ์ถ๊ฐํ์ฌ ์ง์ ํ  ์ ์์ต๋๋ค.

```kotlin
<string name="welcome_messages">Hello, %1$s! You have %2$d new messages.</string>
```

์ด ์์๋ ์์ ๋ฌธ์์ด์ ๋ ๊ฐ์ ์ธ์๊ฐ ์์ต๋๋ค. `%1$s`๋ ๋ฌธ์์ด์ด๊ณ  `%2$d`๋ 10์ง์์๋๋ค. `getString(int, Object...)`์ ํธ์ถํ์ฌ ๋ฌธ์์ด์ ์์์ ์ง์ ํด๋ณด๊ฒ ์ต๋๋ค. ์๋ฅผ ๋ค๋ฉด ๋ค์๊ณผ ๊ฐ์ต๋๋ค.

```kotlin
var text = getString(R.string.welcome_messages, username, mailCount)
```

<br>

#### View๋ฅผ ํด๋ฆญํ์ ๋, ๋์ ์คํํ๊ธฐ

```kotlin
private var lemonImage: ImageView? = null

lemonImage = findViewById(R.id.image_lemon_state)

lemonImage!!.setOnClickListener {
            // TODO: call the method that handles the state when the image is clicked
            clickLemonImage()
        }

lemonImage!!.setOnLongClickListener {
            // TODO: replace 'false' with a call to the function that shows the squeeze count
            // ๊ธธ๊ฒ ๋๋ ์ ๋ ์ผ๋ง๋ ๋ ๋ชฌ์ ์งฐ๋์ง ์๋ ค์ค
            showSnackbar()
        }
```

<br>

#### onSaveInstanceState 

+ `onSaveInstanceState()` ๋ฉ์๋๋ฅผ ์ด์ฉํ๋ฉด Activity๊ฐ ์ข๋ฃ๋  ๋ ๋ฐ์ดํฐ๋ฅผ ์ ์ฅํ  ์ ์์ต๋๋ค. ์ผ๋ฐ์ ์ผ๋ก ์ฌ์ฉ์๊ฐ ์ ์์ ์ธ ํ๋์ผ๋ก Activity๋ฅผ ์ข๋ฃํ  ๋๋ ํด๋น ์ด๋ฒคํธ๋ฅผ ๋ฏธ๋ฆฌ ๊ฐ์งํ๊ณ  ๊ทธ์ ๋ง๋ ๋์ฒ๋ฅผ ํด์ค ์๊ฐ ์์ง๋ง, ์ค์ ๋ก๋ ๋ค์ํ ์ํฉ์์ Activity๊ฐ ์ข๋ฃ๋๋ ํ์์ด ๋ฐ์ํ  ์ ์์ต๋๋ค. ๊ทธ๋ฆฌ๊ณ  ๋ค์ ์กํฐ๋นํฐ๊ฐ ์คํ๋  ๋๋ `onCreate(savedInstanceState: Bundle?)`์์ Bundle์์ data๋ฅผ ๋ฐ์์ ์ด์ฉํ  ์ ์๋ค.

<br>

+ Activity๊ฐ ์ข๋ฃ๋๋ ๊ฒฝ์ฐ
  + ์ฌ์ฉ์๊ฐ โ๋ค๋ก ๊ฐ๊ธฐ(Back)โ ๋ฒํผ์ ๋๋ฌ Activity๋ฅผ ์ข๋ฃํ ๊ฒฝ์ฐ
  + Activity๊ฐ ๋ฐฑ๊ทธ๋ผ์ด๋์ ์์ ๋ ์์คํ ๋ฉ๋ชจ๋ฆฌ๊ฐ ๋ถ์กฑํด์ง ๊ฒฝ์ฐ(OS๊ฐ ๊ฐ์  ์ข๋ฃ์ํด)
  + ์ธ์ด ์ค์ ์ ๋ณ๊ฒฝํ  ๋
  + ํ๋ฉด์ ๊ฐ๋ก/์ธ๋ก ํ์ ํ  ๋
  + ํฐํธ ํฌ๊ธฐ๋ ํฐํธ๋ฅผ ๋ณ๊ฒฝํ์ ๋

<br>

+ ์ฌ์ฉ ์์

  ```kotlin
  override fun onSaveInstanceState(outState: Bundle) {
      outState.putString(LEMONADE_STATE, lemonadeState)
      outState.putInt(LEMON_SIZE, lemonSize)
      outState.putInt(SQUEEZE_COUNT, squeezeCount)
      super.onSaveInstanceState(outState)
  }
  
  override fun onCreate(savedInstanceState: Bundle?) {
          super.onCreate(savedInstanceState)
          setContentView(R.layout.activity_main)
  
          // === DO NOT ALTER THE CODE IN THE FOLLOWING IF STATEMENT ===
          if (savedInstanceState != null) {
              lemonadeState = savedInstanceState.getString(LEMONADE_STATE, "select")
              lemonSize = savedInstanceState.getInt(LEMON_SIZE, -1)
              squeezeCount = savedInstanceState.getInt(SQUEEZE_COUNT, -1)
          }
  ```











## Quiz/Unit1/Pathway4

1. Which of the following is an example of a class?

   => 

   + A Car class that has a make and model, and that can be driven
   + A Flower class that has a scent
   + A Puppy class that has breed, weight and age, and that can bark
   + A ShoppingCart class that has a cart size and cart value, and that can hold items
   + A Song class that has lyrics



2. Which of the following is a difference between a class and an instance?

   => 

   + You can think of a class as a blueprint and an instance as the actual โthing".

   + A class is like architectural plans for a bridge, and the Golden Gate bridge an instance of those plans.
   + You can create multiple instances from a class, but you can't create classes from instances.



3. For each of the following types of information, select whether it should be part of a class or an instance.

   => 

   + Information about properties shared by all "things" belonging to the class, such as number of sides, number of legs, or that it has a color. => **class**

   + The specifics about a property, such as the specific color of a โthingโ that can have a color. 

     => **Instance**

   

4. True or false? Every MainActivity class in Android must have a main() function.

   => False



5. Which of the following is NOT a way for creating a comment in Kotlin?

   =>  

   + Use // to turn the rest of a function into a comment.
   + Use /* to start a comment that is one line long.

   => way of creating comment in Kotlin

   + Add // at the beginning of or inside a line and anything after that // is considered a comment.
   + Put /* or /** to start a block comment, and end it with */.

   

6. Which of the following statements about a conditional statement is true?

   => 

   + A conditional statement is a way for you to set up a condition and ensure that code following it is only executed if that condition is met.
   + A conditional statement can be used within functions to return output based on conditions defined in that function.



7. What is a good reason for you to add comments to your code?

   => 

   + To explain to yourself or others why the code is written a certain way.
   + To structure code, like chapter headings in books.
   + To point out some part of the code that is very important.
   + To explain to other developers how to use your code for their own programs.



8. Which of the following are Kotlin data types?

   => 

   + IntRange
   + Int
   + Boolean(true or false)



9. Which of the following are valid keywords used in conditional statements in Kotlin?

   => 

   + if, else

   + when

 
