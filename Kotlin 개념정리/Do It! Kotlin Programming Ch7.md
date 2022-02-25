# Do It! Kotlin Programming Ch7

## 다양한 클래스와 인터페이스

-----

## 🚩 7 - 1 추상 클래스와 인터페이스

### 📌 추상 클래스

+ 추상 클래스란 객체로 만들 수 없는 그야말로 추상적인 개념으로 일종의 **설계도** 역할을 한다. 각 개체들이 주고받는 데이터를 구조화할 수 있다. 

+ 선언 등의 대략적인 설계 명세와 공통의 기능을 구현한 클래스이다.

+ `abstract class Vehicle`

  추상 클래스의 프로퍼티나 메서드도 abstract로 선언될 수 있다. 물론 기본적인 프로퍼티나 메서드의 선언은 abstract가 아니므로 특정 초기화나 구현이 필요하지만 **abstract로 선언된 프로퍼티나 메서드는 아직 미완성되었다는 의미를 줄 수 있다.**

<br>

만일 **추상 클래스로부터** 하위 클래스를 생성하지 않고 **단일 인스턴스로 객체를 생성**하려면 object를 사용해서 지정할 수 있다.

```kotlin
abstract class Printer {
    abstract fun print() // 추상 메서드
}

val myPrinter = object: Printer() { // 객체 인스턴스
    override fun print() { // 추상 메서드의 구현 
        println("출려")
    }
}
```

추상 메서드 하나를 가지는 클래스인 Printer는 객체 인스턴스를 지정하기 위해 **익명 객체를 지정하는 object 키워드를 사용**했습니다. 이때는 **콜론(:) 오른쪽에 생성자 이름을 사용하고 블록에서 관련 메서드를 오버라이딩해 구현해야 한다.** 

<br>

### 📌 인터페이스

인터페이스에는 abstract로 정의된 추상 메서드나 일반 메서드가 포함된다. 다른 객체 지향 언어와는 다르게 **메서드에 구현 내용이 포함될 수 있다.** 하지만 추상 클래스처럼 **프로퍼티를 통해 상태를 저장할 수는 없다.** 선언만 가능하다. 

인터페이스는 현실 세계의 "계약서"와 비슷하다. 계약서에는 무엇 무엇을 하라는 추상적인 활동이 적혀있다.이것을 어떤 '작업자'가 받아들인다면 계약서에 있는 활동의 구체적인 내용을 반드시 실행해야 한다. 계약서 자체로는 실행되지 않는다. 작업자에 의해 구체적인 작업이 구현되어야 실행하는 것이다. 

추상 클래스와 용도가 비슷해 보이는데 인터페이스를 쓰는 이유는 무엇일까? 

추상 클래스를 쓸 때의 제한 => 상속을 통해 하위 클래스로 확장해나갈 수 있지만 하위 클래스는 상속을 하나만 허용하기 때문에 **2개 이상의 클래스로부터 프로퍼티나 메서드를 상속받을 수 없다.** 그리고 상위 클래스와 하위 클래스에 강한 연관이 생기면서 하위 클래스는 상위 클래스의 영향을 받는다. 예를 들어 상위 클래스가 정의한 내용이 불완전하다면 그 상위 클래스를 상속받는 하위 클래스도 그대로 영향을 받는다. 

인터페이스는 클래스가 아니다. 따라서 상속이라는 형태로 하위 클래스에 프로퍼티와 메서드를 전하지 않는다. 그래서 하위 클래스보다는 구현 클래스라고 이야기하고, 이러한 구현 클래스의 목적은 인터페이스가 제시한 메서드를 구체적으로 '구현'한다는데 있다. 인터페이스는 원하는 만큼 구현 클래스에 붙여서 필요한 메서드를 구현해내면 된다. 인터페이스가 바뀐다고 할지라도 그것을 구현하는 클래스에는 크게 영향을 끼치지 않는다. 



#### 게터를 구현한 프로퍼티

인터페이스에서는 프로퍼티에 값을 저장할 수 없다고 했다. **단 val로 선언된 프로퍼티는 게터를 통해 필요한 내용을 구현할 수 있다.** 

```kotlin
interface Pet {
    var category: String
    val msgTags: String // val 선언 시 게터의 구현이 가능
    	get() = "I'm your lovely pet!"
    
    var species: String // 종을 위한 프로퍼티
    fun feeding()
    fun patting(){
        println("Keep patting!")
    }
}
```

val로 선언된 msgTags는 초기화할 수 없지만 게터를 통해 반환값을 지정할 수 있다. 하지만 **여전히 보조 필드인 field를 사용할 수 없다.** var로 프로퍼티를 선언하더라도 보조 필드를 사용할 수 없기 때문에 받은 value를 저장할 수 없다.

<br>

메서드를 매번 오버로딩해야하는 문제 => 인터페이스 사용

```kotlin
class Master {
    fun playWithPet(pet: Pet) { // 인터페이스를 객체로 매개변수를 지정
        println("Enjoy with my ${pet.species}.")
    }
}
```

Pet 인터페이스에 종을 위한 프로퍼티인 species를 선언하고 이것을 이용해 어떤 애완동물과 놀게 될지 알 수 있다. 이제 Master 클래스의 playWithPet() 메서드는 각 애완동물에 따라서 메서드를 오버로딩할 필요가 없어졌다. 

=> 그럼 이 매개변수인 pet에 들어갈 수 있는 것은 인터페이스 Pet을 구현한 클래스 Cat이나 Dog의 객체?

<br>

#### 인터페이스의 위임

인터페이스에서도 by 위임자를 사용할 수 있다. 

```kotlin
interface A{
    fun functionA(){}
}
```

```kotlin
interface B{
    fun functionB(){}
}
```

```kotlin
class C(val a: A, val b: B){
    fun function(){
        a.functionA()
        b.functionB()
    }
}
```

class C를 설계하기위해 인터페이스 A와 B를 매개변수로 사용한다. functionA()와 functionB() 메서드에 직접 접근하기 위해 a와 b 변수를 사용했다. 이때 by위임자를 사용하면 코드를 더 간략화할 수 있다. 각각 a와 b를 인터페이스 A와 B에 위임함으로써 해당 메서드를 사용할 때 점(.) 표기법 접근 없이 사용할 수 있게 된다.

```kotlin
class DelegatedC(a: A, b: B): A by a, B by b{
    fun functionC(){
        functionA()
        functionB()
    }
}
```



#### 😨 위임을 이용한 멤버 접근



인터페이스를 사용하는 가장 큰 이유는 특정 구현에 의존적이지 않은 코드를 만들 수 있다는 점이다. 그래서 기능의 정의와 구현을 분리할 수 있고 구현 내용을 확장하거나 교체하기 쉽다. 프로젝트가 점점 커질수록 확장이 쉬운 구조를 만들고 싶다면 인터페이스를 사용해야 한다. 



## 🚩 7 - 2 데이터 클래스와 기타 클래스

### 📌 데이터 클래스

보통 클래스는 속성과 동작을 가지기 때문에 프로퍼티와 메서드를 멤버로 가진다. 하지만 만일 특정 동작을 가지지 않고 오로지 데이터 저장을 위해서 사용한다면 일반적인 클래스가 가지는 구현부가 필요 없을 수도 있다**. 구현부 때문에 메모리를 낭비하지 말고 오로지 데이터 저장에 초점을 맞추기 위해 데이터 클래스를 사용할 수 있다.** 

코틀린에서는 데이터 전달을 위한 객체를 위해 데티터 클래스를 정의할 때 게터/세터, toString(), equals() 같은 메서드를 직접 만들 필요 없이 내부적으로 자동 생성된다. 데이터를 위한 프로퍼티만 신경 써서 작성하면 된다. 

<br>

코틀린의 데이터 클래스에서 내부적으로 자동 생성되는 메서드

+ 프로퍼티를 위한 게터/세터
+ 비교를 위한 equals()와 키 사용을 위한 hashCode()
+ 프로퍼티를 문자열로 변환해 순서대로 보여주는 toString()
+ 객체 복사를 위한 copy()
+ 프로퍼티에 상응하는 component1(), component2()



<br>

#### 데이터 클래스 선언

`data class Customer(var name: String, var email: String)`

데이터 클래스가 만족해야 하는 조건

+ 주 생성자는 최소한 하나의 매개변수를 가져야한다.
+ 주 생성자의 모든 매개변수는 val, var로 지정된 프로퍼티여야 한다.
+ 데이터 클래스는 abstract, open, sealed, inner 키워드를 사용할 수 없다. 

<br>

필요하다면 부 생성자나 init 블록을 넣어 데이터를 위한 간단한 로직을 포함할 수 있다. 

```kotlin
data class Customer(var name: String, var email: String){
    var job: String = "Unknown"
    
    // 부 생성자
    constructor(name: String, email:String, _job:String): this(name, email){
        job = _job
    }
    
    init{
        // 간단한 로직은 여기에
    }
}
```

데이터 클래스로 정의된 Customer는 필요한 데이터인 name과 email을 주 생성자에 프로퍼티로 가지고 있고, 부 생성자를 통해 job을 하나 더 초기화할 수 있다. 

<br>

#### 데이터 클래스가 자동 생성하는 메서드

+ equals() : 두 객체의 내용이 같은지 비교하는 연산자
+ hashCode() : 객체를 구별하기 위한 고유한 정숫값 생성, 데이터 세트나 해시 테이블을 사용하기 위한 하나의 생성된 인덱스
+ copy() : 빌더 없이 특정 프로퍼티만 변경해서 객체 복사하기
+ toString(): 데이터 객체를 읽기 편한 문자열로 반환하기
+ componentN() : 객체의 선언부 구조를 분해하기 위해 프로퍼티에 상응하는 메서드

<br>

##### equals()

두 개체의 값이 같은지 동등성을 비교하는 것이다. 보통 우리가 사용하는 연산자인 == 표현은 내부적으로 equals()를 호출하는 것과 같다. 두 값이 동등하다면 true를 반환한다.

<br>

##### hashCode()

hashCode()는 객체를 구별하기 위한 고유한 정숫값을 생성한다. 만약 두 객체가 동등하다면 동일한 정숫값을 생성한다.

<br>

```kotlin
data class Customer(var name: String, var email: String){
    var job: String = "Unknown"
    
    // 부 생성자
    constructor(name: String, email:String, _job:String): this(name, email){
        job = _job
    }
    
    init{
        // 간단한 로직은 여기에
    }
}
```

```kotlin
val cus1 = Customer("Sean", "sean@mail.com")
val cus2 = Customer("Sean", "sean@mail.com")

println(cus1 == cus2) // 동등성 비교
println(cus1.equals(cus2)) // 위와 동일
println("${cus1.hashCode()}, ${cus2.hashCode()}")
```

<br>

##### copy()

copy()를 사용하면 데이터 객체를 복사하되 다른 프로퍼티 값을 가지는 것만 명시하여 변경할 수 있다. 

```kotlin
val cus3 = cus1.copy(name = "Alice") // name만 변경하고자 할 때
println(cus1.toString())
println(cus3.toString())
```

```kotlin
Customer(name=Sean, email=sean@mail.com)
Customer(name=Alice, email=sean@mail.com)
```

<br>

##### 객체 Destructuring 하기

+ 객체를 Destructuring 한다는 것은 객체가 가지고 있는 프로퍼티를 개별 변수로 분해하여 할당하는 것을 말한다. **변수를 선언할 때 소괄호를 사용해서 분해하고자 하는 객체를 지정**한다. 

  ```kotlin
  val(name, email) = cus1
  println("name = $name, email = $email")
  ```

  위와 같이 cus1 객체의 프로퍼티 값 2개를 각각 **name과 email로 선언된 변수**에 가져온다. 

<br>

+ 특정 프로퍼티를 가져올 필요가 없는 경우 다음과 같이 언더스코어(_)를 사용해 제외할 수 있다. 이 경우에는 name은 제외하고 email 프로퍼티만 가져오게 된다.

  ```kotlin
  val(_, email) = cus1 // 첫번째 프로퍼티 제외 kotlin
  ```

  <br>

+ 개별적으로 프로퍼티를 가져오기 위해 componentN() 메서드를 사용할 수 있다. cus1의 첫 번째 프로퍼티 name과 두 번째 프로퍼티 email을 각각 따로 가져온 것을 알 수 있다.

  ```kotlin
  val name2 = cus1.component1()
  val email2 = cus1.component2()
  println("name = $name2, email = $email2")
  ```

<br>

+ 람다식 이용

  ```kotlin
  val myLamda = {
      (nameLa, emailLa): Customer ->
      println(nameLa)
      println(emailLa)
  }
  myLamda(cus1) // 함수처럼 사용
  ```

  객체를 소괄호로 감싸 두었기 때문에 하나의 객체로 람다식에 전달하고, 여기에 2개의 매개변수가 destructuring된 프로퍼티를 각각 출력한다. 이렇게 데이터 클래스는 앞에서 배웠듯이 매개변수에 기본값을 지정할 수 있다.

<br>

### 📌 기타 클래스

<br>

### 내부 클래스 기법

+ 중첩(Nested) 클래스

+ 이너(Inner) 클래스

+ 지역 클래스, 익명 객체 방법으로도 내부 클래스를 정의할 수 있다.

<br>

클래스 내부에 또 다른 클래스를 설계하여 내부에 두는 이유는 독립적인 클래스로 정의하기 모호한 경우나 다른 클래스에서는 잘 사용하지 않는 내부에서만 사용하고 외부에서 접근할 필요가 없을 대가 있기 때문이다. 하지만 너무 남용하면 클래스의 의존성이 커지고 코드가 읽기 어렵게 되므로 주의해야 한다.

<br>

#### 코틀린에서의 내부 클래스

+ 중첩 클래스 : 객체 생성 없이 사용 가능
+ 이너 클래스 : 필드나 메서드와 연동하는 내부 클래스로 inner 키워드가 필요하다
+ 지역 클래스 : 클래스의 선언이 블록 안에 있는 지역 클래스이다. 
+ 익명 객체 : 이름이 없고 주로 일회용 객체를 사용하기 위해 object 키워드를 통해 선언된다

<br>

#### 중첩 클래스

```kotlin
class A{
    class B{ // 코틀린에서는 아무 키워드가 없는 클래스는 중첩 클래스
        // 외부 클래스 A의 프로퍼티, 메서드에 접근할 수 없음
    }
}
```

코틀린에서 중첩 클래스는 기본적으로 정적(Static) 클래스처럼 다뤄진다. 즉, 중첩 클래스는 객체 생성 없이 접근할 수 있다. 

<br>

```kotlin
class Outer {
    val ov = 5
    class Nested {
        val nb = 10
        fun greeting() = "[Nested] Hello ! $nv" // 외부의 ov에는 접근 불가 
    }
    
    fun outside() {
        val msg = Nested().greeting()ㅇ // 객체 생성 없이 중첩 클래스의 메서드 접근
        println("[Outer]: $msg,  ${Nested().nv}") // 중첩 클래스의 프로퍼티 접근
    }
}

fun main(){
    // static 처럼 객체 생성 없이 사용
    val output = Outer.Nested().greeting()
    println(output)
    
    // Outer.outside() // 오류 ! 외부 클래스의 경우 객체를 생성해야함
    val outer = Outer()
    outer.outside()
}
```

+ `Outer.Nested().greeting()`와 같은 방법으로 중첩 클래스의 메서드가 객체 생성 없이 호출될 수 있다. 
+ 외부 클래스의 메서드인 `outside()`에서 중첩 클래스의 멤버 greeting()에 접근할 수 있다. 반대로 중첩 클래스에서 외부 클래스의 멤버인 `ov`와 같은 프로퍼티에 접근할 수 없다.

+ 중첩된 Nested 클래스에서 바로 바깥 클래스인 Outer의 멤버에 접근할 수 없다. 단, Outer 클래스가 컴패니언 객체를 가지고 있을 때는 접근이 가능하다. 

  ```kotlin
  class Outer {
      class Nested {
          ...
          fun accessOuter(){
              println(country) //  컴패니언 object에 접근
              getSomething()
          }
      }
      
      compation object{ // 컴패니언 object는 static 처럼 접근 가능
      	const val country = "Korea"
      	fun getSomething() = println("Get something")
      }
  }
  ```

  + Nested 클래스에서 바깥 클래스인 Outer의 프로퍼티인 `country`와 `getSomething()`에 접근하고 있는데 이것이 가능한 이유는 컴패니언 객체로 지정되어 객체 생성 없이 고정적인 메모리를 가지기 때문이다

<br>

#### 이너클래스

```kotlin
class A{
    inner class B{
        // 외부 클래스 A의 필드에 접근 가능
    }
}
```

단순히 내부에 작성된 중첩 클래스와는 좀 다른 역할을 한다. 클래스 안에 이너 클래스를 정의할 수 있는데 이때 이너 클래스는 바깥 클래스의 멤버들에 접근할 수 있다. 심지어 private 멤버도 접근 가능하다. 

<br>

#### 지역 클래스

```kotlin
class Smartphone(val model: String){
    private val cpu = "Exynos"
    
    fun powerOn(): String {
        class Led(val color: String){ // 지역 클래스 선언
        	fun blink(): String = "Blinking $color on $model" // 외부의 프로퍼티는 접근 가능
        }
        val powerStatus = Led("Red") // 여기에서 지역 클래스가 사용됨
        return powerStatus.blink()
    }
}
```

지역 클래스는 특정 메서드의 블록이나 init 블록과 같이 블록 범위에서만 유효한 클래스이다. 블록 범위를 벗어나면 더 이상 사용되지 않는다. 여기서 사용된 `Led` 클래스는 Smartphone 클래스의 메서드인 powerOn()에서만 유효한 클래스이다. ***단 Led 클래스에서 외부의 멤버인 프로퍼티에는 접근할 수 있다.*** 

<br>

#### 익명 객체

```kotlin
interface Switcher { // 인터페이스의 선언
	fun on(): String
}

class Smartphone(val model: String){
    ...
    fun powerOn(): String {
        class Led(val color: String){ // 지역 클래스 선언
        	fun blink(): String = "Blinking $color on $model" 
        }
        val powerStatus = Led("Red") 
        val powerSwitch = object : Switcher { // 익명 객체를 사용해 Switcher의 on()을 구현
            override fun on(): String {
                return powerStatus.blink()
            }
        }
        return powerSwitch.on() // 익명 객체의 메서드 사용
    }
}
```

스위치를 위한 인터페이스 `Switcher`를 선언하고 이후 Smartphone 클래스의 powerOn() 메서드를 수정한다. object를 사용해 `Switcher` 인터페이스의 on() 메서드를 구현하고 있다. `Switcher` 인터페이스로부터 만들어진 객체는 이름이 없으며 `powerSwitch` 프로퍼티를 위해 일회성으로 사용된다. 이 메서드가 호출될 때마다 일회성 객체의 인스턴스가 만들어진다.

<br>

#### 열거형 클래스

열거형 클래스란 **여러 개의 상수를 선언하고 열거된 값을 조건에 따라 선택**할 수 있는 특수한 클래스이다. enum 키워드와 함께 선언할 수 있고 , 자료형이 동일한 상수를 나열할 수 있다.

+ 각 상수는 Direction 클래스의 객체로 취급되고 쉼표로 구분한다. 

  ```kotlin
  enum class Direction{
      NORTH, SOUTH, WEST, EAST
  }
  ```

<br>

+ 주 생성자를 가지고 값을 초기화 할수도 있다. 다음은 각 요일마다 숫자를 지정한 열거형 클래스이다.

  ```kotlin
  enum class DayOfWeek(val num: Int){
      MONDAY(1), TUESDAY(2). WEDNESDAY(3), THURSDAY(4),
      FRIDAY(5), SATURDAY(6), SUNDAY(7)
  }
  
  val day = DayOfWeek.SATURDAY 
  when(day.num) {
      1, 2, 3, 4, 5 -> println("Weekday")
      6,7 -> println("Weekend!")
  }
  ```

<br>

+ 필요한 경우 메서드를 포함할 수도 있다. 이때는 세미콜론(;)을 사용해 열거한 상수 객체를 구분해야 한다. 





Q) 뭔가 상수를 써야할 때,  companion object를 써야하나, enum class를 써야 하나 ? 둘의 용도의 차이?



#### 애노테이션 클래스

Annotation은 코드에 부가 정보를 추가하는 역할을 한다. @ 기호와 함께 나타내는 표기법으로 주로 컴파일러나 프로그램 실행 시간에서 사전 처리를 위해 사용한다. 예를 들어 `@Test`는 유닛 테스트를 위해 사용하고 `@JvmStatic`은 자바 코드에서 컴패니언 객체를 접근 가능하게 한다. 

애노테이션 클래스를 직접 만드는 것은 사실 고급 기법에 해당하기 때문에 프레임워크를 제작하지 않는 한 사용할 일은 별로 없다. 오히려 **프레임워크에서 제공하는 애노테이션을 사용하는 경우가 많다.** 애노테이션을 선언하고 사용하는 방법에 대해 대략적으로만 살펴보자



##### 애노테이션 선언

사용자 애노테이션을 만들기 위해서는 키워드 **annotation**을 사용해 클래스를 다음과 같이 선언하다. 

```kotlin
annotation class Fancy // 애노테이션 선언

@Fancy class MyClass{...} // 사용
```

<br>



## 🚩 7 - 3 연산자 오버로딩

#### 연산자의 작동 방식

연산자를 사용하면 관련된 멤버 메서드를 호출하는 것과 같다. 예를 들어 a + b는 `a.plus(b)`라는 함수가 내부적으로 호출되는 것이다. 사실 +와 - 같은 연산자는 기본적으로 많은 자료형을 처리하기 위해 이미 오버로딩되어 있다. 

코틀린 표준 라이브러리에서 Primitives.kt를 살펴보면 operator 키워드를 사용해 **plus() 함수가 다양한 자료형으로 선언되어 있는 것**을 알 수 있다. 오버로딩되어 있는 것이다. 

<br>

#### 연산자의 종류

+ 산술 연산자

  +, -, *, /, %, ..

+ 호출 연산자

  함수 호출을 돕는데 사용된다. **특정 객체에 인수를 넣어 처리**하기 위해 다음과 같은 표현이 가능하다.

  ```kotlin
  class Manager {
      operator fun invoke(value: String){
          println(value)
      }
  }
  
  fun main() {
      val manager = Manager()
      manager("Do something for me !") // manager.invoke("...") 형태로 호출되며 invoke가 생략됨
  }
  ```

  Manager 클래스에는 invoke가 선언되어 Manager 클래스를 통해 생성한 객체 manager라는 이름만으로 접근해 사용할 수 있다. 원래는 manager.invoke("...") 형태로 호출되어야 하지만 invoke를 생략하고 객체 이름만 작성해서 코드를 읽기가 수월해진다.

+ 인덱스 접근 연산자

  게터와 세터를 다루기 위한 대괄호(`[]`) 연산자를 제공한다. 인덱스 표기법을 통해 값을 읽어 오거나 쓰기가 가능하다.

+ 범위 연산자 

  in 연산자는 특정 객체를 반복하기 위해 반복문에 사용하거나 범위 연산자와 함께 포함 여부를 판단할 수도 있다. 

+ 대입 연산자

  대입 연산자는 연산의 결과를 할당한다. 예를 들어 `a += b`는 `a + b`의 연산 결과를 다시 `a`에 할당한다. 주의해야 할 것은 +에 대응하는 `plus()`를 오버로딩 하면 `+=`는 자동으로 구현된다. 따라서 `plusAssign()`을 따로 오버로딩할 필요가 없다. 

+ 동등성 연산자

  일치와 불일치에 대한 연산자는 두 객체의 값의 동등성을 판별한다. 	

<br>

