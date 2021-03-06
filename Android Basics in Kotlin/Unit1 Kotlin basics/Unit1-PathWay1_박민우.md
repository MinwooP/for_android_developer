# π₯ Unit 1: Kotlin basics

## PATHWAY 1 : Introduction to Kotlin

<br>

###  νλ‘κ·Έλ¨κ³Ό ν¨μ, λ³μ

+ __νλ‘κ·Έλ¨__μ΄λ μμ€νμμ μμμ μννκΈ° μν μΌλ ¨μ λͺλ Ή. 

+ νλ‘κ·Έλ¨μ μ€νν  λ μ²«λ²μ§Έλ‘ νΈμΆλλ ν¨μ __main__

  ```kotlin
  fun main() {
      println("Happy Birthday!")
      print("Happy Birthday!") // λ¬Έμμ΄ λμ μ€λ°κΏμ μΆκ°νμ§ μκ³  νμ€νΈλ₯Ό μΆλ ₯νλ€
      println("") // νμ€νΈλ₯Ό μλ ₯νμ§ μκ³  λΉ μ€μ μΆλ ₯ 
  }
  ```

+ ```val``` ν€μλλ₯Ό μ¬μ©νμ¬ μ μΈλ λ³μλ ν λ²λ§ μ€μ ν  μ μλ€. νλ‘κ·Έλ¨ νλ°λΆμ κ°μ λ³κ²½ν  μ μλ€.  ```var```  ν€μλλ‘ λ³κ²½κ°λ₯ν λ³μλ₯Ό μ μΈν  μ μλ€.

+ print λ¬Έ λ΄μμ λ³μλ₯Ό μ¬μ©νλ €λ©΄ μμ€νμ λ€μμ μ€λ κ²μ΄ νμ€νΈκ° μλλΌ λ³μμμ μλ €μ£Όλ κΈ°νΈλ‘ λ³μλ₯Ό λλ¬μΈμΌ νλ€. νμ€νΈλ₯Ό μΆλ ₯νλ λμ  μμ€νμ λ³μ κ°μ μΆλ ₯ν΄μΌ νλ€. 

  ```kotlin
  ${variable}
  ```

  ```kotlin
  println("You are already ${age}!")
  println("${age} is the very best age to celebrate!")
  ```

<br><br>

### ν¨μ μ μ

+ ν¨μ μ΄λ¦μ __μλ¬Έμ__μ __λμ¬__λ‘ μμνλ κ²½μ°κ° κ±°μ λλΆλΆμ΄λ©°, μ΄λ¦μ ν¨μκ° νλ μμμ μ€λͺν΄μΌ νλ€. 

+ ν¨μ μ΄λ¦μ λ λ²μ§Έ λ¨μ΄λ λλ¬Έμλ‘ μμνλ€. μ΄λ¬ν μ€νμΌμ '__camel case__' λΌκ³  νλ©°, μ΄λ₯Ό ν΅ν΄ μ΄λ¦μ ν¨μ¬ μ½κ² μ½μ μ μλ€.

+ ```printBorder``` ν¨μ μ μ  

  ```kotlin
  fun printBorder() {
      println("===================")
  }
  ```

<br><br>

### repeatλ¬Έ

+ μ½λμμλ ```repeat()``` λ¬Έμ μ¬μ©νμ¬ λ°λ³΅μ μΈ μμμ κ°νΈν ν  μ μλ€. 

  ```kotlin
  fun printBorder(){
      repeat(23) {
          print("=")
      }
      println()
  }
  ```

+ κ΄νΈ ```()``` μμλ λ°λ³΅ νμκ° μ¨λ€.
+ μ€κ΄νΈ ```{}``` μμλ λ°λ³΅ν  μ½λλ₯Ό νμνλ€.





### ν¨μ μΈμ μ λ¬

```kotlin
fun main() {
    val border = "`-._,-'"
    val timesToRepeat = 4
    printBorder(border, timesToRepeat)
    println("  Happy Birthday, Jhansi!")
    printBorder(border, timesToRepeat)
}

fun printBorder(border: String, timesToRepeat: Int) {
    repeat(timesToRepeat) {
        print(border)
    }
    println()
}
```

+ μΈμμ μ΄λ¦μ ```border``` μ΄λ€. 
+ μ΄λ¦ λ€μλ μ½λ‘  ```:``` μ΄ μ¨λ€.
+ κ·Έ λ€μμ μΈμμ μ’λ₯λ μ νμ μ€λͺνλ λ¨μ΄ ```string``` μ΄ μ΄μ΄μ§λ€.
+ **ν¨μ μΈμ μ¬μ© μμ½:** ν¨μμ μΈμλ₯Ό μ¬μ©νλ €λ©΄ λ€μ μΈ κ°μ§ μμμ μ€νν΄μΌ ν©λλ€.
  - ν¨μ μ μμ μΈμμ μ νμ μΆκ°ν©λλ€. ```printBorder(border: String)```
  - ν¨μ λ΄μμ μΈμλ₯Ό μ¬μ©ν©λλ€. ```println(border)```
  - ν¨μ νΈμΆ μ μΈμλ₯Ό μ κ³΅ν©λλ€. ```printBorder(border)```



### Quiz/Unit1/pathway1

1. What is a program?

   => a series of instructions that a computer system executes to accomplish action

   => μ΄λ€ λμμ μ€ννκΈ° μν΄ μ»΄ν¨ν° μμ€νμ΄ μ€ννλ μΌλ ¨μ λͺλ Ήμ΄λ€μ μ§ν©

   

2. Which keyword do you use to define a function in Kotlin?

   => fun

   ```kotlin
   fun printBorder() {
       println("===================")
   }
   ```

   

3. Which of the following do you need to create a Kotlin program that prints a line of text?

   =>

   + ```main()``` ν¨μ

   + λͺλ Ήμ΄λ€μ λλ¬μΈλ μ€κ΄νΈ ```{}```

   + ```print()``` λλ ```println()``` ν¨μμ νΈμΆ

   + ```" "```λ‘ λλ¬μΈμΈ μΆλ ₯ν  text

     

4. What do you expect this Kotlin code to do?

   ```kotlin
   fun main(args: Array<String>) {
     println("Hello, world!")
     println("It's a sunny and warm day!")
   }
   ```

   => μ΄ ν¨μλ λ κ°μ text lineμ μΆλ ₯ν  κ²μ΄λ€. 

   ```kotlin
   // "Hello, world!"
   // "It's a sunny and warm day!"
   ```



5. How would you modify this `main()` function so that it prints a 6-layer cake for someone's 4th birthday?

   ```kotlin
   fun main() {
     val age = 24 // val age = 4λ‘ μμ ν΄μΌ ν¨
     val layers = 5 // val layers = 6λ‘ μμ ν΄μΌ ν¨
     printCakeCandles(age)
     printCakeTop(age)
     printCakeBottom(age, layers)
   }
   ```

   

6. Which of these options correctly calls the function, below, and passes it valid input arguments?

   ```kotlin
   fun createMessage(name: String, location: String, age: Int) {
     println("My name is ${name}. I am from ${location}, and I am ${age} years old.")
   }
   ```

   => μ΄ ν¨μλ₯Ό μ λλ‘ νΈμΆνλ €λ©΄, ```createMessage("Amy", "Australia", 20)``` κ°μ΄ νΈμΆν΄μΌ νλ€. 
