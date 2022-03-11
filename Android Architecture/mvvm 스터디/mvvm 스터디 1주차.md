## mvvm 스터디 1주차

개발엔 정답이 없다

=> 장, 단점과 특징이 있을 뿐 

=> 모든 것을 의심하라 

=> 남들 코드 엄청 많이 봐라 100개 ?

=> 다른 사람의 코드를 보면서 내가 싫은 코드는 왜 싫은지 이유도 적어놓아라

<br>

아키텍쳐를 왜 쓰나 ? 

우리는 다른 사람과 함께 일을 해야 함 

퇴사한 사람의 코드를 봐야하기도 함

=> 아키텍쳐를 적용한 프로젝트는 구조가 비슷비슷해진다. 

=> 코드의 역할, 의존관계가 잘 분리 

<br>

### 🚩 MVC

+ Activity에 모든 코드를 받아버리는 구조

+ View에 model이 박혀있어서 완벽한 분리 x	

<br>

### 🚩 MVP

+ View는 Presenter에게 모든 일을 시키고, Presenter는 View가 원하는 데이터들을 model로부터 가져옴. 
+ Presenter는 중간 다리 역할. 가져온 데이터를 view에 알린다. 
+ View는 아는게 없음 => 띄워주기만 함. 
+ View와 model은 깔끔하게 분리되었지만, 기능이 조금만 많아질수록 Presenter가 엄청나게 커짐.
+ Presenter가 View와 1:1 관계라 계속 필요함 

<br>

### 🚩 MVVM

View => ViewModel => model

+ View는 Viewmodel을 알고 있고, Viewmodel은 model을 알고 있다. 

+ 역방향으로는 모른다.  model은 Viewmodel을 알지 못하고, Viewmodel은 View를 알지 못한다. **알아서는 안된다.**

+ View는 Viewmodel을 관찰하고 있다. 무엇인가 바뀌면 View가 알아서 변경 

+ 사실 mvvm은 layer가 하나 더 숨어져있다. 

  => View와 Viewmodel 사이에 **binder**가 숨어있다.  

  + 안드로이드에서는 binder를 databinding으로 지원
  + databinding을 안쓰면 mvvm이 아니다 ! => 이거는 mvp다 

+ ***mvvm의 Viewmodel은 AAC의 Viewmodel과 다르다.*** 

  원래는 AAC의 Viewmodel을 쓰지 않고도 mvvm을 구현할 수 있어야 한다. 애초에 mvvm은 microsoft 사에서 발표한 아키텍쳐이다. => 단순히 AAC의 Viewmodel을 썼다고 해서 mvvm이라고 부르는 것은 아님 

+ mvvm에서의 Viewmodel
  + activity와 fragment의 lifecycle과의 의존성을 낮추기 위한 것 

+ AAC의 Viewmodel
  + 많은 일을 함
  + activity와 fragment의 lifecycle에 의존적일 수 밖에 없음 
  + 그냥 데이터를 담는 모델 느낌 ?

+ mvvm의 가장 큰 목적 

  => view와 ViewModel의 연결을 최소화 

+ AAC의 Viewmodel을 가지고 mvvm을 설명하려고 한다면 네이버 1차 면접도 통과하지 못할 것이다 

  => AAC의 ViewModel과 mvvm의 ViewModel은 그만큼 서로 다르다. 

+ 구글의 아키텍쳐 내용 공식문서를 봐도 mvvm이라는 단어 사용하지 않음 

  => 권장 아키텍쳐라고만 써있음 



+ 구글의 권장 아키텍쳐

  + presentation layer => domain layer => data layer

    (View => ViewModel => model)

  + model = domain(use case , repository) +  data(data source, retrofit/room/ ~)

  + domain이란

    + 프로젝트에서 무엇을 만들까 ?  => 핵심요소들 
    + 프로젝트를 관통하는 핵심 로직들 

  + domain data은 다 서버에 들어가 있다. 우린 요청하면 받을 뿐.
  + usecase는 정보가 안드로이드 로컬에서 오는지 서버에서 오는지 몰라도 됨, repo는 알고 있어야 함. repo는 data source를 갖고 있음. local data source, remote data source 이렇게 2개의 data source를 갖고 있음 . 
  + data source는 repository가 local이나 remote로 data를 요청할텐데 repo는 어떤 local에서 온 건지 알 필요가 없음. SQL Lite에서 온건지 메모리에서 온건지 알 필요가 없음. 그냥 data source에서 온 것. remote도 마찬가지. repository는 어떤 remote에서 왔는지 알 필요가 없음. 

  +  RemoteDataSource라는 Interface를 만들고 ~~ LocalDataSource라는 Interface도 만들고 ~~

    => 왜 이렇게 하는지 모르겠음

  + Data source는 이름 그 자체로 data source 이다. 

    => DataSource라는 Interface 하나만 만들면 된다. 

##### findViewById

+ 안드로이드에서 태초의 뷰를 찾는 방법

+ 하지만 ***findViewById 방법은 null unsafe, type unsafe하다***. 

  => 다른 Activity의 view와 binding 할 수도 있고, 같은 activity내의 다른 뷰(ex)버튼인데 framelayout)와 binding 될 수도 있다.  
  
  => 이러한 null unsafe, type unsafe를 view binding이 해결 !

##### viewBinding

+ null unsafe, type unsafe를 방지할 수 있다

##### dataBinding

+ databinding 안쓰면 mvvm이 아니다. => mvp다 

+ view를 어떻게 만드는가 ? 

  xml파일은 xml 파일일 뿐, 이 xml을 써먹을려면 이 뷰들을 핸드폰에서 만들어내야 하는데, 핸드폰은 JVM을 쓰고 있다. 근데 xml을 넣었다고 해서 뷰를 만들 수 없다. xml을 **parsing** 해야한다. 이를 **inflate**가 해주는 것. 

  inflater가 xml을 쭉 parsing함. inflater안에 xml parser가 있음. 무식하게 string 다 긁어와서 parsing 하는 것.  





원래 xml의 `android:text = `에서 string 값이 아닌 string resource id인 int가 들어간다. 

=> `android:text = "@{String.valueOf(bindingInt)}"` 이렇게 사용



`app:createDate="@{diary.createDate}"` 이렇게 쓰고 싶다면 DataBindingAdapter를 만들어야 함.



`BindingAdapter`

```kotlin
@BindingAdapter("app:createDate")
fun bindCreateDate(textView: TextView, data: Date?){
    val dateFormat = SimpleDateFormat("yyyy.MM.dd", Locale.KOREA)
    val createDataString = dataFormat.format(date ?: return)
    textView.text = createDateString 
}
```













### 추가 공부

#### AAC ViewModel vs MVVM ViewModel

+ 위에서 MVVM 패턴에서의 ViewModel과 AAC에서의 ViewModel의 특징에 대해 알아보았습니다. 간단하게 요약해보자면, MVVM ViewModel은 **View에 필요한 데이터를 관리하여 바인딩 해주고, 비즈니스 로직을 담당해 데이터를 처리하는 요소**, AAC의 ViewModel은 **Android의 수명 주기를 고려하여 UI 관련 데이터를 저장하고 관리하는 요소**로 요약할 수 있습니다.

  두 ViewModel의 역할을 보면 다른 개념인 것을 알 수 있습니다. 실제로 AAC의 ViewModel을 사용하지 않고도 MVVM 패턴을 구현할 수 있습니다. 반대로 AAC ViewModel을 사용했다고 해서 MVVM 패턴이 되지는 않습니다. 

  MVVM 패턴에 대한 예제 프로젝트를 찾아보면 대부분이 AAC의 ViewModel을 사용하고 있습니다. MVVM 패턴의 ViewModel과 AAC의 ViewModel은 전혀 다른 개념인데 왜 다들 AAC의 ViewModel을 사용하는 것일까요? 

  => **AAC의 ViewModel로 MVVM 패턴의 ViewModel을 구현할 수 있기 때문**. MVVM 패턴의 ViewModel의 역할은 위에서 보았듯이 View에 필요한 데이터를 관리하여 바인딩해주는 것입니다. AAC의 ViewModel을 위의 개념대로 구현해주면 됩니다. ViewModel 내에서 ObservableField나 LiveData 등을 사용하여 데이터 바인딩 해준다면 MVVM 패턴의 ViewModel로써 사용이 가능합니다.

> 참고 - [AAC ViewModel vs MVVM ViewModel](https://wooooooak.github.io/android/2019/05/07/aac_viewmodel/)
>
> ​		- [하나 더](https://leveloper.tistory.com/216)











### 더 알아볼 것 

+ 인터페이스, 구현체, 다형성 
+ 파싱 