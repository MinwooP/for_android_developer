# Do It! Kotlin Programming Ch4

### 🚩 4 - 1 조건문

### 📌 if문

```kotlin
} else if(score >= 80.0 && score <= 89.9) {
```

```kotlin
} else if(score in 80.0..90.0) {
```

위와 같이 포함여부확인을 위해 in 연산자와 2개의 점(..)으로 구성된 범위(range) 연산자를 사용할 수 있다.

} else if(score >= 80.0 &&)

<br>

#### 📌 when문

+ when문에서 **in 연산자**와 **범위 연산자** 사용

  ```kotlin
  when(x) {
      in 1..10 -> print("x는 1이상 10 이하입니다.")
      !in 1..10 -> print("x는 10이상 20이하의 범위에 포함되지 않습니다")
      else -> print("x는 어떤 범위에도 없습니다.")
  }
  ```

<br>

+ when 문에서 **is 키워드** 사용

  변수에 값을 할당할 때, when문을 이용해 간단히 표현할 수 있다. 

  ```kotlin
  val str = "안녕하세요."
  val result = when(str) {
      is String -> "문자열입니다."
      else -> false
  }
  ```

<br>

+ 인자가 없는 when문

  when문에 인자가 주어지지 않으면 **else if** 처럼 각각의 조건을 실행할 수 있다. 즉, 인자 있는 when문과는 다르게 조건식을 구성할 수 있음

  ```kotlin
  when{
      score >= 90.0 -> grade = 'A'
      score in 80.0..89.9 -> grade = 'B'
  }
  ```

<br>

+ **Any**를 인자로 사용해 다양한 자료형의 인자를 받기

  ```kotlin
  fun cases(obj: Any){
      when(obj) {
          1 -> println("Int: $obj")
          is Long -> print("Long: $obj")
          !is String -> println("Not a String")
          else -> println("Unknwon")
      }
  }
  ```

<br><br>

### 🚩 4 - 2 반복문

### for문, while문, do~while문

#### 📌 for문

+ for문은 변수를 선언하고 조건식에 따라 변수 값을 반복해서 증감하는 구문이다. for문, while문, do~while문의 반복문 중, **특정 변수를 계속 증가하거나 감소시킬 필요가 있을 때 for문을 쓰는게 좋겠다.** 

+ 자바의 for문에서는 초기화식. 조건식, 증감식을 세미콜론(;)으로 구분하지만 코틀린은 세미콜론을 사용할 수 없다. 

  ```java
  for(int i = 1; i<=5 ; i++) {...} // 자바에서는 이렇게 
  ```

+ 코틀린에서는 **in** 연산자와 함께 for문을 사용

  ```kotlin
  for(요소 변수 in 컬렉션 또는 범위) { 반복할 본문 }
  ```

+ for문은 내부적으로 반복을 처리하는 인터페이스인 **이터레이터**에 의해 배열이나 특정 값의 범위, 컬렉션으로 불리는 요소 등에서 사용할 수 있다. 

<br>

#### 📌 for문의 활용

+ **in**과 **범위 지정**을 활용한 반복

  ```kotlin
  for (x in 1..5){
      println(x)
  }
  ```

<br>

+ 하행 반복

  ```kotlin
  for(i in 5..1) print(i) // 아무것도 출력되지 않음
  ```

  이렇게 범위 연산자(`..`)을 이용해 숫자를 역순으로 작성하는 방법으로는 화면에 아무것도 출력되지 않는다. 이때는 범위 연산자 대신 **downTo** 키워드를 사용해야 한다.  

  ``` 
  for(i in 5 downTo 1)
  ```

<br>

+ 증감의 단위 지정

  ```kotlin
  for(i in 1..5 step 2) print(i)
  ```

<br><br>

### 🚩 4 - 3 흐름의 중단과 반환

조건문이나 반복문을 사용할 때 수행 중이던 코드를 바로 중단하거나 조건식으로 되돌아가도록 프로그램을 작성해야 하는 경우도 있다. 여기에서는 **return, break, continue**문을 사용해 프로그램 흐름을 제어하는 방법을 배울 것이다.

프로그램 실행 도중 오류가 발생하여 프로그램이 중단되는 예외를 처리하는 **try ~ catch**문도 있다.

<br>

#### 📌 return문 

##### return으로 값 반환하기

```kotlin
fun add(a: Int, b: Int) Int{
    return a + b
    print;n("이 코드는 실행되지 않습니다. ") // 여기에 도달하지 않음
}
```

보통 return문은 다음과 같이 값을 반환하는데 사용한다.  그리고 return 이후의 코드는 실행되지 않는다. **return이 사용되면 코드 흐름을 중단하고 함수의 역할을 끝내기 때문**이다. 

<br>

##### return으로 Unit 반환하기

**코틀린에서 Unit이란 반환하는 값이 아예 없다는 뜻이 아니라 Unit이라는 자료형 자체를 반환한다는 뜻**이다. 

1. Unit을 명시적으로 반환

   ```kotlin
   fun hello(name: String): Unit {
       println(name)
       
       return Unit // 1. Unit을 명시적을 반환
       return 		// 2. Unit 이름을 생략한 반환
       			// 3. return문 자체를 반환
   }
   ```

   <br>

   > 람다식에서는 return은 라벨 표기와 함께 사용해야 하고 break, continue는 아직 지원되지 않는다. 

<br>

#### 📌 😨 람다식에서 return 사용하기

인라인(inline)으로 선언되지 않은 람다식에서는 return을 그냥 사용할 수 없다. **return @label**과 같이 라벨(label) 표기와 함께 사용해야 한다. **라벨이란 코드에서 특정한 위치를 임의로 표시한 것**으로, **@기호와 이름을 붙여서 사용**한다. 인라인으로 선언된 함수에서 람다식을 매개변수로 사용하면 람다식에서 return을 사용할 수 있다. 

<br>

##### inline을 사용한 람다식의 반환 - 비지역 반환

```kotlin
fun main(){
    retFunc()
}

inline fun inlineLambda(a: Int, b: Int, out: (Int, Int) -> Unit) {
    out(a, b)
}

fun retFunc( ) {
    println("start of retFunc") // 1번
    inlineLambda(13, 3) {a, b -> // 2번
                        val result = a + b
                        if(result > 10) return // 10보다 크면 여기서 비지역 반환
                        println("result: $result")
                       }
    println("end of retFunc")
}
```

`inlineLambda()` 함수는 **람다식을 매개변수로 사용하는 인라인 함수**이다. `retFunc()` 함수가 호출되어 실행될 때 1번의 내용을 출력하고 2번으로 진입해 람다식을 인자로 사용하고 있다. 만일 a와 b인자의 합이 10을 넘는 경우 return한다. 이 코드에서는 13+3으로 10을 넘기에 **if문에서 return문이 호출되고 람다식 바깥의 `retFunc()` 함수까지 빠져나가게 된다**. 따라서 그 뒤의 코드는 실행되지 않는다. 이런 반환을 비지역 반환이라고 한다.  

<br>

##### 람다식에서 라벨과 함께 return 사용하기

그렇다면 **비지역 반환을 방지**하고 가장 가까운 함수인 **retFunc()** 함수 위치로 빠져 나가게 하려면 어떻게 할까 ?

이런 경우 람다식에서 **라벨을 정의해 return을 사용**해야 한다. 먼저 라벨을 지정하기 위해 정의할때는 @기호를 라벨 뒤에 붙여 **라벨이름@**와 같이 지정하고, 사용할 때는 앞부분에 **return@라벨이름**으로 지정한다. 

```kotlin
람다식_함수_이름 라벨_이름@ {
    ...
    return@라벨 이름
} 
```

<br>

```kotlin
fun main(){
    retFunc()
}

fun inlineLamda(a: Int, b: Int, out: (Int, Int) -> Unit) { // inline을 제거
    out(a, b)
}

fun retFunc( ) {
    println("start of retFunc") 
    inlineLambda(13, 3) lit@{a, b -> // 1번 람다식 블록의 시작 부분에 라벨을 지정
                        val result = a + b
                        if(result > 10) return@lit // 2번 라벨을 사용한 블록의 끝부분으로 반환
                        println("result: $result")
                       } // 3번 이 부분으로 빠져나감
    println("end of retFunc") // 4번 이 부분이 싫애
}
```

앞에서 작성한 `inlineLambda( )` 함수는 코드 앞에 **inline**을 삭제했으므로 이제 인라인 함수가 아니다. 따라서 **inline**을 지운 순간 **return**에 오류가 표시된다. 이 때 1번처럼 ***람다식 블록 앞에 라벨(lit@)을 정의***한다. 그리고 2번처럼 return에 @으로 시작하는 라벨(@lit)을 붙여 준다. 그러면 오류가 사라지고 result가 10보다 큰 경우 ***라벨이 붙은 블록의 끝부분으로 반환***할 수 있다. 

첫번째 예제에서는 **retFunc( )** 함수 자체가 남은 문장을 수행하지 않고 **return**을 사용한 지점에서 반환되었다. 그러나 이번에는 **retFunc( )**의 람다식 다음 줄인 4번 부분이 이상 없이 수행된다. 이번 예제에서는 retFunc()가 유지되고 있는 것이다.

<br>

##### 암묵적 라벨

람다식 표현식 블록에 **직접 라벨을 쓰는 것이 아닌 *람다식의 명칭을 그대로 라벨처럼 사용***할 수 있는데 이를 암묵적 라벨이라고 부른다. 

```kotlin
...
fun retFunc( ){
    println("start of retFunc")
    inlineLambda(13, 3) { a, b ->
                        val result = a + b
                        if(result > 10) return@inlineLambda
                        println("result: $result")
                        }
    println("end of retFunc")
}
```

결과는 라벨을 사용한 예제와 동일하게 `inlineLambda()`를 빠져나간다. 

<br>

##### 익명 함수를 사용한 반환

물론 람다식 대신에 익명 함수를 넣을 수도 있다. 이때는 라**벨을 사용하지 않고도 *가까운 익명 함수 자체가 반환***되므로 위와 동일한 결과를 가질 수 있다. 

```kotlin
fun inlineLamda(a: Int, b: Int, out: (Int, Int) -> Unit) { // inline을 제거
    out(a, b)
}
...
fun retFunc( ){
    println("start of retFunc")
    inlineLambda(13, 3, fun(a, b) {
                        val result = a + b
                        if(result > 10) return
                        println("result: $result")
                        }) // inlineLambda()의 긑부분
    println("end of retFunc")
}
```

익명 함수는 앞에서 배운 것처럼 **`fun (...) {...}`**의 형태로 이름 없이 특정 함수의 인자로 넣을 수 있다. 이때는 일반 함수처럼 작동하기 때문에 return도 일반 함수에서 반환되는 것과 같이 사용할 수 있는 것이다. 

람다식은 익명 함수에 포함된다. 

> 184p부터 다시 보고, 정리하기 ~

<br><br>

#### 📌 break문

break는 해당 키워드를 사용한 지점에서 반복문(for, while, do~while문) 루프를 빠져나온다.

continue는 이후 본문을 계속 진행하지 않고 다시 반복 조건을 살펴보게 된다. 

<br>

##### break과 continue에 라벨 함께 사용하기

이번에는 break과 함께 라벨을 사용해서 반복문이 중단되는 위치를 바꿔보자.

<img src = "https://user-images.githubusercontent.com/31370590/139680168-e9f9a61c-b284-4455-bdba-13c7deda87ee.PNG">

+ 라벨 없이 break를 사용하면 가장 가까운 반복문 블록을 중단시키고, `break@first`처럼 라벨을 사용하는 경우에는 `first@ for`로 빠져나가면서 for문이 종료된다. 

  => 이처럼 **2중 포문**을 빠져나갈 때 라벨을 이용해 사용하면 될 것 같다.

  > 어떤 식 블록 **앞에 라벨을 정의**하면 그 block을 빠져나간다. 

<br><br>

### 📌 예외 처리

프로그램 코드를 작성하다 보면 **해당 코드가 제대로 작동하지 못하고 중단되는 현상**이 발생할 수 있다. 그것을 예외(Exception)라고 한다. 대부분의 오류(Error)는 ***코드를 작성하는 도중***에 컴파일러가 잡아낼 수 있다. 

하지만 메모리 부족이나 파일이 손상되는 등의 **실행 도중의 잠재적인 오류까지 검사할 수 없기 때문**에 정상적으로 실행되다가 비정상적으로 프로그램이 종료될 수 있다. 

예외를 발생시키는 상황

+ 운영체제의 문제(잘못된 시스템 호출)
+ 입력값의 문제(존재하지 않는 파일 또는 숫자 입력란에 문자 입력 등)
+ 받아들일 수 없는 연산(0으로 나누기)
+ 메모리의 할당 실패 및 부족
+ 컴퓨터 기계 자체의 문제(전원 문제, 망가진 기억 장치 등)

=> 이러한 상황들은 코드를 작성하는 도중에는 예상할 수 없는, 즉 컴파일러가 잡아낼 수 없는 오류들로 이러하나 예외에 대비해야 하고 이것을 **예외 처리**라고 한다. 

잠재적으로 예외가 발생할 수 있는 코드를 **try ~ catch**문으로 감싸 놓는다. try 블록에서 예외가 발생하면 catch 블록에서 잡아서 그 예외를 처리한다.

<br>

```kotlin
try{
    예외 발생 가능성 있는 문장
} catch (e: 예외 처리 클래스 이름) {
    예외를 처리하기 위한 문장
} finally {
    반드시 실행되어야 하는 문장
}
```

보통 try 블록 안에 예외가 발생할 수 있는 코드를 작성하고 catch 블록의 인자에 예외를 처리하는 클래스를 작성한다. 만일 일치하는 catch 예외가 없어 처리할 수 없으면 프로그램이 중단된다. finally 블록은 try 블록의 예외 발생 여부에 상관없이 반드시 처리되어야 하는 문장을 작성한다.

예를 들어 try 블록에 '파일 열기' 작업을 작성했다면 finally 블록에는 '파일 닫기' 작업을 작성한다. 반드시 실행해야 할 작업이 없다면 finally 블록은 생략하고 try~catch 블록만으로 코드를 구성할 수 있다. 

<br>

##### 0으로 나누었을 때 예외를 발생하는 예제

```kotlin
fun main() {
    val a = 6
    val b = 0
    val c: Int
    
    try{
        c = a/b
    } catch (e: Exception){
        println("Exception is handled.")
    } finally {
        println("finally 블록은 반드시 실행됨")
    }
}
```

+ try 블록에서 예외가 발생하고 catch 블록의 구문이 출력된다. catch의 인자에 **Exception** 클래스는 일반적인 모든 예외를 가리킨다. 특정 예외를 지정하는 요소도 있다.

<br>

##### 특정 예외 처리

+ 산술 연산에 대한 예외 => **ArithmeticException** 

  ```kotlin
   } catch (e: ArithmeticException){
          println("Exception is handled. ${e.message}")
      } 
  ```

  `e.message` 처럼 예외를 가리키는 객체 e의 멤버 변수 또는 프로퍼티로 불리는 message를 읽으면 예외 원인을 간단히 출력해준다.

<br>

##### 스택의 추적

이번에는 **임시 메모리 영역인 스택을 추적할 수 있도록** 코드를 작성해보자.

```kotlin
...
} catch (e: Exception) {
    e.printStackTrace( )
}
...
```

e의 멤버 메서드인 printStackTrace( )를 사용하면 다음과 같이 ArithmeticException이 발생했음을 알 수 있고, 또한 오류가 발생한 코드의 줄을 확인할 수 있다. 

이렇게 오류의 원인이 되는 줄을 스택으로부터 추적할 수 있는 이유는 프로그램이 디버깅 정보를 유지하고 있기 때문이다.  단, finally 블록이 먼저 실행된 것처럼 보이고 있는데 이것은 실행할 때마다 조금씩 달라질 수 있다. println()의 경우 일반 출력인 **System.out**을 사용하고 오류용 출력은 **System.err**를 사용하기 때문이다. 

<br>

##### 예외 발생시키기

throw 키워드를 사용하여 의도적으로 예외를 발생시킬 수 있다. 특정 함수를 만들면서 필요한 경우 예외를 발생하도록 하려면 다음과 같은 형태로 지정한다. 

```kotlin
throw Exception(message: String)
```

<br>

**잔고가 1000 이하일 때 예외를 발생시키는 예제**

```kotlin
fun main(){
    var amount = 600
    
    try{
        amount -= 100
        checkAmount(amount)
    } catch (e: Exception){
        println(e.message)
    }
    println("amount: $amount")
}

fun checkAmount(amount: Int){
    if(amount< 100)
    throw Exception("잔고가 $amount로 1000이하입니다.")
}
```

```kotlin
// 실행결과
잔고가 500으로 1000이하입니다. 
amount : 500
```

<br>

##### 사용자 정의 예외

기본 Exception 클래스로부터 새롭게 사용자가 정의한 예외 클래스를 만들어낼 수 있다.

```kotlin
class <사용자 예외 클래스 이름> (message: String) : Exception(message)
```

<br>

**이름에 숫자가 포함되어있으면 예외 발생 시키는 예제**

```kotlin
clase InvalidNameException(message: String) : Exception(message)

fun main() {
    var name = "Killdong123" // 숫자가 포함된 이름
    
    try{
        validate(name)
    } catch(e : InvalidNameException){ // 숫자가 포함되었을 때 예외 처리
        println(e.message)
    } catch(e : Exception){ // 기타 예외 처리
        println(e.message)        
    }
}

fun validateName(name : String){
    if(name.matches(Regex(".*\\d+.*"))){
        throw InvalidNameException("Your name : $name : contains numerals.")
    }
}
```

