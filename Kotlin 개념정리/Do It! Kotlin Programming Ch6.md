# Do It! Kotlin Programming Ch6

## 프로퍼티와 초기화

-----

## 🚩 6 - 1 프로퍼티의 접근

코틀린의 클래스의 프로퍼티는 변수와 접근 메서드가 포함된 개념이다. 보통 변수에 접근하기 위해 사용하는 접근 메서드는 게터(Getter)와 세터(Setter)라고 부른다. 게터는 변수에서 값을 읽어 들이기 위한 메서드이며 세터는 값을 할당하기 위한 메서드이다. 코틀린에서 프로퍼티는 게터와 세터를 자동으로 만든다. 코틀린에서 **프로퍼티는 반드시 초기화되어야 하는데** 나중에 초기화할 수 있도록 lateinit과 lazy를 사용하는 기법이 있다. 

<br>

자바에서는 프로퍼티의 게터와 세터에 해당하는 접근 메서드를 직접 만들어야 했다. 따라서 자바의 필드가 점점 늘어나면 그와 상응하는 접근 메서드도 아주 많아지게 되어 코드가 아주 어려워진다. 

<br>

#### 📌 코틀린에서 게터와 세터가 작동하는 방식

``` kotlin
class User(val id: Int, var name: String, var age: Int)

fun main(){
    val user = User(1, "Sean", 30)
    
    val name = user.name // 게터에 의한 값 획득
    
    user.age = 41 // 세터에 의한 값 지정
    
    println("name: $name, ${user.age}")
}
```

+ 객체 user를 생성하고 점(`.`) 표기법으로 프로퍼티에 접근한다. `user.name`은 프로퍼티에 직접 접근하는 것처럼 보이나 코틀린 내부적으로 접근 메서드가 내장되어 있어 실제로는 `getName( )`과 같은 코틀린 내부의 게터 메서드를 통해 접근하는 것이다. `user.age = 41` 처럼 프로퍼티에 값을 할당하면 반대로 `setAge()`와 같은 세터 메서드를 사용하는 것이다. 

+ 그런데 여기서 **val**로 설정되어있던 **id**에 값을 할당하려고 시도하면 오류가 발생한다. **val로 선언된 프로퍼티는 값을 변경할 수 없는 읽기 전용이기 때문에** 값을 바꾸는 세터를 사용할 수 없다. 

  => ***val로 선언된 프로퍼티에는 세터가 정의되지 않고, 게터만 정의된다.*** 

<br>

#### 📌 기본 게터와 세터 직접 지정하기

게터와 세터가 포함되는 프로퍼티 선언에 대한 구조

```kotlin
var 프로퍼티_이름[: 프로퍼티_자료형] [= 프로퍼티_초기화]
	[get( ) { 게터_본문 }]
	[set(Value) { 세터_본문 }]

val 프로퍼티_이름[: 프로퍼티_자료형] [= 프로퍼티_초기화]
	[get( ) { 게터 본문 }]
```

<br>

게터와 세터 직접 지정하기 예제

```kotlin
class User(_id: Int, _name: String, _age: Int) {
    // 프로퍼티
    
    // val이니까 게터만
    val id: Int = _id
    	get() = field
    
    var name: String = _name
    	get() = field
    	set(value){
            field = value
        }
    
     var age: Int = _age
    	get() = field
    	set(value){
            field = value
            // this.name = value로 변환됨
        }
}
```

+ value와 field

  + value : 세터의 매개변수로 외부로부터 값을 가져옴
  + field : 프로퍼티를 참조하는 변수

  객체를 생성한 후, `user1.age = 35` 형태로 사용하면 35 정숫값이 매개변수 인자로 들어와 value에 할당된다. value라는 이름은 정해진 이름은 아니므로 다른 이름으로 변경해 사용할 수 있지만 field는 이름이 정해져 있어 변경할 수 없다. 

<br>

##### 보조 필드의 역할

field는 프로퍼티를 참조하는 변수로 보조필드라고도 한다. **get( ) = field**는 결국 각 프로퍼티의 값을 읽는 특별한 식별자이다. 

만일 게터와 세터 안에서 **field**대신 `get( ) = age`나 `set(value){ name = value }`처럼 사용하면 **프로퍼티의 `get()`과 `set()` 이 다시 호출되는 것과 같으므로 무한 재귀 호출에 빠져 스택 오버플로 오류가 발생할 수 있다.** 

그래서 임시적인 **보조 *필드***를 따로 사용해 프로퍼티 변수에 접근하는 것이다. set( ) 에도 값을 할당하기 위해 프로퍼티 이름을 직접 사용하지 않도록 주의해야 한다. 

```kotlin
set(value){
    name = value // 결국 자바로 변환되어 this.setName(value) 형태가 됨
    // 지속적으로 setName()이 계속 호출되다가 어느 순간 스택이 꽉 차게 되어 스택 오버플로 발생
}
```

<br><br>

#### 📌 커스텀 게터와 세터의 사용

단순히 값을 반환하거나 설정할 대는 굳이 게터와 세터를 따로 지정하지 않지만 **입력 문자를 대문자로 바꾸는 등의 특정 연산을 수행해야 한다면 게터와 세터를 확장해 코드를 구성할 수 있다.**

```kotlin
class User(_id: Int, _name: String, _age: Int) {
    // 프로퍼티
    
    // val이니까 게터만
    val id: Int = _id
    
    var name: String = _name
    	set(value){
            println("The name was changed")
            field = value.toUpperCase() // 받은 인자를 대문자로 변경
        }
    
    var age: Int = _age
}

fun main(){
    val user1 = User(1, "kildong", 36)
    user1.name = "coco" // 여기서 사용자 고유의 출력 코드가 실행
    println("user3.name = ${user1.name}")
}
```

+ 만약 보안 때문에 외부에서 name에 접근해서 변경할 수 없도록 하려면 `private` 가시성 지시자를 넣어줄 수 있다. 그러면 외부에서 객체 생성 후 `user.name = "test"`와 같이 값을 재할당하는 것이 금지된다. 

  ```kotlin
  var name: String = _name
      	private set(value){

<br>

##### 보조 프로퍼티의 사용

만일 보조 필드를 사용하지 않는 경우에는 **임시적으로 사용할 프로퍼티를 선언해놓고** 게터나 세터에서 사용할 수 있다. 

다음은 보조 프로퍼티 **tempName**을 정의하고 **name** 프로퍼티이 게터에서 임시로 사용한 예제이다.

<br>

##### 프로퍼티의 오버라이딩

프로퍼티는 기본적으로는 오버라이딩 할 수 없는 **final** 형태로 선언된다. 만일 프로퍼티를 오버라이딩 가능하게 하려면 **open** 키워드를 사용해 프로퍼티를 선언해야 한다. 

=> 오버라이딩 함으로써 프로퍼티의 구현부를 다르게 할 수 있음(ex) get()을 다르게 구현)

<br><br><br>

## 🚩 6 - 2 지연 초기화와 위임

프로퍼티를 선언하면 기본적으로 모두 초기화해야 한다. 하지만 객체의 정보가 나중에 나타나는 경우 객체 생성과 동시에 초기화하기 힘든 경우가 있다. 그럴 때 지연 초기화를 사용한다. 

<br>

#### 📌 lateinit을 사용한 지연 초기화

기본 자료형들은 생성자에서 반드시 초기화되어야 하지만 의존성이 있는 초기화나 유닛 테스트를 위한 코드를 작성하면서 설정에 의한 초기화를 할 때는 매번 초기화하기 불편하다. 예를 들어 Car 클래스의 초기화 부분이 Engine 클래스와 의존성을 가질 때 Engine 객체가 생성되지 않으면 완전하게 초기화 할 수 없다. 이처럼 **특정 객체의 의존성이 있는 경우에는 지연 초기화를 해야 한다.** 

또 해당 자료형의 프로퍼티를 즉시 사용하지 않는데도 미리 생성해서 초기화한다면 메모리가 사용되어 낭비될 수 있다. 모듈별로 소스 코드를 테스트하는 유닛 테스트를 할 때는 임시적으로 객체를 생성시켜야 하는 경우가 많다. 이 때도 지연 초기화를 사용해야 한다. 

<br>

##### 프로퍼티 지연 초기화하기

클래스를 선언할 때 프로퍼티 선언은 NULL을 허용하지 않는다. 하지만 지연 초기화를 위한 **lateinit** 키워드를 사용하면 프로퍼티에 값이 바로 할당되지 않아도 컴파일러에서 허용하게 된다. 단 실행할 때까지 값이 비어 있는 상태라면 오류를 유발할 수 있으니 주의해야 한다. 

지금까지 배운 프로퍼티 초기화 하는 방법

+ 주 생성자에서 초기화
+ init 블록 초기화
+ 부 생성자에서 초기화
+ 매개변수의 기본값 초기화
+ 클래스 내부에서 선언과 동시에 기본값 초기화

<br>

##### lateinit의 제한

+ var로 선언된 프로퍼티만 가능하다
+ 프로퍼티에 대한 게터와 세터를 사용할 수 없다. 

<br>

`lateinit 예제`

```kotlin
class Person {
    lateinit var name: String // 지연 초기화를 위한 선언
    
    fun test( ) {
        if(!::name.isInitialized){ // 프로퍼티의 초기화 여부 판단
            println("not initialized")
        } else{
            println("initialized")
        }
    }
}
```

```kotlin
fun main(){
    val kildong = Person()
    kildong.test()
    kildong.name = "Kildong" // 이 시점에서 초기화 됨
    kildong.test()
}
```

<br><br>

#### 📌 😨 lazy를 사용한 지연 초기화

lateinit을 사용할 때는 val은 허용하지 않고 var만 허용했다. 하지만 var로 선언하면 객체나 프로퍼티의 경우 언제든 값이 변경될 수 있는 단점이 있다. **읽기 전용의 val로 선언한 객체나 프로퍼티를 나중에 초기화하려면 lazy를 적용하면 된다.**

<br>

##### lazy의 특징

+ 호출 시점에 by lazy {...} 정의에 의해 블록 부분의 초기화를 진행한다.
+ 불변의 변수 선언인 val에서만 사용 가능하다(읽기 전용)
+ val이므로 값을 다시 변경할 수 없다.

<br>

##### 프로퍼티 지연 초기화하기

**lazy**는 ***람다식으로 구성되어 lazy 인스턴스 반환값을 가지는 함수***이다. **lazy**를 사용하는 프로퍼티를 선언해보자.

```kotlin
class LazyTest {
    init {
        println("init block") // 2
    }
    
    val subject by lazy {
        println("lazy initialized") // 6 
        "Kotlin Programming" // 7 - lazy 반환값
    }
    
    fun flow(){
        println("not initialized") // 4
        println("subject one: $subject") // 5 - 최초 초기화 시점 , 8
        println("subject two: $subject") // 9
    }
}

fun main() {
    val test = LazyTest() // 1
    test.flow() // 3
}
```

프로퍼티에 최초로 접근한 시점에 해당 프로퍼티가 초기화된다. 이후에는 9번처럼 이미 초기화된 내용을 재사용한다. 그리고 초기화된 subject는 val로 선언되었으므로 다시 값을 설정할 수 없다. 

<br>

##### 객체 지연 초기화하기

```kotlin
class Person(val name: String, val age: Int)

fun main() {
    val isPersonInstantiated: Boolean = false // 초기화 확인 용도
    
    val person : Person by lazy { // 1번 - lazy를 사용한 person 객체의 지연 초기화
        isPersonInstantiated = true
        Person("Kim", 23) // 2번 - 이 부분이 Lazy 객체로 반환됨
    }
    
    val personDelegate = lazy {Person("Hong", 40)} // 3번 - 위임 변수를 사용한 초기화
    
    // 객체 접근
    println("person.name = ${person.name}") // 이 시점에서 초기화
    println("personDelegate.value.name = ${personDelegate.value.name}") // 이 시점에서 초기화   
}
```

+ 1번의 **by lazy**를 사용해 person 객체를 지연 초기화하고 있고 3번의 **lazy**만 사용해 위임 변수를 받아서 지연 초기화에 사용하고 있다. 2가지 방법 모두 지연 초기화를 lazy 블록 구문에서 수행한다. lazy 블록의 마지막 표현식이 초기화된 후 Lazy 객체로 반환되므로 2번과 같이 객체 생성자를 반환한다. 

  이는 바로 객체의 프로퍼티나 메서드가 접근되는 시점에서 초기화된다. 즉 객체에 lazy가 선언된 시점에서 객체가 생성되는 것이 아니라, 코드의 접근 시점(ex) `person.name`에 초기화된다. 

+ ***by lazy**와 lazy 할당의 차이점은 **by lazy는 객체의 위임**을 나타내며 **lazy는 변수에 위임된 Lazy 객체 자체**를 나타내므로 이 변수의 value를 한 단계 더 거쳐 객체의 멤버인 value.name과 같은 형태로 접근해야 한다는 것이다.* 

  ???

<br>

##### lazy 모드 확인하기

앞에서 lazy는 람다식으로 만들어져 있다고 설명했다. 

lazy()는 매개변수 없는 람다식을 받을 수 있으며 `Lazy<T>`를 반환한다. 이는 제네릭이다. T를 사용해 어던 자료형이라도 처리할 수 잇다. 

<br><br>

#### 📌 by를 이용한 위임

실제 세계에서 **위임**이란 어떤 특정 일을 대신하는 중간자 역할을 말한다. 예를 들어 상속 재산을 상속 받으려면 합의서에 모든 상속자가 서명해야 하지만 특정 상속자가 다른 상속자를 대신하여 서명할 수 있게 위임장을 쓰면 대신 서명할 수 있다.

코틀린에서도 특정 클래스를 확장하거나 이용할 수 있도록 by를 통한 위임이 가능하다. **by를 사용**하면 **하나의 클래스가 다른 클래스에 위임하도록 선언하여 위임된 클래스가 가지는 멤버를 *참조 없이 호출할 수 있게 된다*.** 

프로퍼티 위임이란 ? 

프로퍼티의 게터와 세터를 특정 객체에게 위임하고 그 객체가 값을 읽거나 쓸 때 수행하도록 만드는 것이다. 

<br><br>

##### 클래스의 위임

```kotlin
interface Animal {
    fun eat() { ...}
    ...
}

class Cat : Animal { }
val cat = Cat( )
class Robot : Animal by cat // Animal에 정의된 Cat의 모든 멤버를 Robot에 위임
```

+ 만약 Animal Interface를 구현하고 있는 Cat 클래스가 있다면 Animal에서 정의하고 있는 Cat의 모든 멤버를 Robot 클래스로 위임할 수 있다. 즉, **Robot은 Cat이 가지는 모든 Animal의 메소드를 가지는데 이를 클래스 위임이라고 한다**.
+ 사실 Cat은 Animal 자료형의 private 멤버로 Robot 클래스 안에 저장되며 Cat에서 구현된 모든 Animal의 메서드는 정적 메서드로 생성된다. 따라서 우리가 Robot 클래스를 사용할 때 Animal을 명시적으로 참조하지 않고도 `eat()`을 바로 호출하는 것이 가능하다.

- [ ] 왜 위임을 사용할까?

  기본적으로 코틀린이 가지고 있는 표준 라이브러리는 open으로 정의되지 않은 클래스를 사용하고 있는데, 다시 말하면 모두 final 형태의 클래스이므로 상속이나 직접 클래스의 기능 확장이 어렵게 된다. 오히려 이렇게 어렵게 만들어 둠으로써 표준 라이브러리의 무분별한 상속에 따른 복잡한 문제를 방지할 수 있다. 따라서 필요한 경우에만 위임을 통해 상속과 비슷하게 해당 클래스의 모든 기능을 사용하면서 동시에 기능을 추가 확장 구현할 수 있는 것이다. 

<br><br>

##### 클래스의 위임 사용하기 예제

<br>



<br>

##### 프로퍼티의 위임과 by lazy

앞에서 살펴본 프로퍼티의 lazy도 by lazy { ... }처럼 by가 사용되어 위임된 프로퍼티가 사용되었다는 것을 알 수 있다. lazy는 사실 람다식이므로 사용된 프로퍼티는 람다식에 전달되어(위임되어) 사용된다. 따라서 앞에서 분석한 lazy의 동작을 설명하면 다음과 같다.

1. lazy 람다식은 람다식을 전달받아 저장한 Lazy<T> 인스턴스를 반환한다. 
2. 최초 프로퍼티의 게터 실행은 lazy에 넘겨진 람다식을 실행하고 결과를 기록한다.
3. 이후 프로퍼티의 게터 실행은 이미 초기화되어 기록된 값을 반환한다.

by lazy에 의한 지연 초기화는 **스레드에 좀 더 안정적으로 프로퍼티를 사용할 수 있다**. 예를 들어 프로그램 시작 시 큰 객체가 있다면 초기화할 때 모든 내용을 시작 시간에 할당해야 하므로 느려질 수 밖에 없다. 이것을 필요에 따라 해당 객체를 접근하는 시점에서 초기화하면 시작할 대마다 프로퍼티를 생성하느라 소비되는 시간을 줄일 수 있다. 

<br>

##### observable() 함수와 vetoable() 함수의 위임

코틀린의 표준 위임 구현 중 하나인 observable() 함수와 vetoable() 함수

<br>

>  import 해줘야 함 
>
> `import kotlin.properties.Delegates`

<br>

프로퍼티를 위임하는 object인 Delegates로부터 사용할 수 있는 위임자인 obsevable() 함수는 **프로퍼티를 감시하고 있다가 특정 코드의 로직에서 변경이 일어날 때 호출되어 처리된다.** 특정 변경 이벤트에 따라 호출되므로 **콜백**이라고도 부른다.

vetoable() 함수는 observable() 함수와 비슷하지만 **반환값에 따라 프로퍼티 변경을 허용하거나 취소할 수 있다는 점이 다르다.** 반환값이 참이면 변경을 허용, 거짓이면 허용하지 않는다. 

이 두 위임을 생성하기 위해서는 배개변수에 기본값을 지정해야 한다. 

<br><br>

-----

### ✅ 인터페이스와 추상클래스 자세히

우리는 관악기, 타악기, 현악기를 프로그램 상에 구현하고 싶다. 세 악기 종류 모두 play() 라는 기능이 있기 때문에, 우리는 Instrument 라는 클래스를 만들고 play() 함수를 추가하여, 세 악기 종류를 뜻하는 Wind, Percussion, Stringed 클래스가 Instrument를 상속받도록 하기로 했다. 

이를 클래스로 구현하려면 open class로 Instrument를 구현하고 이 안에 open fun play() { ~ }를 구현하고 각 Wind, Percussion, Stringed 클래스가 Instrument를 상속받도록 하고 각 클래스 안에 play() 함수를 오버라이드 하면 된다.

Instrument 클래스 내 play() 함수의 구현 부분이 없이 이런 기능을 사용할 수 없을까 ??

=> 인터페이스와 추상 클래스를 이용해 사용 가능

<br>

#### 인터페이스

+ **인터페이스는 구현 부분이 없게 만들 수 있는 클래스**이다.  **인터페이스의 객체는 생성할 수 없다**. 그래서 다른 클래스가 인터페이스를 상속받고(구현하고), 그 클래스에서 인터페이스의 메서드들의 구현 부분을 채운 후 그 클래스의 객체를 통해 사용할 수 있다. 

+ 코틀린 인터페이스는 함수 뿐만 아니라 val/var 프로퍼티도 포함할 수 있는데 이 프로퍼티는 인터페이스에서 초기화해줄 수 없다. 
+ 인터페이스는 클래스를 통하여 '구현된다'고 표현된다. 인터페이스를 구현한 클래스는 인터페이스의 하위 클래스가 된다. 클래스를 상속받는 방법과 비슷하게 콜론(`:`)뒤에 인터페이스 이름을 쓰면 된다. 다른 점은 인터페이스 이름 뒤에는 괄호가 오지 않는 다는 것이다.(그런데 자식 클래스에 부생성자만 존재할 때도 클래스 이름 뒤에 괄호가 없기 때문에 이것만으로 구분하기는 어렵다)
+ 또한 인터페이스를 구현하는 클래스는 인터페이스의 **디폴트 구현이 없는 모든 함수와 프로퍼티**를 구현해야 한다. **인터페이스의 함수와 프로퍼티의 게터/세터 메서드는 디폴트 구현을 가질 수 있는데** 이 경우 인터페이스를 구현한 클래스에서 해당 함수나 프로퍼티의 게터/세터 메서드를 구현하지 않으면 디폴트 구현이 사용된다

<br>

인터페이스의 특징

+ 인터페이스의 접근 제어자는 **public, open**이다. 클래스 기본 접근제어자인 public, final과 다르며, 접근 제어자를 변경할 수 없다. 인터페이스의 메서드, 프로퍼티에도 똑같이 적용된다. 
+ 인터페이스에서 메서드를 구현하면 그 메서드 구현이 default 구현으로 적용된다. 
+ 인터페이스의 프로퍼티 역시 default getter 함수와 setter 함수를 구현할 수 있다. 그러나 인터페이스는 뒷받침하는 필드를 가질 수 없기 때문에 field 키워드 사용이 불가하고 프로퍼티 초기화도 불가능하다. 
+ 인터페이스도 인터페이스를 상속받을 수 있다. 

<br><br>

#### 추상클래스

추상 클래스는 인터페이스와 클래스의 중간이라고 볼 수 있다. 즉 일반 클래스의 특징도 가질 수 있고, 인터페이스의 특징도 가질 수 있다. 

+ 인터페이스의 특징으로는 추상 메소드와 추상 프로퍼티도 가질 수 있고, 

+ 클래스의 특징으로는 일반 클래스와 다르지 않다. 

<br>

참고 : [블로그](https://medium.com/depayse/kotlin-%ED%81%B4%EB%9E%98%EC%8A%A4-6-%EC%9D%B8%ED%84%B0%ED%8E%98%EC%9D%B4%EC%8A%A4-interface-%EC%B6%94%EC%83%81-%ED%81%B4%EB%9E%98%EC%8A%A4-abstract-class-ed57aeecb9ce)

-----

<br><br><br>

-----

### 🚩 6 - 3 정적 변수와 컴패니언 객체

보통 우리가 사용할 수 있는 변수는 사용 범위에 따라 **지역 변수**와 **전역 변수**로 나뉜다. 이런 변수들은 초기화를 통해서 사용되며 변수가 영향을 미치는 영역이 있다. 

> **코틀린은 자바와 같이 정적 타입(statically typed) 지정 언어**이다. 정적 타입 지정 언어라는 것은 컴파일 시점에 구성 요소의 타입을 알 수 있고, 컴파일러가 타입을 검증해준다는 것이다. 
>
> 대표적으로 파이썬(python)언어는 동적 타입 지정 언어이다. 동적 타입 지정 언어는 타입과 관계 없이 모든 값을 변수에 넣을 수 있고, 이로 인해 코드가 더 간결해지고 데이터 구조 자체를 유연하게 사용할 수 있다. 하지만 파이썬 언어를 다뤄본 사람이라면 알 수 있듯이, 컴파일시 타입에 대한 검증이 없기 때문에 실행 시점(run time)에 에러가 발생할 수 있다.
>
> 한편 **코틀린은 정적 타입 지정언어 임에도 불구하고 자바와는 달리 모든 변수의 타입을 프로그래머가 직접 명시해주지 않아도 된다.** 컴파일러가 문맥을 고려하여 변수 타입을 결정한다. 그리고 이러한 기능을 타입 추론(type inference)이라고 부른다.
>
> 출처: [Tigercow.Door](https://doorbw.tistory.com/241)

클래스는 인스턴스를 생성해 메모리에 동적으로 초기화해서 사용한다. 마찬가지로 클래스에서 사용하는 프로퍼티나 메서드도 코드의 블록 영역에 따라 사용하는 범위가 결정된다. **그렇다면 모든 변수나 클래스의 객체는 꼭 동적으로 객체를 생성해서 사용해야만 할까 ?**

=> 동적인 초기화 없이 사용할 수 있는 변수 개념이 있다. 바로 정적 변수나 컴패니언 객체를 사용하는 것이다. 이것은 동적인 메모리에 할당 해제되는 것이 아닌 **프로그램을 실행할 때 고정적으로 가지는 메모리로 객체 생성 없이 사용할 수 있다.** 

<br><br>

#### 📌 정적 변수와 컴패니언 객체

객체 생성 없이 정적 변수나 메서드를 사용 => 따로 인스턴스화할 필요 없이 사용 가능

독립적으로 값을 가지고 있기 때문에 **어떠한 객체라도 동일한 참조값**을 가지고 있어 해당 클래스의 상태에 상관없이 접근할 수 있다. 따라서 모든 객체에 의해 공유되는 효과를 가진다.

<br>

##### 컴패니언 객체 사용하기

코틀린에서는 **정적 변수를 사용할 때** static 키워드가 없는 대신 **컴패니언 객체를 제공**한다. 

***컴패니언 객체는 실제 객체의 싱글톤으로 정의된다***. 싱글톤이란 전역 변수를 사용하지 않고 객체를 하나만 생성하도록 하며, 생성된 객체를 어디에서든지 참조할 수 있도록 하는 디자인 패턴의 하나이다. 

=> 이러한 패턴을 사용하는 이유 ? **객체가 서로 동일한 정보를 가질 때 하나의 메모리만 유지해 자원의 낭비를 줄이기 위해**

<br><br>

##### 코틀린에서 자바의 static 멤버 사용하기

코틀린에서는 컴패니언 객체를 사용하면 되지만, 자바와 연동해서 사용하려면 정적 변수나 메서드를 접근해야 하는 경우가 있다. 

코틀린 코드에서 사용된 **const**는 컴파일 시간의 상수이다. 컴파일 시간의 상수란 **val**과 다르게 컴파일 시간에 이미 값이 할당되는 것으로 **자바에서 접근하기 위해 필요**하다. **val**은 실행시간에 할당된다. 



<br>

##### 코틀린과 자바에서 서로의 정적 객체에 접근하기

<br>

##### 최상위 함수 사용하기

최상위 함수(패키지 레벨 함수) - 클래스 없이 만든 함수  = 즉, 전역 함수?

```kotlin
fun packageLevelFunc( ){
    println("Package-Level Function")
}

fun main() {
    packageLevelFunc()
}
```

+ 이 코드는 클래스나 객체가 없으나 최상위 함수인 packageLevelFunc() 함수가 main() 블록에서 잘 실행된다. 이를 역컴파일 해보면 최상위 함수는 JVM에서 실행되기 위해 **static**으로 선언되어 있음을 알 수 있다. 

<br>

##### object와 싱글톤

내용이 조금 변경된 클래스를 만들고 싶은데 (상위 클래스에서 하위 클래스를 새로 선언해 변경된 내용을 기술할 수 있지만) 새로 하위 클래스를 선언하지 않고 조금 변경한 객체를 생성하고 싶다면

=> 자바에서는 익명 내부 클래스를 사용하면 되고, 코틀린은 **object 표현식**이나 **object 선언**으로 좀 더 쉽게 처리할 수 있다.  

<br>

##### object 선언

```kotlin
// 1️⃣ object 키워드를 이용한 방식
object OCustomer {
    var name = "Kildong"
    fun greeting( ) = println("Hello World!")
    val HOBBY = Hobby("Basketball")
    
    init{
        println("Init!")
    }
}

// 2️⃣ 컴패니언 객체를 사용한 방식
class CCustomer{
    companion object{
        const val HELLO = "hello" // 상수 표현
        var name = "Joosol"
        @JvmField val HOBBY = Hobby("Football")
        @JvmStatic fun greeting() = println("Hello World!")
    }
    
}

class Hobby(val name: String)

fun main() {
    OCustomer.greeting( ) // 객체의 접근 시점 => 객체가 생성
    OCustomer.name = "Dooly"
    println("name = ${OCustomer.name}")
    println(OCustomer.HOBBY.name)
    
    CCustomer.greeting()
    println("name = ${CCustomer.name}, HELLO = ${CCustomer.HELLO}")
    println(CCustomer.HOBBY.name)
}
```

+ object로 선언된 OCustomer는 멤버 프로퍼티와 메서드를 객체 생성 없이 이름의 점(`.`) 표기법으로 바로 사용할 수 있다. 이것 역시 단일 인스턴스를 생성해 처리하기 때문에 **싱글톤 패턴**에 이용된다. 
+ **object 선언 방식을 사용하면 접근 시점에 객체가 생성**된다. 그렇기 때문에 생성자 호출을 하지 않으므로 object 선언에는 주 생성자와 부 생성자를 사용할 수 없다. 하지만 초기화 블록인 **init**은 들어갈 수 있는데 최초 접근에서 실행된다. object 선언에서도 클래스나 인터페이스를 상속할 수 있다.

<br>

##### object 표현식

object 표현식은 object 선언과 달리 이름이 없으며 싱글톤이 아니다. 따라서 **object 표현식이 사용될 때마다 새로운 인스턴스가 생성**된다. 결과적으로 **이름이 없는 익명 내부 클래스로 불리는 형태를 object 표현식으로 만들 수 있는 것**이다.

object 표현식을 이용해 **하위 클래스를 만들지 않고도 클래스의 특정 메서드를 오버라이딩할 수 있다.** 

```kotlin
open class Superman( ){
    fun work( ) = println("Taking photos")
    fun talk( ) = println("Taking with people.")
    open fun fly() = println("Flying in the air") 
}

fun main(){
    val pretendedMan = object: Superman(){ // 1️⃣ object 표현식으로 fly() 구현의 재정의
        override fun fly() = println("I'm not a real superman. I can't fly")
    }
    pretendedMan.work()
    pretendedMan.talk()
    pretendedMan.fly()
}
```

+ 1️⃣번에 익명 객체가 object 표현식으로 만들어졌다. 여기서 익명 객체는 Superman 클래스를 상속해 fly() 메서드를 오버라이딩 하고 있다. 결국 하위 클래스를 만들지 않고도 Superman 클래스의 fly() 메서드를 오버라이딩해 변경했다.  

<br>

##### object 표현식 활용사례

```kotlin
window.addMouseListener(object: MouseAdapter() {
    override fun mouseClicked(e: MouseEvent){
        ...
    }
    
    override fun mouseEntered(e: MouseEvent){
        ...
    }
})
```

- [ ] addMouseListener()의 매개변수로 object 표현식이 사용되었는데 이때 2개의 메서드가 MouseAdapter()를 통해서 오버라이딩하고 클래스의 이름 없이 사용했다.

  => addMouseListener의 매개변수가 MouseAdapter()라는 클래스의 인스턴스인 object이고, 이 object는 MouseAdapter()라는 클래스의 mouseClicked() method와 mouseEntered() method를 override 한 상황??

<br><br><br>

-----

### 질문

+ `::name` 이렇게 프로퍼티 접근할 때 콜론2개(`::`) 사용해야 함?
+ static





by lazy는 지연초기화 할 때, val을 나중에 초기화 할때



개발자가 얘를 초기화를 안시켜주고, 변수를 사용하게 될 때 그 때는 중괄호 
