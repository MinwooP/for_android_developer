# Do It! Kotlin Programming Ch2

<br>

## 🚩 2 - 1 코틀린 패키지

코틀린에서 **프로젝트**는 **모듈, 패키지, 파일**로 구성되어 있습니다. 

+ 코틀린 프로젝트 - 여행
+ 모듈 - 목적지
+ 패키지 - 여행용 가방
+ 파일 - 가방 속에 넣은 짐

<br>

<br>

##### 코틀린 프로젝트, 모듈, 패키지, 파일의 관계 이해하기 

+ 파일(클래스) => 패키지 => 모듈 => 코틀린 프로젝트

<img src = "https://user-images.githubusercontent.com/31370590/137160006-d7ca78b1-1b30-415a-bb91-400a5f6cffc6.PNG">

<br>

+ HelloKotlin 프로젝트
  + HelloKotlin 모듈
    + com.example.edu 패키지
    + default 패키지
  + OtherKotlin 모듈

<br>

+ 프로젝트와 모듈의 관계

  보통 대규모 **프로젝트를 진행할 때**는 **기능을 모듈로 분리하여 관리**합니다. 즉, HelloKotlin 프로그램은 2개의 기능을 가지고 있는 것이다.

+ 코틀린 파일은 .kt 확장자를 가지며 파일의 맨 위에는 이 파일이 어떤 패키지에 포함된 것인지 코틀린 컴파일러가 알 수 있도록 패키지 이름을 선언해야 한다. 패키지 이름을 선언하지 않으면 그 파일은 자동으로 default 패키지에 포함된다.

<br>

##### 패키지를 만들어야 하는 이유

2명의 프로그래머가 프로젝트를 진행하다 우연히 같은 이름의 파일(클래스)를 만들었다면 오류가 발생하지만, **패키지가 다르면 오류가 발생하지 않는다.** 

<br>

##### 패키지 이름 정하기

패키지 이름은 파일 맨 위에 적으면 되고, 여러 단계의 분류가 필요하면 점(.)을 붙여 이름을 지으면 된다. 이름을 지을 때 다른 이름과 중복되지 않도록 **웹사이트 주소 이름**을 짓는 방식을 많이 사용한다. 

<br>

#### 기본 패키지 활용하기

기본 패키지란 코를린으로 프로그램을 만들 때 자주 사용하는 클래스와 함수 등을 미리 만들어 노은 것이다. 이들은 **import** 키워드로 패키지를 선언하지 않아도 바로 사용가능하다.

ex) `kotlin.*` package

<br>

<br>

<br>

## 🚩 2 - 2 변수와 자료형

### 변수

- val

  - **val**ue
  - 선언하면 최초로 지정한 변수의 값으로 초기화 후 읽기만 가능
  - java의 final과 동일

- var

  - **var**iable
  - 최초로 지정한 변수의 초깃값이 있더라도 값을 변경 가능

  => val로 변수를 선언해놓고 변경해야 할 때 var로 바꾸는 방법을 권장한다.
  
  > ```kotlin
  > val a = 3 //이렇게 선언해놓고 
  > // 코딩하다가 a를 사용할 일 있으면
  > var a = 3 // 이렇게 직접 var로 바꾸라는 뜻?
  > ```
  >
  > 
  
  

<br>

- 변수 선언

  - 자료형을 지정하지 않고 선언하면 변수에 **할당된 값을 통해 추론하여 자료형을 지정**

    => `val username = "Minwoo"`

  - 값을 할당하지 않고 변수를 선언하려면 반드시 자료형을 지정해야 한다.

    => `val username : String`

  - 변수 이름 짓는 주의 사항

    - 변수 이름은 숫자로 시작 불가
    - 변수 이름으로 while과 if 같이 코틀린에서 사용되는 키워드 불가
    - 여러 단어를 사용하여 변수 이름을 지으면 카멜 표기법 사용 권장

<br>

<br>

### 자료형

##### 코틀린의 자료형은 참조형 자료형을 사용한다.

+ **기본형**(Primitive Data Type)은 가공되지 않은 순수한 자료형을 말하며 프로그래밍 언어에 내장되어 있다.

+ **참조형**(Reference Type)은 **객체를 생성하고 동적 메모리 영역에 데이터를 둔 다음 이것을 참조하**는 자료형을 말한다.

자바에서는 int, long, float, double 등 기본형과  String, Date와 같은 참조형을 모두 사용하지만 코틀린에서는 참조형만 사용한다. **참조형으로 선언한 변수는 성능최적화를 위해 코틀린 컴파일러에서 다시 기본형으로 대체된다**. 따라서 코틀린에서는 참조형을 기본형으로 고려하는 등의 최적화를 신경쓰지 않아도 된다.

<br>

<br>

##### 기본형과 참조형의 동작 원리

자바에서 사용된 기본형과 참조형으로 선언한 변수

```java
int a = 77; // 기본형
Person person = new Person(); // 참조형으로 person 객체를 위해 참조 주소(A12)를 가진다.
```

+ 기본형으로 선언한 변수 a는 주로 임시 메모리인 **스택**에 저장되며 값이 저장된 메모리의 크기도 고정되어 있다.
+ 참조형은 스택에 값이 아닌 참조 주소가 있다. 그러면 참조형의 실제 객체는 동적 메모리인 **힙**에 저장된다. 
+ 기본형이 참조형보다 코드 수행시간이 빠르고 코틀린은 컴파일 과정을 거치면서 참조형을 기본형으로 바꿔주며 자동으로 최적화를 수행해준다. 따라서 코틀린에서 기본형을 사용할지 참조형을 사용할지 고민x => **참조형만 사용하면 됨**

<img src = "https://user-images.githubusercontent.com/31370590/137169464-a4eb9a57-c08c-44b0-9fdf-75682b0e0cd7.PNG">

<br>

<br>

#### 정수 자료형

+ **Long**  - 8B
+ **Int** - 4B
+ **Short** - 2B
+ **Byte** - 1B

<br>

+ 정수를 표현할 때 숫자를 그냥 사용하면 10진수를 나타내지만 접미사나 접두사를 사용하면 2진수나 16진수 표현가능

  ```kotlin
  val num1 = 123
  val num2 = 123L // 접미사 L을 통해 Long형으로 추론
  val num3 = 0x0F // 접두사 0x를 사용해 16진법으로 표기된 Int형으로 추론
  val num4 = 0b00001011 // 접두사 0b를 사용해 2진 표기가 사용된 Int형으로 추론
  ```

<br>

<br>

#### 실수 자료형

+ **Double** - 8B
+ **Float** - 4B

+ 데이터 크기에 맞게 자료형을 지정하려면 자료형의 최솟값과 최댓값을 파악해야 한다.

<br>

<br>

#### 논리 자료형

+ **Boolean** - 1bit => true or false

+ 논리 자료형은 흔히 **검사 용도의 변수**를 만들 때 사용하낟.

  ```kotlin
  val isOpen = true
  val isUpLoaded : Booleean

<br>

<br>

#### 문자 자료형

+ **Char** - 2B

+ 컴퓨터는 문자 자료형 값을 저장할 때 문자세트(**아스키코드 표**, 유니코드 표)를 참고하여 번호로 저장한다. 하지만 **선언할 때는 문자 값으로 선언해야 한다.** 선언한 다음에는 문자 자료형에 숫자를 더하는 방식으로 다른 문자를 표현할 수 있다.

  ```kotlin
  val ch = 'A'
  println(ch+1) // B
  
  val chNum: Char = 65 // 오류! 숫자를 사용하여 선언하는 것은 금지

<br>

<br>

#### 문자열 자료형

+ **String** 

+ 문자 자료형 Char은 char과 같은 기본형으로 처리되지만, 문자열 자료형은 **기본형에 속하지 않은 배열 형태로 되어 있는 특수한 자료형**이다.

<br>

+ 문자열 자료형 선언과 저장 방식

  ```kotlin
  fun main(){
      var str1: String = "Hello"
      var str2 = "World"
      var str3 = "Hello"
  }
  // str1 == str3
  ```

  + str1, str3에는 같은 문자열이 저장되어 있는데 이런 경우, **"Hello"**를 스택에 2번 저장하는 것이 아니라, 힙 영역의 **String pool**이라는 공간에 문자열인 "Hello"를 저장해두고 이 값을 str1, str3이 참조하도록 만든다. 

    => String Pool을 이용해 필요한 경우 메모리를 재활용한다. 

    <img src = "https://user-images.githubusercontent.com/31370590/137173986-bf0446f1-e9da-4bab-aecc-06356f6076c5.PNG">

<br><br>

+ 변수의 값이나 표현식을 문자열 안에 넣어 출력하려면 `$` 기호와 중괄호 `{}`를 사용하면 된다.

  ```kotlin
  var a = 1
  val s1 = "a is $a" // 문자열에 변수 사용
  ```

  ```kotlin
  val a = 1
  val str2 = "a = ${a + 2}" // 문자열에 표현식 사용

<br><br>

+ 형식화된 다중 문자열 사용하기

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

## 🚩 2 - 3 자료형 검사하고 변환하기

+ 값이 할당되지 않은 변수를 사용하면 코틀린에서 오류가 발생한다. 

  => 코틀린은 변수에 아예 null을 허용하지 않아 **NullPointerException**을 방지할 수 있다.

  => 아예 null을 허용하지 않는 건 아니고, null을 할당하려면 자료형 뒤에 `?` 기호를 명시하면 된다.

<br>

##### null을 허용한 변수 사용하기

+ null을 허용하기 : 
  원래 코틀린에서는 변수에 null을 허용하지 않는데 꼭 null을 허용하는 변수를 사용하고 싶으면 자료형 뒤에 `?`기호를 명시하면 된다.

  ```kotlin
  val str1 : String? = "Hello kotlin"
  str1 = null // 널 가능
  ```

  하지만 이렇게, null을 허용한 변수를 사용하기 위해선 조건이 있다. 

  ```kotlin
  ㅇfun main(){
      var str1: String? = "Hello Kotlin"
      str1 = null
      println("str1: $str1 length: ${str1.length}") // 불가능
  }
  ```

  `str1` 변수가 null을 허용했기 때문에 이는 그냥 `str1.length` 이렇게 사용될 수 없다. 오류가 발생한다. null을 허용한 변수를 **검사**해줘야 한다. 이에 대한 방법은 `?.`, `!!.`, 조건문을 활용한 검사 등의 방법이 있다. 

<br>

1. 세이프 콜 `?.`\

   null이 할당되어 있을 가능성이 있는 변수를 검사하여 안전하게 호출하도록 도와주는 기법으로 세이프 콜을 추가하려면 호출할 변수 이름 뒤에 `?.`를 작성하면 된다. 

   ```kotlin
   var str1 : String? = "HelloKotlin"
   str1 = null
   str1?.length // null
   ```

   => 변수 str1을 검사한 다음 null이 아니면 str1의 멤버 변수인 length에 접근해 값을 읽도록 하는 것. str1은 null이니 length에 접근하지 않고 그대로 null을 출력한다. 

<br>

2. non-null 단정기호 `!!.`

   non-null 단정기호는 변수에 할당된 값이 null이 아님을 단정하므로 컴파일러가 **null 검사없이 무시**한다. 따라서 변수에 null이 할당되어 있어도 컴파일은 잘 진행된다. 하지만 실행 중에 **NPE**를 발생시킨다. 따라서, 사용자가 변수를 보고 무조건 null인 경우에만 `!!.`을 사용해줘야 한다. 만약 null이라면 이에 대한 문제는 사용자의 책임? \

   ```kotlin
   println("str1: $str1 length: ${str1!!.length}")
   ```

<br>

3. 조건문을 활용해 null을 활용한 변수 검사하기

   세이프 콜이나 non-null 단정 기호를 사용하는 방법 대신 조건문으로 null을 허용한 변수를 검사해도 된다. 즉, null을 허용한 변수의 null 상태 가능성을 검사하기만 하면 컴파일러는 오류를 발생시키지 않는다. 

   ```kotlin
   fun main(){
       var str1 = String? = "Hello Kotlin"
       str1 = null
       // 조건식을 통해 null 상태 검사
       val len = if(str1 != null) str1.length else -1
       println("str1: $str1 length: ${len}")
   }
   ```

   

<br>

##### 세이프콜 `?.`과 엘비스 연산자 `?:`를 활용해 null을 허용한 변수 더 안전하게 사용하기

+ `?:` : 변수가 null인지 아닌지 검사하여 null이 아니라면 왼쪽 식을 그대로 실행하고 null이라면 오른쪽 식을 실행한다. 

  ```kotlin
  ${Str1?.length ?: -1}
  ```

  이는 다음 코드와 동일하다

  ```kotlin
  if(str1 != null)
  	str1.length
  else
  	-1

<br>

<br>

#### 자료형 비교, 검사, 변환

##### 자료형 변환

+ 코틀린에서는 자료형이 서로 다른 변수를 비교하거나 연산할 수 없다. 

+ 자바에서는 자료형이 서로 다르면 자동 형 변환이 되지만, 코틀린에서는 자료형이 다른 변수에 재할당되면 자동 형 변환이 되지 않고, 자료형 불일치 오류가 발생한다.

  ```kotlin
  val a: Int = 1
  val b: Double = a // 자료형 불일치 오류 발생
  val c: Int = 1.1 // 자료형 불일치 오류 발생

+ 올바르게 변환하려면 **자료형 변환 메서드**를 이용해야 한다.

  ```kotlin
  val b: Double = a.toDouble() // a는 Int type이므로
  ```

+ 표현식에서 자료형이 서로 다른 값을 연산하면 자료형이 표현할 수 있는 범위가 큰 자료형으로 자동 형 변환하여 연산한다.

  ```kotlin
  val result = 1L + 3 // Long형 + Int형 -> Long형
  ```

<br>

<br>

##### 기본형과 참조형 자료형의 비교 원리

자료형의 비교

1. 단순히 값만 비교 => `==`

   참조에 상관없이 값이 동일하면 true, 다르면 false

2. 참조 주소까지 비교 => `===` 

   값에 상관없이 참조가 동일하면 true, 다르면 false

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

+ `Int`형으로 선언된 a는 기본형으로 변환되어 스택에 128이라는 값 자체를 저장하지만, `Int?`형으로 선언된 b는 참조형으로 저장되므로 b에는 저장된 128이 저장된 힙의 참조 주소가 저장되어 있습니다. 그래서 `a === b`는 false가 나온다. 

ex)

<img src = "https://user-images.githubusercontent.com/31370590/137180458-e5d5386b-9e63-4290-9128-42ee1a431751.PNG" width = "600" height = "900">

<br>

<br>

##### 스마트캐스트 사용하기

```ko
var test: Number = 12.2
```

+ Number형으로 정의된 변수에는 저장되는 값에 따라 정수형이나 실수형 등으로 자로형이 변환된다. 

<br>

##### 자료형 검사하기

```kotlin
if(num is Int)
```

+ `is` 키워드 사용

<br>

<br>

## 🚩 2 - 4  코틀린 연산자







#### 스터디 후

isBlankOrNull() / isBlank()

의 차이점

string의 null을 조사하는 방법들 조사



+ 앨비스 연산자



` a ?: b` a 객체가 null 이면 



+ binding을 var로 선언하는 이유? 

