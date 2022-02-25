## 🚩 RecyclerView

### RecyclerView란?

+ 앱에서의 List를 표현할 때 사용하는 뷰
+ 가로/세로/격자 방향을 지원
+ ItemDecoration을 이용해 애니메이션을 넣을 수 있음
+ 이름 그래도 View를 재사용하기 때문에 효율적임
+ ListView보다 유연 -> 커스텀이 편함
+ ViewHolder 패턴을 강제 

<br>

#### RecyclerView VS ListView

<img src = "https://user-images.githubusercontent.com/31370590/138226738-a37effa7-08fd-451c-a7ce-bf73b9b8ff60.PNG">

<br>

### 도넛 비유로 RecyclerView 이해하기

+ 맛이 다른 **도넛**을 묶어서 판매하고 싶다. **포장지**를 만들고 이 포장지를 가지고 **업체**가 도넛을 포장해줌. 그러면 **도넛 묶음**이 완성된다. 

  <img src = "https://user-images.githubusercontent.com/31370590/138227600-3e1ad23c-3ef1-4046-abc1-5e3e7ac24848.PNG">

  + 도넛 - data
  + 포장지 - Viewholder
  + 업체 - Adapter
  + 도넛 묶음 - RecyclerView

<br>

### RecyclerView 작업 순서

+ 리스트에 반복적으로 보여질 **아이템의 Layout(xml) 만들기**
+ 아이템의 **data class** 만들기
+ 아이템 뷰의 UI요소를 가지고 있는 **ViewHolder** 만들기
+ ViewHolder를 생성하고 ViewHolder에 데이터를 전달하는 **Adapter**만들기
+ **RecyclerView** 배치하기
+ RecyclerView 아이템의 **배치방향(가로/세로/격자)** 확인하기(LayoutManager)
+ RecyclerView에 **Adapter** 연결하기
+ Adapter의 **데이터 갱신**하기



<br>

##### 1. 아이템 레이아웃 만들기

+ `layout > new > Layout Resource File`을 클릭 해 `item_sample_list`로 이름을 지어 새로운 item layout을 만든다.

+ 그리고 거기에 원하는 뷰를 배치한다.

  ex) textView, textView, imageView

<br>

##### 2. 아이템의 data class 만들기

+ 우리가 만든 item layout에 넣어줄 data를 담는 클래스

+ `java > com.example.~ > new > Kotlin Class/File `

```kotlin
data class UserData{
    val name : String, // 이름
    val introduction : String // 소개 
}
```

+ 이제 이 data들을 **ViewHolder**가 가지고 있는 View(Item layout)에 넣어주면 되겠구나

<br>

##### 3, 4. ViewHolder, Adapter 만들기

##### ViewHolder란?

+ RecyclerView의 재활용 되는 Item Layout(View)를 붙잡고 관리하는 역할
+ Adapter에서 전달받은 데이터를 Item Layout에 Bind 시켜주는 역할

+ VIewHolder는 계속해서 재활용 됨

<br>

##### Adapter란?

+ 포장지(ViewHolder)를 만들고 이 포장지를 가지고 도넛(data)을 포장(bind)해주는 업체

+ ViewHolder를 생성하고 ItemLayout을 ViewHolder에 넘겨준다.
+ 리스트로 보여줄 Data를 각 ViewHolder에 전달해준다. 

<br>

=> ViewHolder는 Adapter로부터 Item Layout(view)도 받고, 그 view에 띄울 data도 받는다. 받아서 data를 Item Layout에 Bind 시켜준다. 

<br>

`Adapter class` code

<img src = "https://user-images.githubusercontent.com/31370590/138236424-349cd932-6df9-4135-afe5-0ed410422e43.PNG">

`ViewHolder` 코드 분석

+ Binding 객체를 생성자로 가지는 ViewHolder 클래스 생성

  `ItemSampleListBinding`

+ RecyclerView.ViewHolder 클래스 상속

  이 때, RecyclerView.ViewHolder 클래스는 생성자로 View를 요구하므로, **binding.root(root뷰)**를 넘겨준다. 

  (이때 넘겨주는 View는 재활용되는 ItemLayout(`item_sample_list.xml`의 root 뷰이다.)

+ `onBind()`함수

  ViewHolder가 가진 View에 Adapter로부터 전달받은 data를 붙여주는 함수

  (Adapter에서 **onBindViewHolder()** 호출 시 실행된다.)

<br>

`Adapter` 코드 분석

+ RecyclerView.Adapter()를 상속 받는다.

  <>안에 해당 Adapter가 데이터를 전달할 ViewHolder 클래스 작성

###### override 해야하는 함수 3가지

1. `getItemCount()`

   + RecyclerView로 보여줄 전체 데이터의 개수 반환

2. `onCreateViewHolder()`

   + ViewHolder를 생성하고 ItemLayout의 Binding 객체를 만들어 ViewHolder의 생성자로 넘겨주는 함수

     => 이 때, View(Item Layout)을 ViewHolder에게 넘겨준다 !

   + Binding 객체를 생성할 때, **LayoutInflater.from**을 통해 **LayoutInflater(뷰를 만들 때 사용)를 생성**한다. 이때, LayoutInflater.from의 context인자로는 parent(ViewGroup)의 context를 넘긴다. 

3. `onBindViewHolder()`

   + 재활용 되는 뷰(ViewHolder의 뷰)가 호출하여 실행되는 함수
   + **ViewHolder와 position의 데이터를 결합**시키는 역할을 한다.

<br>

##### 5. RecyclerView 배치하기

<img src = "https://user-images.githubusercontent.com/31370590/138240550-29060a20-86cd-46ad-a975-a649d1f46ab5.PNG" width = "900" height = "350">

+ itemCount
+ listitem 

<br>

##### 6. RecyclerView 아이템의 **배치방향(가로/세로/격자)** 확인하기(LayoutManager)

`app:layoutManager = "andriodx.recyclerview.widget.LinearManager"`

<br>

##### 7, 8. RecyclerView에 **Adapter** 연결하기, Adapter의 data 갱신하기

`MainActivity` code

<img src = "https://user-images.githubusercontent.com/31370590/138242205-82aef629-3662-44b5-b639-848842cc126a.PNG">









-----









매번 사용자가 아래로 스크롤 할 때 마다 맨 위에 위치한 뷰 객체가 새로 삭제되고, 아랫 부분에서 새로 나타날 채팅방 뷰 객체를 새로 생성하면 결국 100개의 뷰 객체가 삭제되고 생성되는 것일 뿐만 아니라, 스크롤을 위아래로 왔다 갔다 하면 수 백개의 뷰 객체가 새로 생성되고 삭제됨을 반복한다.

리사이클러 뷰는 사용자가 아래로 스크롤 한다고 가정했을 때, **맨 위에 존재해서 이제 곧 사라질 뷰 객체를 삭제 하지않고 아랫쪽에서 새로 나타나날 파란색 뷰 위치로 객체를 이동시킨다.** 즉 뷰 객체 자체를 재사용 하는 것인데, **중요한 점은 뷰 객체를 재사용 할 뿐이지 뷰 객체가 담고 있는 데이터(채팅방 이름)는 새로 갱신된다는 것**이다. 어쨋거나 뷰 객체를 새로 생성하지는 않으므로 효율적인 것이다.

결과적으로 보자면, 맨 처음 화면에 보여질 10개 정도의 뷰 객체만을 만들고, 실제 데이터가 100개든 1000개든 원래 만들어 놓은 10개의 객체만 계속 해서 재사용 하는 것이다.

따라서 맨 처음 10개의 뷰객체를 기억하고 있을(홀딩) 객체가 필요한데 이 것이 ViewHolder이다. 나중에 전체 코드를 보겠지만, ViewHolder 코드 부분만 보자면 아래와 같다.

```kotlin
class MyViewHolder(view: View): RecyclerView.ViewHolder(view) {
    var textField = view.chat_title
}
```

```kotlin
// MainActivity
override fun onCreate(savedInstanceState: Bundle?) {
    super.onCreate(savedInstanceState)
    setContentView(R.layout.activity_recycler_view)

    val datas = Array(100) {
        "chat $it"
    }

    recycler_view.adapter = MyApdater(datas)
    recycler_view.layoutManager = LinearLayoutManager(this)
    // 코드단에서 layoutmanager 설정하기
}
```



참고

+ [리사이클러뷰의 원리와 사용법](https://wooooooak.github.io/android/2019/03/28/recycler_view/)
+ [멀티뷰 타입 리사이클러뷰 만들기](https://wooooooak.github.io/android/2019/04/13/RecyclerView_mutiType/)

