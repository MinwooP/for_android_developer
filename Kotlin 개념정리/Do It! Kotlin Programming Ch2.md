# Do It! Kotlin Programming Ch2

<br>

## π© 2 - 1 μ½νλ¦° ν¨ν€μ§

μ½νλ¦°μμ **νλ‘μ νΈ**λ **λͺ¨λ, ν¨ν€μ§, νμΌ**λ‘ κ΅¬μ±λμ΄ μμ΅λλ€. 

+ μ½νλ¦° νλ‘μ νΈ - μ¬ν
+ λͺ¨λ - λͺ©μ μ§
+ ν¨ν€μ§ - μ¬νμ© κ°λ°©
+ νμΌ - κ°λ°© μμ λ£μ μ§

<br>

<br>

##### μ½νλ¦° νλ‘μ νΈ, λͺ¨λ, ν¨ν€μ§, νμΌμ κ΄κ³ μ΄ν΄νκΈ° 

+ νμΌ(ν΄λμ€) => ν¨ν€μ§ => λͺ¨λ => μ½νλ¦° νλ‘μ νΈ

<img src = "https://user-images.githubusercontent.com/31370590/137160006-d7ca78b1-1b30-415a-bb91-400a5f6cffc6.PNG">

<br>

+ HelloKotlin νλ‘μ νΈ
  + HelloKotlin λͺ¨λ
    + com.example.edu ν¨ν€μ§
    + default ν¨ν€μ§
  + OtherKotlin λͺ¨λ

<br>

+ νλ‘μ νΈμ λͺ¨λμ κ΄κ³

  λ³΄ν΅ λκ·λͺ¨ **νλ‘μ νΈλ₯Ό μ§νν  λ**λ **κΈ°λ₯μ λͺ¨λλ‘ λΆλ¦¬νμ¬ κ΄λ¦¬**ν©λλ€. μ¦, HelloKotlin νλ‘κ·Έλ¨μ 2κ°μ κΈ°λ₯μ κ°μ§κ³  μλ κ²μ΄λ€.

+ μ½νλ¦° νμΌμ .kt νμ₯μλ₯Ό κ°μ§λ©° νμΌμ λ§¨ μμλ μ΄ νμΌμ΄ μ΄λ€ ν¨ν€μ§μ ν¬ν¨λ κ²μΈμ§ μ½νλ¦° μ»΄νμΌλ¬κ° μ μ μλλ‘ ν¨ν€μ§ μ΄λ¦μ μ μΈν΄μΌ νλ€. ν¨ν€μ§ μ΄λ¦μ μ μΈνμ§ μμΌλ©΄ κ·Έ νμΌμ μλμΌλ‘ default ν¨ν€μ§μ ν¬ν¨λλ€.

<br>

##### ν¨ν€μ§λ₯Ό λ§λ€μ΄μΌ νλ μ΄μ 

2λͺμ νλ‘κ·Έλλ¨Έκ° νλ‘μ νΈλ₯Ό μ§ννλ€ μ°μ°ν κ°μ μ΄λ¦μ νμΌ(ν΄λμ€)λ₯Ό λ§λ€μλ€λ©΄ μ€λ₯κ° λ°μνμ§λ§, **ν¨ν€μ§κ° λ€λ₯΄λ©΄ μ€λ₯κ° λ°μνμ§ μλλ€.** 

<br>

##### ν¨ν€μ§ μ΄λ¦ μ νκΈ°

ν¨ν€μ§ μ΄λ¦μ νμΌ λ§¨ μμ μ μΌλ©΄ λκ³ , μ¬λ¬ λ¨κ³μ λΆλ₯κ° νμνλ©΄ μ (.)μ λΆμ¬ μ΄λ¦μ μ§μΌλ©΄ λλ€. μ΄λ¦μ μ§μ λ λ€λ₯Έ μ΄λ¦κ³Ό μ€λ³΅λμ§ μλλ‘ **μΉμ¬μ΄νΈ μ£Όμ μ΄λ¦**μ μ§λ λ°©μμ λ§μ΄ μ¬μ©νλ€. 

<br>

#### κΈ°λ³Έ ν¨ν€μ§ νμ©νκΈ°

κΈ°λ³Έ ν¨ν€μ§λ μ½λ₯Όλ¦°μΌλ‘ νλ‘κ·Έλ¨μ λ§λ€ λ μμ£Ό μ¬μ©νλ ν΄λμ€μ ν¨μ λ±μ λ―Έλ¦¬ λ§λ€μ΄ λΈμ κ²μ΄λ€. μ΄λ€μ **import** ν€μλλ‘ ν¨ν€μ§λ₯Ό μ μΈνμ§ μμλ λ°λ‘ μ¬μ©κ°λ₯νλ€.

ex) `kotlin.*` package

<br>

<br>

<br>

## π© 2 - 2 λ³μμ μλ£ν

### λ³μ

- val

  - **val**ue
  - μ μΈνλ©΄ μ΅μ΄λ‘ μ§μ ν λ³μμ κ°μΌλ‘ μ΄κΈ°ν ν μ½κΈ°λ§ κ°λ₯
  - javaμ finalκ³Ό λμΌ

- var

  - **var**iable
  - μ΅μ΄λ‘ μ§μ ν λ³μμ μ΄κΉκ°μ΄ μλλΌλ κ°μ λ³κ²½ κ°λ₯

  => valλ‘ λ³μλ₯Ό μ μΈν΄λκ³  λ³κ²½ν΄μΌ ν  λ varλ‘ λ°κΎΈλ λ°©λ²μ κΆμ₯νλ€.
  
  > ```kotlin
  > val a = 3 //μ΄λ κ² μ μΈν΄λκ³  
  > // μ½λ©νλ€κ° aλ₯Ό μ¬μ©ν  μΌ μμΌλ©΄
  > var a = 3 // μ΄λ κ² μ§μ  varλ‘ λ°κΎΈλΌλ λ»?
  > ```
  >
  > 
  
  

<br>

- λ³μ μ μΈ

  - μλ£νμ μ§μ νμ§ μκ³  μ μΈνλ©΄ λ³μμ **ν λΉλ κ°μ ν΅ν΄ μΆλ‘ νμ¬ μλ£νμ μ§μ **

    => `val username = "Minwoo"`

  - κ°μ ν λΉνμ§ μκ³  λ³μλ₯Ό μ μΈνλ €λ©΄ λ°λμ μλ£νμ μ§μ ν΄μΌ νλ€.

    => `val username : String`

  - λ³μ μ΄λ¦ μ§λ μ£Όμ μ¬ν­

    - λ³μ μ΄λ¦μ μ«μλ‘ μμ λΆκ°
    - λ³μ μ΄λ¦μΌλ‘ whileκ³Ό if κ°μ΄ μ½νλ¦°μμ μ¬μ©λλ ν€μλ λΆκ°
    - μ¬λ¬ λ¨μ΄λ₯Ό μ¬μ©νμ¬ λ³μ μ΄λ¦μ μ§μΌλ©΄ μΉ΄λ© νκΈ°λ² μ¬μ© κΆμ₯

<br>

<br>

### μλ£ν

##### μ½νλ¦°μ μλ£νμ μ°Έμ‘°ν μλ£νμ μ¬μ©νλ€.

+ **κΈ°λ³Έν**(Primitive Data Type)μ κ°κ³΅λμ§ μμ μμν μλ£νμ λ§νλ©° νλ‘κ·Έλλ° μΈμ΄μ λ΄μ₯λμ΄ μλ€.

+ **μ°Έμ‘°ν**(Reference Type)μ **κ°μ²΄λ₯Ό μμ±νκ³  λμ  λ©λͺ¨λ¦¬ μμ­μ λ°μ΄ν°λ₯Ό λ λ€μ μ΄κ²μ μ°Έμ‘°ν**λ μλ£νμ λ§νλ€.

μλ°μμλ int, long, float, double λ± κΈ°λ³Ένκ³Ό  String, Dateμ κ°μ μ°Έμ‘°νμ λͺ¨λ μ¬μ©νμ§λ§ μ½νλ¦°μμλ μ°Έμ‘°νλ§ μ¬μ©νλ€. **μ°Έμ‘°νμΌλ‘ μ μΈν λ³μλ μ±λ₯μ΅μ νλ₯Ό μν΄ μ½νλ¦° μ»΄νμΌλ¬μμ λ€μ κΈ°λ³ΈνμΌλ‘ λμ²΄λλ€**. λ°λΌμ μ½νλ¦°μμλ μ°Έμ‘°νμ κΈ°λ³ΈνμΌλ‘ κ³ λ €νλ λ±μ μ΅μ νλ₯Ό μ κ²½μ°μ§ μμλ λλ€.

<br>

<br>

##### κΈ°λ³Ένκ³Ό μ°Έμ‘°νμ λμ μλ¦¬

μλ°μμ μ¬μ©λ κΈ°λ³Ένκ³Ό μ°Έμ‘°νμΌλ‘ μ μΈν λ³μ

```java
int a = 77; // κΈ°λ³Έν
Person person = new Person(); // μ°Έμ‘°νμΌλ‘ person κ°μ²΄λ₯Ό μν΄ μ°Έμ‘° μ£Όμ(A12)λ₯Ό κ°μ§λ€.
```

+ κΈ°λ³ΈνμΌλ‘ μ μΈν λ³μ aλ μ£Όλ‘ μμ λ©λͺ¨λ¦¬μΈ **μ€ν**μ μ μ₯λλ©° κ°μ΄ μ μ₯λ λ©λͺ¨λ¦¬μ ν¬κΈ°λ κ³ μ λμ΄ μλ€.
+ μ°Έμ‘°νμ μ€νμ κ°μ΄ μλ μ°Έμ‘° μ£Όμκ° μλ€. κ·Έλ¬λ©΄ μ°Έμ‘°νμ μ€μ  κ°μ²΄λ λμ  λ©λͺ¨λ¦¬μΈ **ν**μ μ μ₯λλ€. 
+ κΈ°λ³Ένμ΄ μ°Έμ‘°νλ³΄λ€ μ½λ μνμκ°μ΄ λΉ λ₯΄κ³  μ½νλ¦°μ μ»΄νμΌ κ³Όμ μ κ±°μΉλ©΄μ μ°Έμ‘°νμ κΈ°λ³ΈνμΌλ‘ λ°κΏμ£Όλ©° μλμΌλ‘ μ΅μ νλ₯Ό μνν΄μ€λ€. λ°λΌμ μ½νλ¦°μμ κΈ°λ³Ένμ μ¬μ©ν μ§ μ°Έμ‘°νμ μ¬μ©ν μ§ κ³ λ―Όx => **μ°Έμ‘°νλ§ μ¬μ©νλ©΄ λ¨**

<img src = "https://user-images.githubusercontent.com/31370590/137169464-a4eb9a57-c08c-44b0-9fdf-75682b0e0cd7.PNG">

<br>

<br>

#### μ μ μλ£ν

+ **Long**  - 8B
+ **Int** - 4B
+ **Short** - 2B
+ **Byte** - 1B

<br>

+ μ μλ₯Ό ννν  λ μ«μλ₯Ό κ·Έλ₯ μ¬μ©νλ©΄ 10μ§μλ₯Ό λνλ΄μ§λ§ μ λ―Έμ¬λ μ λμ¬λ₯Ό μ¬μ©νλ©΄ 2μ§μλ 16μ§μ ννκ°λ₯

  ```kotlin
  val num1 = 123
  val num2 = 123L // μ λ―Έμ¬ Lμ ν΅ν΄ LongνμΌλ‘ μΆλ‘ 
  val num3 = 0x0F // μ λμ¬ 0xλ₯Ό μ¬μ©ν΄ 16μ§λ²μΌλ‘ νκΈ°λ IntνμΌλ‘ μΆλ‘ 
  val num4 = 0b00001011 // μ λμ¬ 0bλ₯Ό μ¬μ©ν΄ 2μ§ νκΈ°κ° μ¬μ©λ IntνμΌλ‘ μΆλ‘ 
  ```

<br>

<br>

#### μ€μ μλ£ν

+ **Double** - 8B
+ **Float** - 4B

+ λ°μ΄ν° ν¬κΈ°μ λ§κ² μλ£νμ μ§μ νλ €λ©΄ μλ£νμ μ΅μκ°κ³Ό μ΅λκ°μ νμν΄μΌ νλ€.

<br>

<br>

#### λΌλ¦¬ μλ£ν

+ **Boolean** - 1bit => true or false

+ λΌλ¦¬ μλ£νμ νν **κ²μ¬ μ©λμ λ³μ**λ₯Ό λ§λ€ λ μ¬μ©νλ.

  ```kotlin
  val isOpen = true
  val isUpLoaded : Booleean

<br>

<br>

#### λ¬Έμ μλ£ν

+ **Char** - 2B

+ μ»΄ν¨ν°λ λ¬Έμ μλ£ν κ°μ μ μ₯ν  λ λ¬ΈμμΈνΈ(**μμ€ν€μ½λ ν**, μ λμ½λ ν)λ₯Ό μ°Έκ³ νμ¬ λ²νΈλ‘ μ μ₯νλ€. νμ§λ§ **μ μΈν  λλ λ¬Έμ κ°μΌλ‘ μ μΈν΄μΌ νλ€.** μ μΈν λ€μμλ λ¬Έμ μλ£νμ μ«μλ₯Ό λνλ λ°©μμΌλ‘ λ€λ₯Έ λ¬Έμλ₯Ό ννν  μ μλ€.

  ```kotlin
  val ch = 'A'
  println(ch+1) // B
  
  val chNum: Char = 65 // μ€λ₯! μ«μλ₯Ό μ¬μ©νμ¬ μ μΈνλ κ²μ κΈμ§

<br>

<br>

#### λ¬Έμμ΄ μλ£ν

+ **String** 

+ λ¬Έμ μλ£ν Charμ charκ³Ό κ°μ κΈ°λ³ΈνμΌλ‘ μ²λ¦¬λμ§λ§, λ¬Έμμ΄ μλ£νμ **κΈ°λ³Ένμ μνμ§ μμ λ°°μ΄ ννλ‘ λμ΄ μλ νΉμν μλ£ν**μ΄λ€.

<br>

+ λ¬Έμμ΄ μλ£ν μ μΈκ³Ό μ μ₯ λ°©μ

  ```kotlin
  fun main(){
      var str1: String = "Hello"
      var str2 = "World"
      var str3 = "Hello"
  }
  // str1 == str3
  ```

  + str1, str3μλ κ°μ λ¬Έμμ΄μ΄ μ μ₯λμ΄ μλλ° μ΄λ° κ²½μ°, **"Hello"**λ₯Ό μ€νμ 2λ² μ μ₯νλ κ²μ΄ μλλΌ, ν μμ­μ **String pool**μ΄λΌλ κ³΅κ°μ λ¬Έμμ΄μΈ "Hello"λ₯Ό μ μ₯ν΄λκ³  μ΄ κ°μ str1, str3μ΄ μ°Έμ‘°νλλ‘ λ§λ λ€. 

    => String Poolμ μ΄μ©ν΄ νμν κ²½μ° λ©λͺ¨λ¦¬λ₯Ό μ¬νμ©νλ€. 

    <img src = "https://user-images.githubusercontent.com/31370590/137173986-bf0446f1-e9da-4bab-aecc-06356f6076c5.PNG">

<br><br>

+ λ³μμ κ°μ΄λ ννμμ λ¬Έμμ΄ μμ λ£μ΄ μΆλ ₯νλ €λ©΄ `$` κΈ°νΈμ μ€κ΄νΈ `{}`λ₯Ό μ¬μ©νλ©΄ λλ€.

  ```kotlin
  var a = 1
  val s1 = "a is $a" // λ¬Έμμ΄μ λ³μ μ¬μ©
  ```

  ```kotlin
  val a = 1
  val str2 = "a = ${a + 2}" // λ¬Έμμ΄μ ννμ μ¬μ©

<br><br>

+ νμνλ λ€μ€ λ¬Έμμ΄ μ¬μ©νκΈ°

  ```kotlin
  fun main() {
      val formattedString = """
  		var a = 6
  		var b = "Kotlin"
  		println(a + num)
  		"""
  }
  ```

  <br>

<br>

<br>

## π© 2 - 3 μλ£ν κ²μ¬νκ³  λ³ννκΈ°

+ κ°μ΄ ν λΉλμ§ μμ λ³μλ₯Ό μ¬μ©νλ©΄ μ½νλ¦°μμ μ€λ₯κ° λ°μνλ€. 

  => μ½νλ¦°μ λ³μμ μμ nullμ νμ©νμ§ μμ **NullPointerException**μ λ°©μ§ν  μ μλ€.

  => μμ nullμ νμ©νμ§ μλ κ±΄ μλκ³ , nullμ ν λΉνλ €λ©΄ μλ£ν λ€μ `?` κΈ°νΈλ₯Ό λͺμνλ©΄ λλ€.

<br>

##### nullμ νμ©ν λ³μ μ¬μ©νκΈ°

+ nullμ νμ©νκΈ° : 
  μλ μ½νλ¦°μμλ λ³μμ nullμ νμ©νμ§ μλλ° κΌ­ nullμ νμ©νλ λ³μλ₯Ό μ¬μ©νκ³  μΆμΌλ©΄ μλ£ν λ€μ `?`κΈ°νΈλ₯Ό λͺμνλ©΄ λλ€.

  ```kotlin
  val str1 : String? = "Hello kotlin"
  str1 = null // λ κ°λ₯
  ```

  νμ§λ§ μ΄λ κ², nullμ νμ©ν λ³μλ₯Ό μ¬μ©νκΈ° μν΄μ  μ‘°κ±΄μ΄ μλ€. 

  ```kotlin
  γfun main(){
      var str1: String? = "Hello Kotlin"
      str1 = null
      println("str1: $str1 length: ${str1.length}") // λΆκ°λ₯
  }
  ```

  `str1` λ³μκ° nullμ νμ©νκΈ° λλ¬Έμ μ΄λ κ·Έλ₯ `str1.length` μ΄λ κ² μ¬μ©λ  μ μλ€. μ€λ₯κ° λ°μνλ€. nullμ νμ©ν λ³μλ₯Ό **κ²μ¬**ν΄μ€μΌ νλ€. μ΄μ λν λ°©λ²μ `?.`, `!!.`, μ‘°κ±΄λ¬Έμ νμ©ν κ²μ¬ λ±μ λ°©λ²μ΄ μλ€. 

<br>

1. μΈμ΄ν μ½ `?.`\

   nullμ΄ ν λΉλμ΄ μμ κ°λ₯μ±μ΄ μλ λ³μλ₯Ό κ²μ¬νμ¬ μμ νκ² νΈμΆνλλ‘ λμμ£Όλ κΈ°λ²μΌλ‘ μΈμ΄ν μ½μ μΆκ°νλ €λ©΄ νΈμΆν  λ³μ μ΄λ¦ λ€μ `?.`λ₯Ό μμ±νλ©΄ λλ€. 

   ```kotlin
   var str1 : String? = "HelloKotlin"
   str1 = null
   str1?.length // null
   ```

   => λ³μ str1μ κ²μ¬ν λ€μ nullμ΄ μλλ©΄ str1μ λ©€λ² λ³μμΈ lengthμ μ κ·Όν΄ κ°μ μ½λλ‘ νλ κ². str1μ nullμ΄λ lengthμ μ κ·Όνμ§ μκ³  κ·Έλλ‘ nullμ μΆλ ₯νλ€. 

<br>

2. non-null λ¨μ κΈ°νΈ `!!.`

   non-null λ¨μ κΈ°νΈλ λ³μμ ν λΉλ κ°μ΄ nullμ΄ μλμ λ¨μ νλ―λ‘ μ»΄νμΌλ¬κ° **null κ²μ¬μμ΄ λ¬΄μ**νλ€. λ°λΌμ λ³μμ nullμ΄ ν λΉλμ΄ μμ΄λ μ»΄νμΌμ μ μ§νλλ€. νμ§λ§ μ€ν μ€μ **NPE**λ₯Ό λ°μμν¨λ€. λ°λΌμ, μ¬μ©μκ° λ³μλ₯Ό λ³΄κ³  λ¬΄μ‘°κ±΄ nullμΈ κ²½μ°μλ§ `!!.`μ μ¬μ©ν΄μ€μΌ νλ€. λ§μ½ nullμ΄λΌλ©΄ μ΄μ λν λ¬Έμ λ μ¬μ©μμ μ±μ? \

   ```kotlin
   println("str1: $str1 length: ${str1!!.length}")
   ```

<br>

3. μ‘°κ±΄λ¬Έμ νμ©ν΄ nullμ νμ©ν λ³μ κ²μ¬νκΈ°

   μΈμ΄ν μ½μ΄λ non-null λ¨μ  κΈ°νΈλ₯Ό μ¬μ©νλ λ°©λ² λμ  μ‘°κ±΄λ¬ΈμΌλ‘ nullμ νμ©ν λ³μλ₯Ό κ²μ¬ν΄λ λλ€. μ¦, nullμ νμ©ν λ³μμ null μν κ°λ₯μ±μ κ²μ¬νκΈ°λ§ νλ©΄ μ»΄νμΌλ¬λ μ€λ₯λ₯Ό λ°μμν€μ§ μλλ€. 

   ```kotlin
   fun main(){
       var str1 = String? = "Hello Kotlin"
       str1 = null
       // μ‘°κ±΄μμ ν΅ν΄ null μν κ²μ¬
       val len = if(str1 != null) str1.length else -1
       println("str1: $str1 length: ${len}")
   }
   ```

   

<br>

##### μΈμ΄νμ½ `?.`κ³Ό μλΉμ€ μ°μ°μ `?:`λ₯Ό νμ©ν΄ nullμ νμ©ν λ³μ λ μμ νκ² μ¬μ©νκΈ°

+ `?:` : λ³μκ° nullμΈμ§ μλμ§ κ²μ¬νμ¬ nullμ΄ μλλΌλ©΄ μΌμͺ½ μμ κ·Έλλ‘ μ€ννκ³  nullμ΄λΌλ©΄ μ€λ₯Έμͺ½ μμ μ€ννλ€. 

  ```kotlin
  ${Str1?.length ?: -1}
  ```

  μ΄λ λ€μ μ½λμ λμΌνλ€

  ```kotlin
  if(str1 != null)
  	str1.length
  else
  	-1

<br>

<br>

#### μλ£ν λΉκ΅, κ²μ¬, λ³ν

##### μλ£ν λ³ν

+ μ½νλ¦°μμλ μλ£νμ΄ μλ‘ λ€λ₯Έ λ³μλ₯Ό λΉκ΅νκ±°λ μ°μ°ν  μ μλ€. 

+ μλ°μμλ μλ£νμ΄ μλ‘ λ€λ₯΄λ©΄ μλ ν λ³νμ΄ λμ§λ§, μ½νλ¦°μμλ μλ£νμ΄ λ€λ₯Έ λ³μμ μ¬ν λΉλλ©΄ μλ ν λ³νμ΄ λμ§ μκ³ , μλ£ν λΆμΌμΉ μ€λ₯κ° λ°μνλ€.

  ```kotlin
  val a: Int = 1
  val b: Double = a // μλ£ν λΆμΌμΉ μ€λ₯ λ°μ
  val c: Int = 1.1 // μλ£ν λΆμΌμΉ μ€λ₯ λ°μ

+ μ¬λ°λ₯΄κ² λ³ννλ €λ©΄ **μλ£ν λ³ν λ©μλ**λ₯Ό μ΄μ©ν΄μΌ νλ€.

  ```kotlin
  val b: Double = a.toDouble() // aλ Int typeμ΄λ―λ‘
  ```

+ ννμμμ μλ£νμ΄ μλ‘ λ€λ₯Έ κ°μ μ°μ°νλ©΄ μλ£νμ΄ ννν  μ μλ λ²μκ° ν° μλ£νμΌλ‘ μλ ν λ³ννμ¬ μ°μ°νλ€.

  ```kotlin
  val result = 1L + 3 // Longν + Intν -> Longν
  ```

<br>

<br>

##### κΈ°λ³Ένκ³Ό μ°Έμ‘°ν μλ£νμ λΉκ΅ μλ¦¬

μλ£νμ λΉκ΅

1. λ¨μν κ°λ§ λΉκ΅ => `==`

   μ°Έμ‘°μ μκ΄μμ΄ κ°μ΄ λμΌνλ©΄ true, λ€λ₯΄λ©΄ false

2. μ°Έμ‘° μ£ΌμκΉμ§ λΉκ΅ => `===` 

   κ°μ μκ΄μμ΄ μ°Έμ‘°κ° λμΌνλ©΄ true, λ€λ₯΄λ©΄ false

```kotlin
val a: Int = 128
val b: Int = 128
println(a == b) // true
println(a === b) // true
```

```kotlin
val a: Int = 128
val b: Int? = 128
println(a == b) // true
println(a === b) // false
```

+ `Int`νμΌλ‘ μ μΈλ aλ κΈ°λ³ΈνμΌλ‘ λ³νλμ΄ μ€νμ 128μ΄λΌλ κ° μμ²΄λ₯Ό μ μ₯νμ§λ§, `Int?`νμΌλ‘ μ μΈλ bλ μ°Έμ‘°νμΌλ‘ μ μ₯λλ―λ‘ bμλ μ μ₯λ 128μ΄ μ μ₯λ νμ μ°Έμ‘° μ£Όμκ° μ μ₯λμ΄ μμ΅λλ€. κ·Έλμ `a === b`λ falseκ° λμ¨λ€. 

ex)

<img src = "https://user-images.githubusercontent.com/31370590/137180458-e5d5386b-9e63-4290-9128-42ee1a431751.PNG" width = "600" height = "900">

<br>

<br>

##### μ€λ§νΈμΊμ€νΈ μ¬μ©νκΈ°

```ko
var test: Number = 12.2
```

+ NumberνμΌλ‘ μ μλ λ³μμλ μ μ₯λλ κ°μ λ°λΌ μ μνμ΄λ μ€μν λ±μΌλ‘ μλ‘νμ΄ λ³νλλ€. 

<br>

##### μλ£ν κ²μ¬νκΈ°

```kotlin
if(num is Int)
```

+ `is` ν€μλ μ¬μ©

<br>

<br>

## π© 2 - 4  μ½νλ¦° μ°μ°μ







#### μ€ν°λ ν

isBlankOrNull() / isBlank()

μ μ°¨μ΄μ 

stringμ nullμ μ‘°μ¬νλ λ°©λ²λ€ μ‘°μ¬



+ μ¨λΉμ€ μ°μ°μ



` a ?: b` a κ°μ²΄κ° null μ΄λ©΄ 



+ bindingμ varλ‘ μ μΈνλ μ΄μ ? 

