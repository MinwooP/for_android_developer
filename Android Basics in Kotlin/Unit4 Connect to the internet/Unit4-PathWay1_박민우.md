# <div align="center">🔥 Unit 4 : Connect to the internet</div>

## <div align="center">Pathway 1 : Coroutines</div>

-----

### <div align="center">목차</div>

- [Introduction to coroutines](#-Introduction-to-Coroutines)
  - [멀티스레딩 및 동시 실행](#멀티스레딩-및-동시-실행)
  - [Challenges with thread](#Challenges-with-thread)
  - [Kotlin의 코루틴](#Kotlin의-코루틴)
  - [코루틴 사용](#코루틴-사용)

------

## <div align="center">🎖 Introduction to Coroutines</div>

### 멀티스레딩 및 동시 실행

+ 기본 스레드가 아닌 스레드로 작업하면 앱의 사용자 **인터페이스 응답성을 유지**하면서 앱이 **이미지 다운로드와 같은 복잡한 작업을 백그라운드에서 실행**할 수 있습니다. 이를 동시 실행 코드 또는 간단히 동시 실행이라고 합니다. 

+ 동시 실행(concurrency)을 통해 여러 코드 단위를 순서에 맞지 않거나 병렬로 실행할 수 있어 리소스 사용의 효율성이 높아집니다. 운영체제는 시스템, 프로그래밍 언어, 동시 실행 단위의 특성을 사용하여 멀티태스킹을 관리할 수 있습니다.

<img src = "https://user-images.githubusercontent.com/31370590/129470913-fa4ea670-08af-41f2-b5b3-1b5f4f5f9478.PNG">

+ 동시 실행을 사용해야 하는 이유는 무엇인가요? 앱이 점점 복잡해짐에 따라 코드가 차단되지 않는 것이 중요합니다. 즉, 네트워크 요청과 같은 장기 실행 작업을 실행하더라도 앱에서 다른 작업의 실행이 중지되지 않습니다. **동시 실행을 올바르게 구현하지 않으면 앱이 사용자에게 응답하지 않는 것으로 보일 수 있습니다.**

<br>

+ Concurrent Programming 예시

  ```kotlin
  fun main() {
      val thread = Thread {
          println("${Thread.currentThread()} has run.")
      }
      thread.start()
  }
  ```

  함수가 `start()` 함수 호출에 도달하면 스레드가 실행됩니다.

  ```kotlin
  Thread[Thread-0,5,main] has run.
  ```

  `currentThread()`는 스레드의 이름, 우선순위, 스레드 그룹을 반환하는 문자열 표현으로 변환되는 `Thread` 인스턴스를 반환합니다. 위 출력 내용이 약간 다를 수 있습니다.

<br>

+ 여러 스레드 만들기 및 실행

  ```kotlin
  fun main() {
     val states = arrayOf("Starting", "Doing Task 1", "Doing Task 2", "Ending")
     repeat(3) {
         Thread {
             println("${Thread.currentThread()} has started")
             for (i in states) {
                 println("${Thread.currentThread()} - $i")
                 Thread.sleep(50)
             }
         }.start()
     }
  }
  ```

  이전 예의 정보 줄을 출력하는 스레드 3개를 만든다.

  플레이 그라운드의 출력

  ```kotlin
  Thread[Thread-2,5,main] has started Thread[Thread-2,5,main] - Starting Thread[Thread-0,5,main] - Doing Task 1 Thread[Thread-1,5,main] - Doing Task 1 Thread[Thread-2,5,main] - Doing Task 1 Thread[Thread-0,5,main] - Doing Task 2 Thread[Thread-1,5,main] - Doing Task 2 Thread[Thread-2,5,main] - Doing Task 2 Thread[Thread-0,5,main] - Ending Thread[Thread-2,5,main] - Ending Thread[Thread-1,5,main] - Ending Thread[Thread-0,5,main] has started
  Thread[Thread-0,5,main] - Starting
  Thread[Thread-1,5,main] has started
  Thread[Thread-1,5,main] - Starting
  ```

  AS(콘솔)의 출력

  ```kotlin
  Thread[Thread-0,5,main] has started
  Thread[Thread-1,5,main] has started
  Thread[Thread-2,5,main] has started
  Thread[Thread-1,5,main] - Starting
  Thread[Thread-0,5,main] - Starting
  Thread[Thread-2,5,main] - Starting
  Thread[Thread-1,5,main] - Doing Task 1
  Thread[Thread-0,5,main] - Doing Task 1
  Thread[Thread-2,5,main] - Doing Task 1
  Thread[Thread-0,5,main] - Doing Task 2
  Thread[Thread-1,5,main] - Doing Task 2
  Thread[Thread-2,5,main] - Doing Task 2
  Thread[Thread-0,5,main] - Ending
  Thread[Thread-2,5,main] - Ending
  Thread[Thread-1,5,main] - Ending
  ```

  코드를 여러 번 실행합니다. 출력이 다양하게 표시됩니다. 어떤 때는 스레드가 순서대로 실행되는 것처럼 보이고 어떤 때는 콘텐츠가 여기저기 흩어져 있습니다. 이 불변성은 스레드가 실행되는 방식으로 인해 발생합니다. 스케줄러는 각 스레드에 일정 시간을 제공하고 스레드는 그 시간 내에 완료되거나 다른 시간을 받을 때까지 정지됩니다.

<br>

<br>

### Challenges with thread

스레드를 사용하면 간단하게 여러 작업과 동시 실행을 사용할 수 있지만 문제가 없는 것은 아닙니다. `Thread`를 코드에서 직접 사용하면 여러 문제가 발생할 수 있습니다. 

#### 많은 리소스가 필요한 스레드

+ 스레드를 만들고 전환하고 관리하는 데는 동시에 관리할 수 있는 원시 스레드 수를 제한하는 시스템 리소스와 시간이 사용됩니다. 만들기 비용은 매우 늘어날 수 있습니다.

+ 실행 중인 앱에는 여러 스레드가 있지만 각 앱에는 전용 스레드가 하나 있고 특히 앱의 UI를 담당합니다. 이 스레드를 기본 스레드 또는 UI 스레드라고도 합니다.
+ 이 스레드는 앱의 UI 실행을 담당하므로 **기본 스레드가 앱이 원활하게 실행되도록 성능 기준에 맞는 것이 중요**합니다. 장기 실행 작업은 완료될 때까지 스레드를 차단하여 앱이 응답하지 않는 원인이 됩니다.
+ 운영체제는 사용자에게 응답성을 유지하기 위해 여러 작업을 시도합니다. 현재 휴대전화는 UI 업데이트를 초당 60회~120회(최소 60회) 시도합니다. 한정된 짧은 시간에 UI를 준비하고 그려야 합니다(초당 60프레임, 각 화면 업데이트에 걸리는 시간은 16ms 이하여야 함).

<br>

#### Race condition과 예측할 수 없는 동작

+ 앞에서 설명했듯이 **스레드**는 **프로세서가 어떻게 한 번에 여러 작업을 처리하는 것처럼 보이는지에 관한 추상화**입니다. 프로세서가 여러 스레드의 명령어 집합 간에 전환할 때 스레드가 실행되는 정확한 시간과 스레드가 일시중지되는 시점은 개발자가 제어할 수 없습니다. 스레드를 직접 사용할 때 항상 예측 가능한 출력을 기대할 수는 없습니다.

+ 예를 들어 다음 코드는 간단한 루프를 사용하여 1에서 50까지 세지만 이 경우에는 숫자가 증가할 때마다 새 스레드가 만들어집니다. 예상되는 출력 내용을 생각해본 후 코드를 몇 번 실행합니다.

  ```kotlin
  fun main() {
     var count = 0
     for (i in 1..50) {
         Thread {
             count += 1
             println("Thread: $i count: $count")
         }.start()
     }
  }uu
  ```

  출력

  ```kotlin
  Thread: 50 count: 49 Thread: 43 count: 50 Thread: 1 count: 1
  Thread: 2 count: 2
  Thread: 3 count: 3
  Thread: 4 count: 4
  Thread: 5 count: 5
  Thread: 6 count: 6
  Thread: 7 count: 7
  Thread: 8 count: 8
  Thread: 9 count: 9
  Thread: 10 count: 10
  Thread: 11 count: 11
  Thread: 12 count: 12
  Thread: 13 count: 13
  Thread: 14 count: 14
  Thread: 15 count: 15
  Thread: 16 count: 16
  Thread: 17 count: 17
  Thread: 18 count: 18
  Thread: 19 count: 19
  Thread: 20 count: 20
  Thread: 21 count: 21
  Thread: 23 count: 22
  Thread: 22 count: 23
  Thread: 24 count: 24
  Thread: 25 count: 25
  Thread: 26 count: 26
  Thread: 27 count: 27
  Thread: 30 count: 28
  Thread: 28 count: 29
  Thread: 29 count: 41
  Thread: 40 count: 41
  Thread: 39 count: 41
  Thread: 41 count: 41
  Thread: 38 count: 41
  Thread: 37 count: 41
  Thread: 35 count: 41
  Thread: 33 count: 41
  Thread: 36 count: 41
  Thread: 34 count: 41
  Thread: 31 count: 41
  Thread: 32 count: 41
  Thread: 44 count: 42
  Thread: 46 count: 43
  Thread: 45 count: 44
  Thread: 47 count: 45
  Thread: 48 count: 46
  Thread: 42 count: 47
  Thread: 49 count: 48
  ```

  + 코드가 나타내는 것과 달리 **마지막 스레드가 첫 번째로 실행되고 다른 스레드 중 일부가 순서에 맞지 않게 실행된 것 같습니다.** 일부 반복의 'count'를 보면 여러 스레드 후에도 변경되지 않고 유지되는 것을 알 수 있습니다. 더 이상한 점은 출력을 통해 실행할 두 번째 스레드일 뿐임을 알 수 있음에도 스레드 43에서 숫자가 50에 도달한다는 것입니다. 출력만 놓고 보면 `count`의 최종값을 알 수 없습니다.

  + 이는 스레드가 예측할 수 없는 동작으로 이어질 수 있는 한 가지 방법일 뿐입니다. 여러 스레드로 작업할 때는 경합 상태도 발생할 수 있습니다. 여러 스레드가 동시에 메모리의 동일한 값에 액세스하려고 할 때 발생합니다. 경합 상태로 인해 무작위로 보이는 버그를 재현하기 어려울 수 있고 이로 인해 예상치 못한 앱의 비정상 종료를 유발할 수 있습니다.

    성능 문제, 경합 상태, 재현하기 어려운 버그는 스레드를 직접 사용하라고 권장하지 않는 이유입니다. 대신 동시 실행 코드 작성에 도움이 되는 코루틴이라는 Kotlin의 기능에 관해 알아봅니다.

<br>

<br>

### Kotlin의 코루틴

+ 백그라운드 작업을 위한 스레드를 직접 만들고 사용하는 것은 Android에서 이루어지지만 Kotlin은 **동시 실행을 더 유연하고 쉽게 관리할 수 있는 코루틴도 제공**합니다.

+ 코루틴은 멀티태스킹을 지원하지만 단순히 스레드로 작업하는 것보다 다른 수준의 추상화를 제공합니다. 코루틴의 주요 기능 중 하나는 **상태를 저장하여 중단했다가 재개할 수 있다**는 것입니다. 코루틴은 실행되거나 실행되지 않을 수 있습니다.

+ *연속(continuations)*으로 표시되는 상태를 통해 코드 일부가 제어권을 넘겨주거나 재개되기 전에 다른 코루틴이 작업을 완료할 때까지 기다려야 하는 시기를 나타낼 수 있습니다. 이 흐름을 협력적인 멀티태스킹(cooperative multitasking)이라고 합니다. 

+ Kotlin의 코루틴 구현은 멀티태스킹을 지원하는 여러 기능을 추가합니다. 
  연속 외에도 코루틴을 만드는 것에는 `CoroutineScope` 내에서 수명 주기가 있는 취소 가능한 작업 단위인 `Job`의 작업이 포함됩니다. 
  `CoroutineScope`는 하위 요소와 그 하위 요소에 취소 및 기타 규칙을 반복적으로 적용하는 컨텍스트입니다. 
  `Dispatcher`는 코루틴이 실행에 사용할 지원 스레드를 관리하므로 개발자가 새 스레드를 사용할 시기와 위치를 파악하지 않아도 됩니다.

  + Job : 취소 가능한 작업 단위(예: `launch()` 함수로 만든 작업 단위)입니다.
  + CoroutineScope : `launch()` 및 `async()`와 같은 새 코루틴을 만드는 데 사용되는 함수는 `CoroutineScope`를 확장합니다.
  + Dispatcher : 코루틴이 사용할 스레드를 결정합니다. `Main` 디스패처는 항상 기본 스레드에서 코루틴을 실행하지만 `Default`나 `IO`, `Unconfined`와 같은 디스패처는 다른 스레드를 사용합니다.

  이 내용은 나중에 자세히 알아보겠지만 `Dispatchers`는 코루틴이 좋은 성능을 발휘할 수 있는 방법 중 하나입니다. 새 스레드를 초기화하는 데 드는 성능 비용이 발생하지 않도록 합니다.

<br>

+ 코루틴 사용 예제

  ```kotlin
  import kotlinx.coroutines.*
  
  fun main() {
      repeat(3) {
          GlobalScope.launch {
              println("Hi from ${Thread.currentThread()}")
          }
      }
  }c
  ```

  ```kotlin
  Hi from Thread[DefaultDispatcher-worker-2@coroutine#2,5,main]
  Hi from Thread[DefaultDispatcher-worker-1@coroutine#1,5,main]
  Hi from Thread[DefaultDispatcher-worker-1@coroutine#3`,5,main]
  ```

  위 스니펫은 기본 Dispatcher를 사용하여 Global Scope에서 코루틴 세 개를 만듭니다. `GlobalScope`는 앱이 실행되는 한 내부의 코루틴이 실행되도록 허용합니다. 기본 스레드에 관해 언급했던 이유로 인해 예 코드 외부에서는 권장되지 않습니다. 앱에서 코루틴을 사용할 때는 다른 범위가 사용됩니다.

  `launch()` 함수는 취소 가능한 Job 객체에 래핑된 닫힌 코드에서 코루틴을 만듭니다. `launch()`는 반환 값이 코루틴의 범위 밖에서 필요하지 않을 때 사용됩니다.

  코루틴의 중요한 다음 개념을 이해하기 위해 `launch()`의 전체 서명을 살펴보겠습니다.

  ```kotlin
  fun CoroutineScope.launch {
      context: CoroutineContext = EmptyCoroutineContext,
      start: CoroutineStart = CoroutineStart.DEFAULT,
      block: suspend CoroutineScope.() -> Unit
  }
  ```

  실제로 개발자가 실행을 위해 전달한 코드 블록은 `suspend` 키워드로 표시됩니다. suspend signals는 코드 또는 함수 블록이 일시중지되거나 재개될 수 있음을 나타냅니다.

<br>

#### runBlocking

다음 예에서는 이름에서 알 수 있듯이 새 코루틴을 시작하고 완료될 때까지 현재 스레드를 차단하는 `runBlocking()`을 사용합니다. 주로 기본 함수와 테스트에서 차단 코드와 비차단 코드 사이를 연결하는 데 사용됩니다. 일반적인 Android 코드에서는 자주 사용하지 않습니다.

```kotlin
import kotlinx.coroutines.*
import java.time.LocalDateTime
import java.time.format.DateTimeFormatter

val formatter = DateTimeFormatter.ISO_LOCAL_TIME
val time = { formatter.format(LocalDateTime.now()) }

suspend fun getValue(): Double {
    println("entering getValue() at ${time()}")
    delay(3000)
    println("leaving getValue() at ${time()}")
    return Math.random()
}

fun main() {
    runBlocking {
        val num1 = getValue()
        val num2 = getValue()
        println("result of num1 + num2 is ${num1 + num2}")
    }
}
```

<br>

`getValue()`는 설정된 지연 시간 후에 랜덤 숫자를 반환하며 `DateTimeFormatter`를 사용하여 적절한 출입 시간을 보여줍니다. main 함수는 `getValue()`를 두 번 호출하고 합계를 반환합니다.

```kotlin
entering getValue() at 17:44:52.311
leaving getValue() at 17:44:55.319
entering getValue() at 17:44:55.32
leaving getValue() at 17:44:58.32
result of num1 + num2 is 1.4320332550421415
```

<br>

실제 동작을 확인하려면 `main()` 함수를 다음으로 바꿉니다(다른 코드는 모두 유지)

```kotlin
fun main() {
    runBlocking {
        val num1 = async { getValue() }
        val num2 = async { getValue() }
        println("result of num1 + num2 is ${num1.await() + num2.await()}")
    }
}
```

두 번의 `getValue()` 호출은 독립적이므로 정지하는 데 코루틴이 필요하지는 않습니다

```kotlin
entering getValue() at 22:52:25.025
entering getValue() at 22:52:25.03
leaving getValue() at 22:52:28.03
leaving getValue() at 22:52:28.032
result of num1 + num2 is 0.8416379026501276
```

<br>

`async()` 함수의 정의

```kotlin
Fun CoroutineScope.async() {
    context: CoroutineContext = EmptyCoroutineContext,
    start: CoroutineStart = CoroutineStart.DEFAULT,
    block: suspend CoroutineScope.() -> T
}: Deferred<T>
```

`async()` 함수는 `Deferred` 유형의 값을 반환합니다. 
`Deferred`는 **미래 값 참조를 보유할 수 있는 취소 가능한 `Job`**입니다. `Deferred`를 사용하면 즉시 값을 반환하는 것처럼 함수를 계속 호출할 수 있습니다. 비동기(asynchronous) 작업이 언제 반환될지 확실히 알 수 없기 때문에 `Deferred`는 자리표시자 역할만 합니다. 
`Deferred`(다른 언어에서는 Promise나 Future라고도 함)는 **나중에 이 객체에 값이 반환된다고 보장**합니다. 반면 비동기 작업은 기본적으로 실행을 차단하거나 기다리지 않습니다. **현재 코드 줄이 `Deferred`의 출력을 기다리도록 하려면 코드 줄에서 `await()`를 호출하면 됩니다.** 그러면 원시 값(raw value)이 반환됩니다.

<br>

#### 함수를 suspend로 표시하는 경우

+ 앞의 예에서 알 수 있듯이 `getValue()` 함수도 `suspend` 키워드로 정의됩니다. `suspend` 함수이기도 한 `delay()`를 호출하기 때문입니다. 함수가 또 다른 `suspend` 함수를 호출하면 언제든지 그 함수는 `suspend` 함수여야 합니다.
+ 그렇다면 이 예에서 `main()` 함수가 `suspend`로 표시되지 않은 이유는 무엇인가요? 결국 `getValue()`를 호출합니다.
+ 꼭 그렇지는 않습니다. `getValue()`는 `launch()`와 `async()`에 전달된 함수와 비슷한 `runBlocking()`에 전달된 함수인 `suspend` 함수에서 호출됩니다. 그러나 `getValue()`가 `main()` 자체에서 호출되지도 않고 `runBlocking()`이 `suspend` 함수도 아니므로 `main()`은 `suspend`로 표시되지 않습니다. 함수가 `suspend` 함수를 호출하지 않으면 그 자체가 `suspend` 함수가 아니어도 됩니다.

<br>

<br>

### 코루틴 사용

처음 코드

```kotlin
fun main() {
   val states = arrayOf("Starting", "Doing Task 1", "Doing Task 2", "Ending")
   repeat(3) {
       Thread {
           println("${Thread.currentThread()} has started")
           for (i in states) {
               println("${Thread.currentThread()} - $i")
               Thread.sleep(50)
           }
       }.start()
   }
}
```

<br>

코루틴 사용

```kotlin
import kotlinx.coroutines.*

fun main() {
   val states = arrayOf("Starting", "Doing Task 1", "Doing Task 2", "Ending")
   repeat(3) {
       GlobalScope.launch {
           println("${Thread.currentThread()} has started")
           for (i in states) {
               println("${Thread.currentThread()} - $i")
               delay(5000)
           }
       }
   }
}
```

<br>

<br>

## 🎖 Quiz/Unit4/Pathway4 

1. 빈칸 채우기

   **기본** 스레드(UI 스레드라고도 함)는 Android 앱에서 화면을 업데이트하는 역할을 합니다.

<br>

2. 다음 중 코드에서 스레드를 직접 사용하는 경우 초래될 수 있는 위험은 무엇인가요?

   =>

   + 경합 상태 발생
   + 출력이 일관되지 않음
   + UI가 응답하지 않음

<br>

3. 코루틴에 관한 다음 설명 중 참인 것은 무엇인가요?

   => 코루틴은 실행되거나 실행되지 않을 수 있습니다.

<br>

4. 참 또는 거짓: 함수가 이미 `suspend` 함수를 호출한 경우 자체적으로 정지 함수로 표시할 필요가 없습니다.

   => 거짓

<br>

5. 다음 중 `suspend` 함수는 무엇인가요?

   => 

   + `async()`에 전달된 람다
   + `runBlocking()`에 전달된 람다

<br>

6. `async()` 및 `runBlocking()`에 관한 다음 설명 중 거짓인 것은 무엇인가요?

    => 두 함수 모두 Deferred를 반환합니다.

<br>

7. 참 또는 거짓: 대부분의 앱에서는 전역 범위를 사용하여 코루틴을 만듭니다.

   => 거짓

<br>

8. 코루틴이 이면에서 사용하는 스레드를 결정하는 역할을 하는 것은 무엇인가요?

   => `Dispatcher`

<br>

9. 빈칸 채우기

   **Deferred**은(는) 다른 언어의 Promise 또는 Future와 유사하며 반환 값의 자리표시자 역할을 합니다.

<br>

10. 참 또는 거짓: `Job`은 코루틴이 실행하는 취소 가능한 작업 단위입니다.

    => 참