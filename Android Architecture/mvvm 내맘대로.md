### 📌 ViewModel에 데이터 저장하기

1.  ViewModel class 추가

   ```kotlin
   class GameViewModel : ViewModel() {
   }
   ```

2. `ViewModel`을 프래그먼트에 연결하기

   + ViewModel을 사용할 View(Activity, Fragment) 내에 viewModel에 관한 참조(객체)를 만든다. 

   ```kotlin
   private val viewModel: GameViewModel by viewModels()
   ```

   => 코틀린의 프로퍼티 위임을 이용해 설명하면 `GameViewModel` type의 변수인 `viewModel`의 값을 읽고 쓸 때, 위임받은 `viewModels`가 대신 값을 읽고 쓴다. 
   
3. ViewModel로 데이터 이동하기

   `GameFragment` 클래스에서 `GameViewModel` 클래스로 데이터 변수를 이동한다.

   ```kotlin
   class GameViewModel : ViewModel() {
   
       private var score = 0
       private var currentWordCount = 0
       private var currentScrambledWord = "test"
   }
   ```

   몇몇 프로퍼티에 backint property 추가

   ```kotlin
   private var _currentScrambledWord = "test"
   val currentScrambledWord: String
      get() = _currentScrambledWord
   ```

4. ViewModel 채우기

   ViewModel 클래스 내의 프로퍼티들을 가지고 작업하는 메서드를 추가할 수 있다. 

   ```kotlin
   class GameViewModel : ViewModel() {
       private var wordsList: MutableList<String> = mutableListOf()
      	private lateinit var currentWord: String
       
       private fun getNextWord() {
      		currentWord = allWordsList.random()
   	}
   }
   ```






### 📌 ViewModel과 함께 LiveData 사용

ViewModel내의 데이터를 LiveData로 변환하고(LiveData로 데이터를 래핑) 이 LiveData 객체에 관찰자를 추가하고 LivewData를 관찰

1. ViewModel 내의 data의 type을 LiveData or MutableLiveData로 바꾼다. 

   + `GameViewModel`에서 변수 `_currentScrambledWord`의 유형을 `MutableLiveData<String>`으로 변경

   + `LiveData`/`MutableLiveData` 객체의 값은 동일하게 유지되고 이 객체에 저장된 데이터만 변경되기 때문에 `_currentScrambledWord`의 변수 유형을 `val`로 변경합니다.

     ```kotlin
     private val _currentScrambledWord = MutableLiveData<String>()
     val currentScrambledWord: LiveData<String>
        get() = _currentScrambledWord
     ```

   + `LiveData` 객체 내의 데이터에 액세스하려면 `value` 속성을 사용한다.

2. LiveData 객체에 관찰자 연결하기

   + LiveData가 쓰이는 Activity나 Fragment에`LiveData`의 관찰자를 연결한다.

     + `GameFragment`의 `onViewCreated()` 콜백 끝에서 `currentScrambledWord`에 관해 `observe()` 메서드를 호출합니다.

       ```kotlin
       // Observe the scrambledCharArray LiveData, passing in the LifecycleOwner and the observer.
       viewModel.currentScrambledWord.observe(viewLifecycleOwner,
          { newWord ->
             binding.textViewUnscrambledWord.text = newWord
          })
       ```

       > 첫번째 매개변수로 전달되는 `viewLifeCycleOwner`는 `LiveData`가 `GameFragment`의 수명 주기를 인식하고, `GameFragmet`가 활성 상태(`Started` 또는 `Resumed`)일 때만 관찰자에 알릴 수 있다. 

       + 이제 `currentScrambledWord`의 값이 바뀌면 자동으로 `textViewUnscrambledWord`의 `text`가 업데이트 됨.

       => 이렇게 LiveData에서는 observe 함수를 통해 관찰자를 설정하여, LiveData의 값이 바뀔 때마다 observe내에 선언된 람다를 통해 layout view의 데이터를 업데이트해주었다. 

       => 하지만 databinding을 사용한다면, liveData 값이 변경될 때마다 layout의 UI 에 자동으로 업데이트 되도록 

3. Data binding과 함께 LiveData 사용하기

   1. 사전 세팅

   2. ```xml
      <layout>
          <data>
             <variable
             name="gameViewModel"
             type="com.example.android.unscramble.ui.game.GameViewModel" />  
              
             <variable
             name="maxNoOfWords"
             type="int" />
          </data>
      
      </layout>
      ```

   3. `GameFragment`의 `onViewCreated()` 메서드 시작 부분에서 레이아웃 변수 `gameViewModel` 및 `maxNoOfWords`를 초기화합니다.

      ```kotlin
      override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
         super.onViewCreated(view, savedInstanceState)
      
         binding.gameViewModel = viewModel
      
         binding.maxNoOfWords = MAX_NO_OF_WORDS
      ...
      }
      ```

   4. 레이아웃에 수명 주기 소유자를 전달해야 합니다.

      ```kotlin
      binding.lifecycleOwner = viewLifecycleOwner
      ```

   5. 레이아웃에 결합 표현식 사용

      ```kotlin
      <TextView
         android:id="@+id/textView_unscrambled_word"
         ...
         android:text="@{gameViewModel.currentScrambledWord}"
         .../>
      ```

      + `GameFragment`에서 `currentScrambledWord`의 `LiveData` 관찰자 코드를 삭제합니다. 프래그먼트에 더 이상 관찰자 코드가 필요하지 않습니다. `LiveData` 변경사항 업데이트가 레이아웃에 직접 수신됩니다.

<br>

아직까지는 한 Activity에 그 Activity에서 사용하는 data들이 변수로 다 선언되어 있고, 다른 Activity로 이동할 때 마다 필요한 data들을 넘겨줬었음. 이제는 Shared ViewModel을 이용하여 이를 서로 공유





### 📌 Shared ViewModel

공유 ViewModel을 사용하여 앱의 데이터를 단일 ViewModel에 저장한다. 앱의 여러 프래그먼트는 activity scope를 사용하여 공유 ViewModel에 접근한다.

사용자는 첫 번째 화면에서 컵케이크의 수량을 선택합니다. 그러면 두 번째 화면에 가격이 컵케이크의 수량에 따라 계산되어 표시됩니다. 마찬가지로 맛 및 수령 날짜와 같은 다른 앱 데이터는 요약 화면에서도 사용됩니다.



**공유 뷰모델을 구현하는 방법**

1. 프로젝트에서 `model`이라는 새 패키지를 만들고 `OrderViewModel` 클래스를 추가한다. 그러면 나머지 UI 코드에서 뷰 모델 코드가 분리된다. 

2. ViewModel 클래스를 만들고, LiveData를 추가하고, 이와 관련된 메서드를 정의한다.

   ```kotlin
   import androidx.lifecycle.ViewModel
   
   class OrderViewModel : ViewModel() {
       
       private val _quantity = MutableLiveData<Int>(0)
   	val quantity: LiveData<Int> = _quantity
   
   	private val _flavor = MutableLiveData<String>("")
   	val flavor: LiveData<String> = _flavor
   
   	private val _date = MutableLiveData<String>("")
   	val date: LiveData<String> = _date
   
   	private val _price = MutableLiveData<Double>(0.0)
   	val price: LiveData<Double> = _price
       
       fun setQuantity(numberCupcakes: Int) {
       _quantity.value = numberCupcakes
   	}
   
   	fun setFlavor(desiredFlavor: String) {
      		_flavor.value = desiredFlavor
   	}
   
   	fun setDate(pickupDate: String) {
       	_date.value = pickupDate
   	}
   }
   ```

3. ViewModel을 사용하도록 Fragment 업데이트

   1. `StartFragment` 클래스에서 공유 뷰 모델의 참조를 클래스 변수로 가져옵니다. `fragment-ktx` 라이브러리의 `by activityViewModels()` Kotlin 속성 위임을 사용합니다.

      ```kotlin
      private val sharedViewModel: OrderViewModel by activityViewModels()
      ```

      + `viewModels()`는 현재 프래그먼트로 범위가 지정된 `ViewModel` 인스턴스를 제공합니다. 따라서 인스턴스는 프래그먼트마다 다릅니다.
      + `activityViewModels()`는 현재 활동으로 범위가 지정된 `ViewModel` 인스턴스를 제공합니다. 따라서 인스턴스는 동일한 활동의 여러 프래그먼트 간에 동일하게 유지됩니다.

   2. ViewModel을 사용하는 각 Fragment에서 1번 단계를 반복한다. 

   3. 각 프래그먼트에서 ViewModel의 메서드를 사용하여 live data의 값을 변경할 수 있다. 

      ```kotlin
      fun orderCupcake(quantity: Int) {
          sharedViewModel.setQuantity(quantity)
          findNavController().navigate(R.id.action_startFragment_to_flavorFragment)
      }
      ```

      + StartFragment에서 어떤 버튼을 클릭했을 때, 참조하고 있는 뷰 모델의 메서드인 sharedViewModel.setQuantity를 사용해 quantity의 값을 업데이트 한다. 

   4. 데이터 바인딩과 함께 공유 뷰 모델 사용

      1. 데이터 바인딩으로 Fragment의 레이아웃을 바꾸고, viewModel이라는 레이아웃 변수 추가

         ```kotlin
         <layout ...>
         
             <data>
                 <variable
                     name="viewModel"
                     type="com.example.cupcake.model.OrderViewModel" />
             </data>
         
             <ScrollView ...>
         
             ...
         ```

      2. Fragment 클래스의 `onViewCreated()` 내에서 뷰 모델 인스턴스를 레이아웃의 공유 뷰 모델 인스턴스와 결합하고, 결합 객체에 수명 주기 소유자를 설정한다.

         ```kotlin
         binding?.apply {
             viewModel = sharedViewModel
             lifecycleOwner = viewLifecycleOwner
             ...
         }
         ```

      3. 레이아웃 변수를 활용해 뷰의 속성을 설정한다.

         ex)

         ```kotlin
         <RadioGroup
            ...>
         
            <RadioButton
                android:id="@+id/vanilla"
                ...
                android:checked="@{viewModel.flavor.equals(@string/vanilla)}"
                .../>
         
            <RadioButton
                android:id="@+id/chocolate"
                ...
                android:checked="@{viewModel.flavor.equals(@string/chocolate)}"
                .../>
         
            <RadioButton
                android:id="@+id/red_velvet"
                ...
                android:checked="@{viewModel.flavor.equals(@string/red_velvet)}"
                .../>
         
            <RadioButton
                android:id="@+id/salted_caramel"
                ...
                android:checked="@{viewModel.flavor.equals(@string/salted_caramel)}"
                .../>
         
            <RadioButton
                android:id="@+id/coffee"
                ...
                android:checked="@{viewModel.flavor.equals(@string/coffee)}"
                .../>
         </RadioGroup>
         ```

      4. 리스너 결합을 사용할 수도 있다. 

         리스너 결합은 `onClick` 이벤트와 같은 이벤트가 발생할 때 실행되는 람다 표현식입니다. 리스너 결합은 `textview.setOnClickListener(clickListener)`와 같은 메서드 참조와 비슷하지만, 리스너 결합을 사용하면 임의의 데이터 결합 표현식을 실행할 수 있습니다.

         ```kotlin
         <RadioGroup
            ...>
         
            <RadioButton
                android:id="@+id/vanilla"
                ...
                android:onClick="@{() -> viewModel.setFlavor(@string/vanilla)}"
                .../>
         
         ...
         
         </RadioGroup>
         ```

      5. LiveData를 관찰하도록 수명 주기 소유자 설정

         Fragment 클래스의 `onViewCreated()` 내에서 뷰 모델 인스턴스를 레이아웃의 공유 뷰 모델 인스턴스와 결합한다.

         ```kotlin
         binding?.apply {
             lifecycleOwner = viewLifecycleOwner
             ...
         }
         ```

      6. 리스너 결합을 사용하여 클릭 리스너 설정 

         1. 프래그먼트에 각 프래그먼트에 해당하는 데이터 변수를 추가. 

            ```kotlin
            <layout ...>
            
                <data>
                    <variable
                        name="startFragment"
                        type="com.example.cupcake.StartFragment" />
                </data>
                ...
                <ScrollView ...>
            ```

         2. 프래그먼트의 `onViewCreated()` 메서드에서 새 데이터 변수를 프래그먼트 인스턴스에 결합합니다. `this` 키워드를 사용하여 프래그먼트 내에서 프래그먼트 인스턴스에 액세스할 수 있습니다.

            ```kotlin
            override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
                super.onViewCreated(view, savedInstanceState)
                binding?.startFragment = this
            }
            ```

         3. 프래그먼트의 xml 파일에서 리스너 결합을 사용하여 이벤트 리스너를 버튼의 `onClick` 속성에 추가하고, 프래그먼트의 메서드를 호출하여 원하는 작업을 실행한다. 

            ```kotlin
            <Button
                android:id="@+id/order_one_cupcake"
                android:onClick="@{() -> startFragment.orderCupcake(1)}"
                ... />
            ```

            



































------

### 참고

#### 📌 onViewCreated 

onCreateView() 의 반환값으로 정상적인 Fragment View 객체를 제공했을 때만 Fragment View 의 Lifecycle 이 생성됩니다. nCreateView() 를 통해 반환된 View 객체는 onViewCreated() 의 파라미터로 전달되는데, 이 시점부터는 Fragment View 의 Lifecycle 이 INITIALIZED 상태로 업데이트 됐기 때문에 **View 의 초기값을 설정해주거나 LiveData 옵저빙, RecyclerView 또는 ViewPager2 에 사용될 Adapter 세팅 등은 onViewCreated() 에서 해주는 것이 적절하겠습니다.**



#### 📌 람다

`val multi: (Int, Int) -> Int = {x:Int, y:Int -> x * y}`

+ 람다 값 : {x:Int, y:Int -> x * y}

+ 람다의 자료형 : (Int, Int) -> Int
+ 람다의 인자의 자료형 : (Int, Int)
+ 람다의 반환값의 자료형 : Int





#### 📌 

