LiveData는 Observer 패턴을 따르며 데이터의 변경이 일어날 때마다 콜백을 받아 원하는 동작을 실행할 수 있다. 이때 LiveData의 값을 변경하게 해주는 함수가 바로 setValue()와 postValue()이다.

#### **setValue()**

setValue()는 **메인 쓰레드**에서 LiveData의 값을 변경해준다. 메인 쓰레드에서 바로 값을 변경해주기 때문에 setValue() 함수를 호출한 뒤 바로 밑에서 getValue() 함수로 값을 읽어오면 변경된 값을 가져올 수 있다. 중요한 점은, **setValue()는 메인 쓰레드에서 값을 dispatch 하기 때문에 백그라운드에서 setValue()를 호출한다면 오류가 나게 된다.** setValue()가 동작하지 않는다면, 해당 함수가 호출되는 쓰레드가 메인 쓰레드인지 체크해봐야 한다.

<br>

#### **postValue()**

 postValue()의 설명으로 구글 공식문서에는 아래와 같이 나와있다.

> If you need set a value from a background thread, you can use postValue(Object) Posts a task to a main thread to set the given value. If you called this method multiple times before a main thread executed a posted task, only the last value would be dispatched.

 postValue()는 setValue()와 다르게 **백그라운드**에서 값을 변경한다. 백그라운드 쓰레드에서 동작하다가 메인 쓰레드에 값을 post 하는 방식으로 사용된다. 함수 내부적으로는 아래와 같은 코드가 실행된다.

```
new Handler(Looper.mainLooper()).post(() -> setValue())
```

 메인 쓰레드에 적용되기 전에 postValue()가 여러 번 호출된다면 모든 값이 적용되는 것이 아니라 가장 최신의 값이 적용된다. 따라서 postValue()를 호출한 뒤 바로 getValue()로 값을 읽으려고 한다면 변경된 값을 읽어오지 못할 가능성이 높다. Hander()를 통해 메인 쓰레드에 값이 전달되기 전에 getValue()를 호출하기 때문이다. LiveData의 값을 즉각적으로 변경해야 한다면 postValue()가 아닌 setValue()를 사용해야 한다.



>  참고
>
> + [꾸준하게](https://leveloper.tistory.com/179)



