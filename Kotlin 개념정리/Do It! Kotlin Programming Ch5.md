# Do It! Kotlin Programming Ch5

## 클래스와 객체

-----

## 🚩 5 - 1 클래스와 객체의 정의

#### 📌객체 지향 프로그래밍

객체 지향 프로그래밍은 **프로그램의 구조를 객체 간 상호작용으로서 표현**하는 프로그래밍 방식이다. 컴퓨터 언어 분야에서 기존 절차적 프로그래밍의 한계를 극복하고자 나온 방법론 중 하나다. 코틀린은 함수형 프로그래밍과 더불어 객체 지향 프로그래밍 기법을 지원한다.

<br>

##### 객체 지향 프로그래밍의 특징

+ 추상화 : 특정 클래스를 만들 때 기본 형식을 규정하는 방법
+ 인스턴스 : 특정 클래스로부터 생성한 객체
+ 상속 
+ 다형성 : 하나의 이름으로 다양한 처리를 제공
+ 캡슐화 : 내용을 숨기고 필요한 부분만 사용
+ 메시지 전송 : 객체 간에 주고받는 메시지
+ 연관 : 클래스 간의 관계 

<br>

자바에서는 변수를 필드, 함수를 메서드라고 부르는데 코틀린에서는 변수를 필드가 아닌 **프로퍼티**라고 부른다. 그 이유는 **변수에 내부적으로 접근 메서드가 포함되어 있기 때문**

<br>

클래스의 멤버가 될 수 있는 것

+ 생성자, 초기화 블록 : 객체가 생성될  때 자동 실행되는 메서드 또는 코드 블록
+ 프로퍼티 : 변수의 이름과 변수의 접근 함수가 포함된 형태
+ 메서드 : 일반적인 함수의 형태
+ Nested class & Inner class : 클래스 내부에 구성되는 클래스
+ 객체 선언 : 클래스 없이 접근할 수 있는 객체 

<br>

##### 클래스 다이어그램

+ 클래스 다이어그램 : 클래스의 정의와 관계를 나타내는 다이어그램으로 UML 기법중 하나이다.

  > UML(통합 모델링 언어) :  객체 지향 프로그램 설계를 위한 다이어그램 표기법

  <img src = "https://user-images.githubusercontent.com/31370590/139712561-de78823b-b84a-4a94-ae9f-09610eecfda5.PNG">

  + 다음과 같이 3개의 상자로 이루어져 클래스 이름, 프로퍼티, 메스드를 손쉽게 파악할 수 있다. **+**는 public을 의미하고, **-** 는 private을 의미한다.

<br>

#### 클래스와 추상화

**추상화**란 

목표로 하는 대상에 대해 필요한만큼 속성과 동작을 정의하는 과정 

예를 들면, 인간이라는 기본 개념을 정의하고 새롭게 발견한 개별적인 새의 일반적인 행동(함수)와 특징(속성)을 알아낸다.

=> 즉, **어떤 대상을 클래스로 만드는 과정**

<br>

##### 클래스 선언하기

```kotlin
class Bird { }
class Bird // 내용이 비어있을 때 중괄호 생략 가능 
```

<br>

##### 클래스와 객체

+ **클래스로부터 객체를 생성**해야만 비로소 클래스라는 개념의 실체인 객체가 물리적인 메모리 영역에서 실행된다.

  => 이를 객체 지향 언어에서 **구체화** 또는 **인스턴스화** 되었다고 이야기한다. 그래서 메모리에 올라간 객체를 인스턴스라고 한다. 

<br><br><br>

-----

## 🚩 5 - 2 생성자

클래스 안의 프로퍼티 값을 직접 입력하여 초기화해도 되지만 이렇게 하면 항상 같은 프로퍼티 값을 가지는 객체가 만들어진다. **객체를 생성할 때 필요한 값을 설정하여 객체를 만들면 훨신 유연할 것**이다. 

<br>

생성자

+ 주 생성자(Primary Constructor)
+ 부 생성자(Secondary Constructor)

<br>

생성자를 선언하는 위치

```kotlin
class 클래스 이름 constructor(필요한 매개변수..) { // 주 생성자의 위치
	...
	constructor(필요한 매개변수..) { // 부 생성자의 위치
    	// 프로퍼티의 초기화
    }
    
	constructor(필요한 매개변수..) { // 추가 부 생성자
        ...
    } 
}
```

+ 부 생성자를 여러 개 사용할 때는 **매개변수를 다르게 정의**해야 한다.

<br>

#### 📌 부 생성자

부 생성자 정의 예시

```kotlin
class Bird{
    var name: String
    var wing: Int
    var beak: String
    var color: String
    // 이렇게 초기화없이 선언되어 있어도 되지만, 객체가 생성될때는 주생성자를 사용하던 부생성자를 사용하던 프로퍼티 값을 설정해줘야 한다
    
    // 부 생성자
    constructor(name: String, wing: Int, beak: String, color: String){
        this.name = name // this.name은 선언된 현재 클래스의 프로퍼티를 나타냄
        this.wing = wing
        this.beak = beak
        this.color = color
    }
    
    fun fly() = ~
    fun sing(vol: Int)
}
```

<br>

#### 📌 주 생성자

주 생성자는 클래스 이름과 함께 생성자 정의를 이용할 수 있는 기법이다. 주 생성자는 클래스 이름과 블록 시작 부분 사이에 선언한다.

```kotlin
class Bird constructor(_name: String, _wing: Int, _beak: String, _color: String {
    // 프로퍼티
    var name: String = _name
    var wing: Int = _wing
    var beak: String = _beak
    var color: String = _color
    
    fun fly() = ~
    fun sing(vol: Int) = ~
}
```

+ 주 생성자의 constructor 키워드는 생략할 수 있다. 

  접근 지시자가 annotation 표기가 클래스 선언에 있으면 생략할 수 없다.

<br>

### 클래스에 주 생성자가 없어도 될까? 



















=> 없어도 된다. 대신 객체를 생성할 때 클래스의 프로퍼티는 클래스 내부에서 초기화해주던, 부생성자를 이용해서 초기화해주던지 해야한다. 주 생성자가 없는 클래스는 괄호가 붙지 않는다. 

ex) `class A : Base { ... }`

<br>

##### 프로퍼티를 포함한 주 생성자

내부의 프로퍼티를 생략하고 **생성자의 매개변수에 프로퍼티 표현을 함께 넣을 수 있다**. ***val, var를 사용하여 매개변수를 선언***하면 생성자에서 this 키워드를 사용하거나 언더스코어를 사용할 필요가 없다.

```kotlin
class Bird constructor(var _name: String, var _wing: Int, var _beak: String, var _color: String) {
    // 프로퍼티는 매개변수 안에 var를 사용해 프로퍼티로서 선언되어 본문에서 생략됨
    
    // 메서드    
    fun fly() = ~
    fun sing(vol: Int) = ~
}

fun main(){
    val coco = Bird("mybird", 2, "short", "blue")
}                       
```

또한, 생성자의 매개변수에 기본값을 사용할 수도 있다. 그러면 객체를 생성할 때 기본값이 있는 인자는 생략할 수 있다. 

```kotlin
class Bird constructor(var name: String = "minwoo", var wing: Int = 2, var beak: String, var color: String) {
    ...
}

fun main(){
    val coco = Bird(beak = "long", color = "blue") 
    // 여기서 beak와 color는 프로퍼티 이름과 동일하게 써준 것
}
```

<br><br>

##### 초기화 블록을 가진 주 생성자

그러면 객체를 생성할 때 **프로퍼티를 초기화하는 것 이외에 코드를 실행**할 수는 없을까? 생성자는 기본적으로 함수를 표현하는 기능이기 때문에 변수를 초기화하는 것 말고도 특정 작업 가능하다. 

단, 클래스 이름 다음에 주 생성자를 표현하는 경우 클래스 블록(`{ }`) 안에 코드를 넣을 수 없다. 초기화에 꼭 사용해야 할 코드가 있다면 `init { ... }` 초기화 블록을 클래스 선언부에 넣어 주어야 한다. 

```kotlin
class Bird constructor(var _name: String, var _wing: Int, var _beak: String, var _color: String {
    
    // 초기화 블록
    init {
        printlm("-----초기화 블록-----")
        this.sing(3) 
    }
```

+ init 초기화 블록에서는 출력문이나 프로퍼티, 메서드 등과 같은 코드를 사용할 수 있다. 

+ init 초기화 블록은 주 생성자가 실행될 때 실행된다 ? 

  => 어떤 생성자를 통해 생성되든, 객체가 생성될 때 실행된다. 

<br>

### init 초기화 블록은 주 생성자가 아닌 부 생성자를 이용해 객체를 생성할 때도 실행될까?

```kotlin
class E {

 var name: String
 var age: Int = 1
 var height: Int = 2

 init {
     println("call Init Block!")
 }

 constructor(name: String) {
     this.name = name
     println("call Name Constructor!")
 }

 constructor(name: String, age: Int) : this(name) {
     this.age = age
     println("call Name, Age Constructor!")
 }

 constructor(name: String, age: Int, height: Int) : this(name, age) {
     this.height = height
     println("call Name, Age, Height Constructor!")
 }
}

fun main(){
 var e = E("박민우", 24, 180)
}
```

```kotlin
출력결과
call Init Block!
call Name Constructor!
call Name, Age Constructor!
call Name, Age, Height Constructor!
```

초기화 블럭 안의 코드는 효과적으로 기본 생성자의 일부가 된다. 기본 생성자로의 위임은 **보조 생성자의 첫번째 문장으로 발생**한다. 그래서 모든 초기화 블럭내의 코드는 보조 생성자 몸체 전에 실행된다**. 클래스가 주 생성자를 가지지 않을때도 위임은 여전히 암시적으로 발생하고, 초기화 블럭은 여전히 실행된다.**

<br>

>  클래스에 주 생성자가 정의되어 있다면, **부 생성자는 무조건 주 생성자를 호출해야 한다.**
>
> ```kotlin
> class A(val name: String) {
> 
>     var age: Int = 20
>     var height: Int = 500
> 
> //    컴파일 에러!
> //    constructor(name: String, age: Int) {
> // 		  this.name = name
> //        this.age = age
> //    }
>     // 클래스의 모든 프로퍼티를 초기화했더라도 주 생성자를 호출하지 않았기 때문에
> 
>     constructor(name: String, age: Int) : this(name) {
>         this.age = age
>     }
> 
>     constructor(name: String, age: Int, height: Int) : this(name, age) {
>         this.height = height
>     }
> }
> ```

<br><br><br>

------

## 🚩 5 - 3 상속과 다형성

**다형성**이란 메서드가 같은 이름을 사용하지만 구현 내용이 다르거나 매개변수가 달라서 하나의 이름으로 다양한 기능을 수행할 수 있는 개념이다.

<br>

### 📌 상속과 클래스의 계층

코틀린의 모든 클래스는 **Any 클래스**의 하위 클래스가 되며, 상위 클래스를 명시하지 않으면 Any 클래스를 상속 받게 된다. 

<br>

클래스가 상속할 수 있는 상태가 되려면 **open** 키워드와 함께 선언해야 한다. 코틀린은 open 없이 기본으로 클래스를 선언하면 상속할 수 없는 기본 클래스가 된다. 

<br>

상속을 위한 기본 구조

```kotlin
open class 기반클래스이름 { // 묵시적으로 Any로부터 상속됨, open으로 파생가능
    ...
}
class 파생클래스이름 : 기반클래스이름( ) { // 기반 클래스로부터 상속됨, 최종 클래스로 파생 불가
    ...
}
```

+ 변수 선언과 클래스 상속이 똑같은 콜론(`:`) 기호를 사용하므로 클래스 이름 오른쪽에 소괄호나 블록의 유무에 따라 이를 구분 가능하다. 
+ 클래스를 선언할 때 콜론 앞뒤에 공백이 있다. 변수 선언처럼 공백 없이 붙여 써도 문제 없지만, 클래스 선언과 변수 선언을 구분하기 위한 일종의 코딩 관례이다.
+ 상속받는 하위 클래스는 **상위 클래스의 생성자를 최소한 동일하게 정의하거나 확장**할 수 있다. 

<br><br>

파생 클래스 만들어보기

```kotlin
// 1️⃣ 상속 가능한 클래스를 선언하기 위해 open 사용
open class Bird constructor(var name: String, var wing: Int, var beak: String, var color: String) {
    // 메서드
    fun fly() = ~
    fun sing(vol: Int) = ~
}

// 2️⃣ 주 생성자를 사용하는 상속
class Lark(name: String, wing: Int, beak: String, color: String) : Bird(name, wing, beak, color){
    fun singHitone( ) = println("Happy Song!") // 새로 추가한 메서드
}

// 3️⃣ 부 생성자를 사용하는 상속
class Parrot : Bird{
    val language: String
    
    constructor(name: String, 
                wing: Int, 
                beak: String, 
                color: String, 
                language: String) : super(name, wing, beak, color){
        this.language = language // 새로 추가한 프로퍼티
    }
    
    fun speak() = ~ // 새로 추가한 메ㅓㅅ드
}

fun main(){
    val coco = Bird("mybird", 2, "short", "blue")
    val lark = Lark("mylark", 2, "long", "brown")
    val parrot = Parrot("myparrot", 2, "short", "multiple", "korean")  
}
```

+ 1️⃣번에서 상속을 위해 open 키워드를 사용해 Bird 클래스 정의
+ 2️⃣번에서 **주 생성자를 이용**하는 방법으로 파생 클래스 Lark 선언, 이때 상위 클래스인 Bird 클래스에 생성자에 사용하는 매개변수와 인자들을 지정해야 한다. 

+ 3️⃣번 Parrot 파생 클래스는 **부 생성자를 이용**하는 방법으로 선언했는데 이때는 본문 내부에 constructor()를 이용한다. 객체를 생성할 때 여기서 기존의 프로퍼티에 Parrot 클래스를 위해 하나 더 추가된 프로퍼티 language를 초기화해 확장되었다. 

<br><br>

### 📌 다형성

+ 오버로딩 : 동작은 동일하지만 인자의 형식만 달라지는 것
+ 오버라이딩 : 메서드나 프로퍼티의 이름은 같지만 기존의 동작을 다른 동작으로 재정의하는 것

<br>

##### 오버로딩

```kotlin
fun add(x: Int, y: Int): Int{ // 정수형 매개변수 2개를 더함 
    return x + y
}

fun add(x: Double, y: Double): Double{ // 실수형 매개변수 2개를 더함 
    return x + y
}

fun add(x: Int, y: Int, z: Int): Int{ // 정수형 매개변수 2개를 더함 
    return x + y + z
}
```

+ 동일한 클래스 안에서 같은 이름의 메서드가 매개변수만 달리해서 여러 번 정의될 수 있는 것. 반환 값은 동일하거나 다를 수 있다. 구현되는 동작은 대부분 동일하다.

+ 클래스의 메서드뿐만 아니라 일반 함수도 오버로딩이 가능하다. 

  보통 코틀린에서 오버로딩은 연산자에 대해 다양한 자료형을 받아들일 수 있도록 연산자에 많이 사용하고 있다.

<br>

##### 오버라이딩

하위 클래스에서 새로 만들어지는 메서드가 ***이름이나 매개변수, 반환값이 이전 메서드와 동일하지만 내용이 새로 작성***되는 것.

코틀린에서는 기반 클래스의 내용을 파생 클래스가 오버라이딩하기 위해 기반 클래스에서는 open 키워드, 파생 클래스에서는 override 키워드를 각각 사용한다. 메서드 뿐만 아니라 **프로퍼티도 오버라이딩**할 수 있다. 

override 키워드 앞에 final 키워드를 사용해 하위 클래스에서 재정의 되는 것을 막을 수 있다.  

```kotlin
open class Bird{ // open은 상속 가능을 나타냄
...
	open fun fly( ) {...}
	open fun sing( ) {...} // sing 메서드는 하위 클래스에서 오버라이딩 가능
}

class Lark( ) : Bird( ){
    override fun sing( ) { /* 구현부를 새롭게 재정의 */}
    final override fun fly( ) { } // fianl을 통해 Lark의 하위 클래스에서 재정의되는 것을 막을 수 있다. 
}
```

<br><br><br>

-----

## 🚩 5 - 4  super과 this의 참조

클래스를 상위와 하위 클래스로 설계하다 보면 때로는 **상위와 현재 클래스의 특정 메서드나 프로퍼티, 생성자를 참조해야 하는 경우**가 생긴다. 상위 클래스는 super 키워드로, 현재 클래스는 this 키워드로 참조가 가능하다.

super

+ super.프로퍼티 이름 => 상위 클래스의 프로퍼티 참조
+ super.메서드 이름() => 상위 클래스의 메서드 참조
+ super( ) => 상위 클래스의 생성자 참조

this

+ this.프로퍼티 이름 => 현재 클래스의 프로퍼티 참조
+ this.메서드 이름() => 현재 클래스의 메서드 참조
+ this( ) => 현재 클래스의 생성자 참조

<br>

### 📌 super

메서드를 오버라이딩하려고 할 때 만일 상위 클래스에서 구현한 내용을 그대로 사용하고 거기에 필요한 내용만 추가하고 싶을 수도 있다. 이 때 super 키워드를 사용해 **상위 클래스의 프로퍼티나 메서드, 생성자를 참조**할 수 있다.

```kotlin
// 상속 가능한 클래스를 선언하기 위해 open 사용
open class Bird constructor(var name: String, var wing: Int, var beak: String, var color: String) {
    // 메서드
    fun fly() = ~
    fun sing(vol: Int) = ~
}

class Parrot(name: String, wing: Int = 2, beak: String, color: String, 
            var language: String= "natural") : Bird(name, wing, beak, color){
    
    fun speak() = println("Speak! $language")
    
    override fun sing(vol: Int) {// 상위 클래스의 내용과 다르게 새로 구현
		super.sing(vol) // 상위 클래스의 sing()을 먼저 수행
        println("I'm a parrot! The volume level is $vol")
        speak()
    }
}

```

<br>

### 📌 this

this를 이용해 **현재 객체의 클래스**의 프로퍼티, 메서드, 생성자 등을 참조할 수 있다. 

<br>

#### this로 현재 객체 참조하기

##### 여러개의 부 생성자에서 참조하기

```kotlin
open class Person{ // 상속 가능한 class
    constructor(firstName: String){ // 부 생성자
        println("[Person] firstName: $firstName")
    }
    
    constructor(firstName: String, age: Int){ // 부 생성자
        println("[Person] firstName: $firstName, age: $age")
    }
}

class Developer : Person {
    constructor(firstName: String): this(firstName, 10) { // 1️⃣
    	println("[Developer] $firstName")
    }
    
    constructor(firstName: String, age: Int): super(firstName, age) { // 2️⃣
    	println("[Developer] $firstName")
    }
}

fun main(){
    val sean = Developer("Sean")
    sean.firstName
}
```

+ **this( )**는 현재 클래스의 생성자를 참조하기 때문에 `constructor(firstName: String): this(firstName, 10)` 에 의해 `firstName`과 `10`을 인자로 가지고 Developer 클래스의 다른 생성자를 호출한다.  여기서 `this( )`는 2개의 인자를 가진 부 생성자인 2️⃣번을 가리킨다.

  => 즉, ***`this( )`는 현재 클래스의 생성자 중 `this( )`에 전달된 인자와 같은 형식의 매개변수를 가지는 생성자를 참조한다.*** 

  같은 맥락으로, ***`super( )`도 상위 클래스의 생성자 중 `super( )`에 전달된 인자와 같은 형식의 매개변수를 가지는 생성자를 참조한다.***

  > `constructor(firstName: String): this(firstName, 10)`에서  **`:`**는 constructor라는 함수의 반환 타입을 가리키는 것? 아니면 상속을 나타내는 것?


<br>

+ 상속을 통해서 클래스를 만드는 경우에는 ***상위 클래스의 생성자가 있다면 반드시 하위 클래스에서 호출해야 한다***. 따라서 생성자 코드를 실행하기 전에 현재 클래스를 가리키는 this나 상위 클래스를 가리키는 super를 사용해 위임하며 다른 생성자를 처리할 수 있게 된다.

  > 상속 시, 상위 클래스의 생성자가 있다면 이를 반드시 하위 클래스에서 호출해야 하고,
  >
  > 비슷한 맥락으로 한 클래스 내에 주생성자가 존재한다면 부생성자는 무조건 주생성자에게 직간접적으로 생성을 위임해야 한다. 즉, **부생성자는 무조건 주생성자를 호출해야 한다.** 

<br>



### 위 코드에서 class `Person`의 프로퍼티는 ? 

부 생성자에 매개변수로 정의되어 있는 `firstName: String, age: Int`는`Person` 클래스의 프로퍼티가 아니다. 

=> 클래스의 프로퍼티 일려면 

+ 주 생성자의 매개변수에 var이나 val로 선언되어 있거나
+ 클래스 내부에 var나 val로 선언되어 있어야 한다.

<br><br>

##### 주 생성자와 부 생성자 함께 사용하기

<img src = "https://user-images.githubusercontent.com/31370590/139847860-ad28aaec-9a4f-4133-a79a-6d5814bbe669.PNG">

+ 이 코드의 **this( )**는 주 생성자를 가리킨다.
+ `out`이라는 인자에 `println( )`을 기본값으로 할당해 인자에 접근할 때 출력되도록 했다.
+ `fName`이라는 프로퍼티에도 출력문을 할당했다. 

<br>

####  바깥 클래스 호출하기

클래스를 선언할 때 클래스 안에 다시 클래스를 선언하는 것이 가능하다. 이 때 특정 클래스 안에 선언된 클래스를 **이너 클래스**라고 한다. 

이너 클래스에서 바깥 클래스의 상위클래스를 참조하려면 **super** 키워드와 함께 @ 기호 옆에 바깥 클래스 이름을 작성한다.

```kotlin
open class Base{
    open val x: Int = 1 // 프로퍼티에 open 붙이면 오버라이딩 가능을 나타냄
    open fun f( ) = println("Base Class f( )")
}

class Child : Base() {
    override val x: Int = super.x + 1
    override fun f( ) = println("Child Class f( )")
    
    
    // 이너 클래스
    inner class  Inside {
        fun f( ) = println("Inside Class f( )")
        fun test( ){
            f( ) // 현재 이너 클래스의 f() 접근
            Child( ).f( ) // 바로 바깥 클래스의 f( ) 접근
            super@child.f( ) // child의 상위 클래스인 base 클래스의 f( ) 접근
            println("[Inside] super@Child.x: ${super@Child.x}")
        }
    }
}

fun main( ){
    val c1 = Child( )
    c1.Inside( ).test( ) // 이너 클래스 Inside의 메서드 test( ) 실행
}
```

+ ` c1.Inside( ).test( )`

  Inside 클래스의 객체를 생성하고 test( ) 메서드를 호출하기 위해 다음과 같이 작성되었다. c1 객체에 이너 클래스인 Inside( )에 생성자 표기로 접근하고 다시 test( ) 메서드에도 각각 점(.)으로 접근하고 있다. 

<br>

#### 인터페이스에서 참조하기

인터페이스는 일종의 구현 약속으로 인터페이스를 참조하는 클래스는 인터페이스가 가지고 있는 내용을 구현해야 하는 가이드를 제시한다. 따라서 인터페이스 자체로는 객체로 만들 수 없고 항상 **인터페이스를 구현하는 클래스에서 객체를 생성**해야 한다.

코틀린에서는 자바처럼 한 번에 2개 이상의 클래스를 상속받는 다중 상속이 되지 않지만 인터페이스로는 필요한 만큼 다수의 인터페이스를 지정해 구현할 수 있다. 이 때 각 인터페이스의 프로퍼티나 메서드의 이름이 중복될 수 있다. 만일 동일한 이름의 프로퍼티나 메서드가 있다면 앵글 브래킷(`< >`)을 사용해 접근하려는 클래스나 인터페이스의 이름을 정해준다. 

<br><br><br>

-----

## 🚩 5 - 5 정보 은닉 캡슐화

### 📌 가시성 지시자

**가시성(visibility)**이란 각 클래스나 메서드, 프로퍼티의 접근 범위를 말한다. 불필요한 부분은 숨기고 사용하기 위해 필요한 부분만 공개하듯이, 각 클래스나 메서드 ,프로퍼티에 가시성 지시자에 의해 공개할 부분과 숨길 부분을 정해줄 수 있다. 

> + private : 외부에서 접근 불가능
> + public : 어디서든 접근 가능 (기본값)
> + protected : 외부에서 접근 불가능, 하위 상속 요소에서는 가능
> + internal : 같은 정의의 모듈 내부에서 접근 가능

<br>

<img src = "https://user-images.githubusercontent.com/31370590/140081464-711fddf0-5942-418b-bbbe-695e163f8b5f.PNG">

<br>

##### private

private은 접근 범위가 선언된 요소에 한정하는 가시성 지시자이다. 클래스를 private과 함께 선언하면 그 클래스 안의 멤버만 접근할 수 있다.

```kotlin
private class PrivateClass {
    private var i = 1
    private fun privateFunc(){
        i += 1 // 🆗 
    }
    fun access() {
        privateFunc() // 🆗 
    }
}

class OtherClass {
    val opc = PrivateClass() // ❌ - 프로퍼티 opc가 private이어야 함
    
    fun test(){
        val pc = PivateClass() // 🆗 왜 여기는 접근 허용????????????????????????????????????/
    }
}

fun main(){
    val pc = PrivateClass() // 🆗
    pc.i // ❌
    pc.privateFunc // ❌
}

fun TopFunction(){
    val tpc = PrivateClass() // 🆗
}
```

+ `PrivateClass`는 private으로 선언되어 있으므로 다른 파일에서 접근할 수 없다. 같은 파일에서는 `PrivateClass`의 객체를 생성할 수 있다. 만일 다른 클래스에서 프로퍼티로서 `PrivateClass`의 객체를 지정하려면 똑같이 private으로 선언해야 한다. 
+ 객체를 생성했더라도 `PrivateClass`의 멤버인 `i`와 `privateFunc()` 메서드가 private으로 선언되었기 때문에 다른 클래스나 main() 같은 최상위 함수에서 접근할 수 없다. private으로 선언된 멤버는 해당 클래스 내부에서만 접근이 가능하다.  

<br>

##### Protected

protected 지시자는 최상위에 선언된 요소에는 지정할 수 없고 **클래스나 인터페이스와 같은 요소의 *멤버에만 지정할 수 있다***. 단, 멤버가 클래스인 경우에는 protected로 선언할 수 있다.(이너 클래스?)

<br>

##### Internal

internal은 프로젝트 단위의 모듈을 가리킨다. 모듈이 달라지면 접근할 수 없다. 기존의 자바에서는 package라는 지시자에 의해 패키지 이름이 같은 경우에 접근을 허용했다. 코틀린에서는 패키지에 제한하지 않고 하나의 모듈 단위를 대변하는 internal 지시자를 사용한다. 만일 프로젝트에 또 다른 모듈이 없고 하나만 있는 경우 internal의 접근 범위는 프로젝트 전체가 된다. 

<br><br>

### 📌 가시성 지시자와 클래스의 관계

가시성 지시자는 클래스 간의 관계에서도 접근 범위를 정할 수 있기 때문에 상속된 하위 클래스에서 가시성 지시자를 사용하거나 다른 클래스와의 연관 관계를 지정하지 위해서도 사용할 수 있다. 

##### UML의 가시성 표시 기호

+ `-` : private
+ `+` : public
+ `#` : protected 
+ `~` : package

<img src = "https://user-images.githubusercontent.com/31370590/140083814-b224b730-7e7a-4973-8504-bf20ef05608c.PNG">

+ 오버라이딩 된 멤버가 있는 경우에는 상위 클래스와 동일한 가시성 지시자를 갖는다. 

<br><br><br>

## 🚩 5 - 6 클래스와 클래스의 관계

#### 📌 클래스 혹은 객체 간의 관계

클래스들 간에 관계가 만들어지고 메시지를 전달하면서 복잡한 현실 세계와 비슷하게 프로그래밍을 설계할 수 있다. 

클래스들이나 객체들 사이의 관계는 약하게 연결된 관계부터 강하게 결합된 관계가 있다.



<img src="https://user-images.githubusercontent.com/31370590/140088396-b28097ec-7200-409c-93a9-c6f774cad35d.PNG">

+ 약하게 참조되고 있는 관계 : 의존(dependency), 연관(association) 

  => 소유의 개념 없이 어떤 객체에서 또 다른 객체를 이용

<br>

##### 연관 관계

2개의 **서로 분리된 클래스가 연결을 가지는 것**. 단방향 혹은 양방향으로 연결될 수 있다. 핵심은 두 요소가 **서로 다른 생명주기**를 가지고 있다는 점.

=> 그냥 단순히, 다른 클래스에서 한 클래스를 **사용** 하는 것.

```kotlin
class Patient(val name: String) {
    fun doctorList(d: Doctor) { // 인자로 참조 
        println("Patient: $name, Doctor: ${d.name}")
    }
}

class Doctor(val name: String) {
    fun patientList(p: Patient) { // 인자로 참조 
        println("Doctor: $name, Patient: ${p.name}")
    }
}

fun main() {
    val doc1 = Doctor("Jaehoon") // 객체가 따로 생성
    val patient1 = Patient("Minwoo")
    doc1.patientList(patient1)
    patient1.doctorList(doc1)
}
```

+ Doctor와 Patient 클래스의 객체는 따로 생성되며 서로 독립적인 생명주기를 가지고 있다. 이 코드에서는 두 클래스가 서로의 객체를 함수의 인자로 참조하고 있으므로 양방향 참조이다. 단방향이든 양방향이든 **각각의 객체의 생명주기에 영향을 주지 않을 때는 연관 관계라고 한다.** 

<br>

##### 의존 관계

한 클래스가 다른 클래스에 의존되어 있어 영향을 주는 경우

아까 예를 조금 변형해, Doctor 클래스를 생성하려고 하는데, 먼저 Patient의 객체가 필요한 경우

=> Doctor 클래스의 프로퍼티 중 `val p: Patient`가 있어서 주 생성자에 Patient 객체를 매개변수로 받아야 하므로 Patient 객체가 먼저 생성되어 있어야 한다. 즉 **서로가 객체의 생명주기에 영향을 준다.** 

```kotlin
class Doctor(val name: String, val p: Patient) { ... }
```

<br>

##### 집합 관계

연관 관계와 거의 동일하지만 **특정 객체를 소유한다는 개념이 추가**

앞에서 연못과 오리의 예에서 오리가 특정 연못을 주거지로 삼는다면 연못이 오리를 소유할 수 있는 것.

=> 두 객체는 **서로의 생명주기에 영향을 주지 않음** 

```kotlin
// 여러 마리의 오리를 윙한 List 매개변수
class Pond(_name: String, _members: MutableList<Duck>) {
    val name: String = _name
    val members: MutableList<Duck> = _membbers
    
    constructor(_name: String): this(_name, mutableListOf<Duck>( ))
}

class Duck(val name: String)
```

+ 의존관계처럼 `Pond` 클래스의 프로퍼티 중 `Duck` 클래스의 객체가 있어서 `Pond` 클래스를 사용하기 위해 `Duck` 클래스의 객체가 먼저 생성되어 있어야 할 것처럼 보이지만, 

  부생성자를 통해 `mutableListOf<Duck>( )`를 넣어줌으로써 `Duck` 클래스의 객체가 없어도 `Pond` 클래스의 객체가 생성될 수 있으므로  **서로의 생명주기에 영향을 주지 않는다.**

<br>

##### 구성 관계

집합 관계와 거의 동일하지만 **특정 클래스가 어느 한 클래스의 부분이 되는 것**이다. 구성품으로 지정된 클래스는 **생명주기가 소유자 클래스에 의존되어 있다**. 소유자 클래스가 삭제되면 구성하고 있던 클래스도 같이 삭제 된다. 

```kotlin
class Car(val name: String, val power: String) {
    private var engine = Engine(power) // Engine 클래스는 Car에 의존적
    ...
}

class Engine(power: String){
    ...
}

fun main() {
    val car = Car("tico", "100hp")
}
```

`Engine` 클래스는 `Car` 클래스의 생명주기에 의존적이다. **car 객체를 생성함과 동시에 Engine 클래스의 객체도 생성된다.** 집합 관계와 달리 구성 관계에서는 만일 car 객체가 삭제되면 동시에 engine 객체도 삭제된다. 

=> 의존 관계에서는 어떤 클래스의 객체를 생성하기 위해 의존관계에 있는 클래스의 객체가 **먼저 생성되어 있었어야 했고**, 구성 관계에서는 어떤 클래스의 객체를 생성하면 이와 구성관계에 있는 객체가 **동시에 생성되고 소멸된다**는 특징이 있다. 

<br>

+ 의존되어 있으면 => 생명주기가 영향

<br>

=> 

중요한 건 이 두 클래스는 구성 관계다, 집합 관계다 를 판별하는게 아니라 우리가 구현하려는 목적에 따라 이 두 클래스간의 관계를 잘 설계하는 것. 

<br><br>

#### 📌 객체간의 메시지 전달하기

시간의 흐름에 따라 일어나는 경우가 대부분 => UML의 시퀀스 다이어그램으로 표현한다. 

보통 메시지는 **받는 수신자**와 **실행할 메서드**가 사용된다. 메서드에는 매개변수로 원하는 메시지를 보낼 수 있다. 

<br>

<br>





+ 객체를 선언할 때 val로 선언하는 이유는? val은 변경불가능 한데 객체의 프로퍼티를 바꾸는 경우가 있음 왜 그럴까?

  > val은 변경이 불가능한 것이 맞다. 하지만, 참조가 가리키는 객체의 내부값은 변경이 가능하다.

+ 주 생성자나 부 생성자는 모든 프로퍼티를 초기화해야하나?

  > 그건 아니지만 객체가 생성될 때, 모든 프로퍼티가 어떤 식으로든 초기화 되어 있어야 한다. 





