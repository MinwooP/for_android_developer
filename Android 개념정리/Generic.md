> Generics는 클래스나 함수를 정의할 때 타입을 확실히 정하지 않는 것을 말한다. 그렇기 때문에 다양한 타입으로 클랫스를 여러개 정의하지 않아도 된다. 
>
> Generic 함수의 정의
>
> ```kotlin
> fun <T> addNumbers(num1: T, num2: T): T {
>     return (num1.toDouble() + num2.toDouble()) as T
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

