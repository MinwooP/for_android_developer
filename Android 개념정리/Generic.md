## Generic

프로그래밍 언어에는 Int, Long, Char 등 여러 타입이 존재합니다. 자신의 프로그램에 따라 타입을 적절하게 지정하는 것은 중요한데, 가끔은 **모든 타입에 대해 동작을 하는 함수나 클래스를 구현하고자 할 때**가 있습니다. 이 때 사용하게 되는 것이 제네릭입니다. **즉 제네릭(Generic)은 어떤 타입에 관계없이 일반화하는 것입니다.** 일반화하다 (generalize) 에서 따와 Generic이 된 모양입니다. 사실 코틀린 말고도 다른 다양한 언어에서도 제네릭을 지원합니다. 그럼 코틀린에서는 어떻게 사용하는지 알아봅시다

<br>

#### 📌 Generic 함수

Generic 함수를 정의할 때, 타입이 정해지지 않은 변수는 함수 이름 앞에 `<T>`처럼 정의되어야 합니다. 아래 코드는 타입 T 변수 num1과 num2를 더하고 타입 T 변수를 리턴하는 함수입니다.

```kotlin
fun <T> addNumbers(num1: T, num2: T): T {
    return (num1.toDouble() + num2.toDouble()) as T
}
```

위 함수는 아래 처럼 호출할 수 있습니다.

```kotlin
fun main(args: Array<String>) {
    println(addNumbers(10, 20))      // 결과: 30
    println(addNumbers(10.1, 20.1))  // 결과: 30.200000000000003
}
```

T는 타입이 정해지지 않았기 때문에 어떤 타입이든 올 수 있습니다.

=> 키워드 `fun`과 함수명 사이에 `<T>`를 써주고, 매개변수나 리턴타입에 T를 활용할 수 있다. 

<br>

#### 📌Generic 클래스

Generic 클래스를 정의할 때 타입이 정해지지 않은 변수는 클래스 이름 다음에 <T>를 붙여서 정의합니다. Generic 함수와 다른 것은 **클래스 이름 다음에 `<T>`가 온다**는 것입니다.

아래 코드는 임의의 타입 T를 받는 Rectangle 클래스 입니다. T의 타입은 설정되지 않았기 때문에 어떤 타입이든 올 수 있습니다.

```kotlin
class Rectangle<T>(val width: T, val height: T) {
}
```

아래 코드는 위에서 정의한 Rectangle 클래스를 생성하는 코드입니다. **객체를 생성할 때 `Rectangle<Double>`처럼 T의 타입이 무엇인지 써줘야 합니다.**

```kotlin
fun main(args: Array<String>) {
    val rec = Rectangle<Double>(10, 20)
    val rec1 = Rectangle<String>("aa", "bb")
}
```

<br>

#### 📌 사용예시

```kotlin
abstract class BaseFragment<T : ViewDataBinding>(@LayoutRes val layout: Int) : Fragment() {
    private var _binding: T? = null
    protected val binding get() = _binding ?: error("View를 참조하기 위해 binding이 초기화되지 않았습니다.")

    override fun onCreateView(
        inflater: LayoutInflater, container: ViewGroup?,
        savedInstanceState: Bundle?
    ): View? {
        _binding = DataBindingUtil.inflate(inflater, layout, container, false)
        return binding.root
    }

    override fun onDestroyView() {
        super.onDestroyView()
        _binding = null
    }

    abstract fun initView()
}
```



> 참고
>
> + [코틀린의 제네릭](https://keykat7.blogspot.com/2021/07/kotlin-generic.html)





















> 
>
> 
>
> Generics는 클래스나 함수를 정의할 때 타입을 확실히 정하지 않는 것을 말한다. 그렇기 때문에 다양한 타입으로 클랫스를 여러개 정의하지 않아도 된다. 
>
> Generic 함수의 정의
>
> ```kotlin
> fun <T> addNumbers(num1: T, num2: T): T {
>  return (num1.toDouble() + num2.toDouble()) as T
> }
> ```
>
> + 타입 T 변수 num1과 num2를 더하고 타입 T 변수를 리턴하는 함수이다.
>
> 
>
> Generic 클래스 정의
>
> ```kotlin
> class Rectangle<T> (val width: T, val height: T) {
> }
> 
> // 호출시
> val rec1 = Rectangle<String>("aa", "bb")
> ```

