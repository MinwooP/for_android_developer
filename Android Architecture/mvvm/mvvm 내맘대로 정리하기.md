### ๐ ViewModel์ ๋ฐ์ดํฐ ์ ์ฅํ๊ธฐ

1.  ViewModel class ์ถ๊ฐ

   ```kotlin
   class GameViewModel : ViewModel() {
   }
   ```

2. `ViewModel`์ ํ๋๊ทธ๋จผํธ์ ์ฐ๊ฒฐํ๊ธฐ

   + ViewModel์ ์ฌ์ฉํ  View(Activity, Fragment) ๋ด์ viewModel์ ๊ดํ ์ฐธ์กฐ(๊ฐ์ฒด)๋ฅผ ๋ง๋ ๋ค. 

   ```kotlin
   private val viewModel: GameViewModel by viewModels()
   ```

   => ์ฝํ๋ฆฐ์ ํ๋กํผํฐ ์์์ ์ด์ฉํด ์ค๋ชํ๋ฉด `GameViewModel` type์ ๋ณ์์ธ `viewModel`์ ๊ฐ์ ์ฝ๊ณ  ์ธ ๋, ์์๋ฐ์ `viewModels`๊ฐ ๋์  ๊ฐ์ ์ฝ๊ณ  ์ด๋ค. 
   
3. ViewModel๋ก ๋ฐ์ดํฐ ์ด๋ํ๊ธฐ

   `GameFragment` ํด๋์ค์์ `GameViewModel` ํด๋์ค๋ก ๋ฐ์ดํฐ ๋ณ์๋ฅผ ์ด๋ํ๋ค.

   ```kotlin
   class GameViewModel : ViewModel() {
   
       private var score = 0
       private var currentWordCount = 0
       private var currentScrambledWord = "test"
   }
   ```

   ๋ช๋ช ํ๋กํผํฐ์ backing property ์ถ๊ฐ

   ```kotlin
   private var _currentScrambledWord = "test"
   val currentScrambledWord: String
      get() = _currentScrambledWord
   ```

4. ViewModel ์ฑ์ฐ๊ธฐ

   ViewModel ํด๋์ค ๋ด์ ํ๋กํผํฐ๋ค์ ๊ฐ์ง๊ณ  ์์ํ๋ ๋ฉ์๋๋ฅผ ์ถ๊ฐํ  ์ ์๋ค. 

   ```kotlin
   class GameViewModel : ViewModel() { 
       private var wordsList: MutableList<String> = mutableListOf()
      	private lateinit var currentWord: String
       
       private fun getNextWord() {
      		currentWord = allWordsList.random()
   	}
   }
   ```
   
   ์๋ฒ ํต์ ํ๋ ์ฝ๋๋ ์ถ๊ฐํ  ์ ์๋ค.
   
   ```kotlin
   class SignInViewModel : ViewModel() {
       val loginStatus = MutableLiveData(false)
       val email = MutableLiveData("")
       val password = MutableLiveData("")
   
       fun login() {
           viewModelScope.launch {
               try {
                   val code = SampleCreator.sampleService.requestLogIn(
                       SignInRequest(
                           email.value.toString(),
                           password.value.toString()
                       )
                   ).message
                   Log.d("1LogIn test Log", code.toString())
   
                   loginStatus.postValue(true)
               } catch (e: Exception) {
                   Log.d("2LogIn test Log",e.toString())
               }
           }
       }
   }
   ```
   
   <br><br>


### ๐ ViewModel๊ณผ ํจ๊ป LiveData ์ฌ์ฉ

ViewModel๋ด์ ๋ฐ์ดํฐ๋ฅผ **LiveData๋ก ๋ณํ**ํ๊ณ (LiveData๋ก ๋ฐ์ดํฐ๋ฅผ ๋ํ) ์ด **LiveData ๊ฐ์ฒด์ ๊ด์ฐฐ์๋ฅผ ์ถ๊ฐ**ํ๊ณ  LiveData๋ฅผ ๊ด์ฐฐ

1. ViewModel ๋ด data์ type์ LiveData or MutableLiveData๋ก ๋ฐ๊พผ๋ค. 

   + `GameViewModel`์์ ๋ณ์ `_currentScrambledWord`์ ์ ํ์ `MutableLiveData<String>`์ผ๋ก ๋ณ๊ฒฝ

   + `LiveData`/`MutableLiveData` ๊ฐ์ฒด์ ๊ฐ์ ๋์ผํ๊ฒ ์ ์ง๋๊ณ  ์ด ๊ฐ์ฒด์ ์ ์ฅ๋ ๋ฐ์ดํฐ๋ง ๋ณ๊ฒฝ๋๊ธฐ ๋๋ฌธ์ `_currentScrambledWord`์ ๋ณ์ ์ ํ์ `val`๋ก ๋ณ๊ฒฝํฉ๋๋ค. 

     ```kotlin
     private val _currentScrambledWord = MutableLiveData<String>()
     val currentScrambledWord: LiveData<String>
        get() = _currentScrambledWord
     ```

   + `LiveData` ๊ฐ์ฒด ๋ด์ ๋ฐ์ดํฐ์ ์ก์ธ์คํ๋ ค๋ฉด `value` ์์ฑ์ ์ฌ์ฉํ๋ค.

2. LiveData ๊ฐ์ฒด์ ๊ด์ฐฐ์ ์ฐ๊ฒฐํ๊ธฐ

   + LiveData๊ฐ ์ฐ์ด๋ Activity๋ Fragment์`LiveData`์ ๊ด์ฐฐ์๋ฅผ ์ฐ๊ฒฐํ๋ค. `observe()` ๋ฉ์๋๋ฅผ ํธ์ถํ๊ณ , ์ธ์๋ก **1. viewLifecycleOwner**์ **2. data๊ฐ์ด ๋ณ๊ฒฝ๋๋ฉด ํ  ํ๋**์ ๋ํ๋ด๋ ๋๋ค๋ฅผ ์ ๋ฌํ๋ค.  

     + `GameFragment`์ `onViewCreated()` ์ฝ๋ฐฑ ๋์์ `currentScrambledWord`์ ๊ดํด `observe()` ๋ฉ์๋๋ฅผ ํธ์ถํ๋ค. 

       ```kotlin
       // Observe the scrambledCharArray LiveData, passing in the LifecycleOwner and the observer.
       viewModel.currentScrambledWord.observe(viewLifecycleOwner,
          { newWord ->
             binding.textViewUnscrambledWord.text = newWord
          })
       ```

       > ์ฒซ๋ฒ์งธ ๋งค๊ฐ๋ณ์๋ก ์ ๋ฌ๋๋ `viewLifeCycleOwner`๋ `LiveData`๊ฐ `GameFragment`์ ์๋ช ์ฃผ๊ธฐ๋ฅผ ์ธ์ํ๊ณ , `GameFragmet`๊ฐ ํ์ฑ ์ํ(`Started` ๋๋ `Resumed`)์ผ ๋๋ง ๊ด์ฐฐ์์ ์๋ฆด ์ ์๋๋ก ํ๋ค. 

       + ์ด์  `currentScrambledWord`์ ๊ฐ์ด ๋ฐ๋๋ฉด ์๋์ผ๋ก `textViewUnscrambledWord`์ `text`๊ฐ ์๋ฐ์ดํธ ๋จ.

       => ์ด๋ ๊ฒ LiveData์์๋ observe ํจ์๋ฅผ ํตํด ๊ด์ฐฐ์๋ฅผ ์ค์ ํ์ฌ, LiveData์ ๊ฐ์ด ๋ฐ๋ ๋๋ง๋ค observe ๋ด์ ์ ์ธ๋ ๋๋ค๋ฅผ ํตํด layout view์ ๋ฐ์ดํฐ๋ฅผ ์๋ฐ์ดํธ ํด์ค ์ ์๋ค.   

       => โ ํ์ง๋ง dataBinding์ ํจ๊ป ์ฌ์ฉํ๋๋ผ๋ ํ์ค์ ์ผ๋ก observe๋ฅผ ์ฌ์ฉํด์ผ ํ๋ ๋ถ๋ถ์ด ๋ง๋ค ??

<br><br>

### ๐ Data binding๊ณผ ํจ๊ป LiveData ์ฌ์ฉํ๊ธฐ

1. ์ฌ์  ์ธํ

2. ๋ ์ด์์ ํ์ผ ํ๊ทธ๋ก ๊ฐ์ธ๊ธฐ

   ```xml
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

3. `GameFragment`์ `onViewCreated()` ๋ฉ์๋ ์์ ๋ถ๋ถ์์ ๋ ์ด์์ ๋ณ์ `gameViewModel` ๋ฐ `maxNoOfWords`๋ฅผ ์ด๊ธฐํํฉ๋๋ค.

   ```kotlin
   override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
      super.onViewCreated(view, savedInstanceState)
   
      binding.gameViewModel = viewModel
   
      binding.maxNoOfWords = MAX_NO_OF_WORDS
   ...
   }
   ```

4. ๋ ์ด์์์ ์๋ช ์ฃผ๊ธฐ ์์ ์๋ฅผ ์ ๋ฌํด์ผ ํฉ๋๋ค.

   ```kotlin
   binding.lifecycleOwner = viewLifecycleOwner
   ```

5. ๋ ์ด์์์ ๊ฒฐํฉ ํํ์ ์ฌ์ฉ

   ```kotlin
   <TextView
      android:id="@+id/textView_unscrambled_word"
      ...
      android:text="@{gameViewModel.currentScrambledWord}"
      .../>
   ```

   + `GameFragment`์์ `currentScrambledWord`์ `LiveData` ๊ด์ฐฐ์ ์ฝ๋๋ฅผ ์ญ์ ํฉ๋๋ค. ํ๋๊ทธ๋จผํธ์ ๋ ์ด์ ๊ด์ฐฐ์ ์ฝ๋๊ฐ ํ์ํ์ง ์์ต๋๋ค. `LiveData` ๋ณ๊ฒฝ์ฌํญ ์๋ฐ์ดํธ๊ฐ ๋ ์ด์์์ ์ง์  ์์ ๋ฉ๋๋ค.
   + โ ์ด๋ ๊ฒ ๋ ์ด์์ xml ํ์ผ์ ๋ทฐ์ ์ง์  ์์ฑ์ผ๋ก liveData๋ฅผ ์ฐ๊ฒฐ(๋ฐ์ธ๋ฉ) ํ์ ๋๋ง, `observe` ์์ด layout UI์ ์๋์ผ๋ก ์๋ฐ์ดํธ ? 

<br>

-----

### ๐ Shared ViewModel

์์ง๊น์ง๋ ํ Activity์ ๊ทธ Activity์์ ์ฌ์ฉํ๋ data๋ค์ด ๋ณ์๋ก ๋ค ์ ์ธ๋์ด ์๊ณ , ๋ค๋ฅธ Activity๋ก ์ด๋ํ  ๋ ๋ง๋ค ํ์ํ data๋ค์ ๋๊ฒจ์คฌ์์. ์ด์ ๋ Shared ViewModel์ ์ด์ฉํ์ฌ ์ด๋ฅผ ์๋ก ๊ณต์ 

<br>

Shared ViewModel์ ์ฌ์ฉํ์ฌ ์ฑ์ ๋ฐ์ดํฐ๋ฅผ ๋จ์ผ ViewModel์ ์ ์ฅํ๋ค. ์ฑ์ ์ฌ๋ฌ ํ๋๊ทธ๋จผํธ๋ activity scope๋ฅผ ์ฌ์ฉํ์ฌ ๊ณต์  ViewModel์ ์ ๊ทผํ๋ค.

์ฌ์ฉ์๋ ์ฒซ ๋ฒ์งธ ํ๋ฉด์์ ์ปต์ผ์ดํฌ์ ์๋์ ์ ํํฉ๋๋ค. ๊ทธ๋ฌ๋ฉด ๋ ๋ฒ์งธ ํ๋ฉด์ ๊ฐ๊ฒฉ์ด ์ปต์ผ์ดํฌ์ ์๋์ ๋ฐ๋ผ ๊ณ์ฐ๋์ด ํ์๋ฉ๋๋ค. ๋ง์ฐฌ๊ฐ์ง๋ก ๋ง ๋ฐ ์๋ น ๋ ์ง์ ๊ฐ์ ๋ค๋ฅธ ์ฑ ๋ฐ์ดํฐ๋ ์์ฝ ํ๋ฉด์์๋ ์ฌ์ฉ๋ฉ๋๋ค.

<br>

**๊ณต์  ๋ทฐ๋ชจ๋ธ์ ๊ตฌํํ๋ ๋ฐฉ๋ฒ**

1. ํ๋ก์ ํธ์์ `model`์ด๋ผ๋ ์ ํจํค์ง๋ฅผ ๋ง๋ค๊ณ  `OrderViewModel` ํด๋์ค๋ฅผ ์ถ๊ฐํ๋ค. ๊ทธ๋ฌ๋ฉด ๋๋จธ์ง UI ์ฝ๋์์ ๋ทฐ ๋ชจ๋ธ ์ฝ๋๊ฐ ๋ถ๋ฆฌ๋๋ค. 

2. ViewModel ํด๋์ค๋ฅผ ๋ง๋ค๊ณ , LiveData๋ฅผ ์ถ๊ฐํ๊ณ , ์ด์ ๊ด๋ จ๋ ๋ฉ์๋๋ฅผ ์ ์ํ๋ค.

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

3. ViewModel์ ์ฌ์ฉํ๋๋ก Fragment ์๋ฐ์ดํธ

   1. `StartFragment` ํด๋์ค์์ ๊ณต์  ๋ทฐ ๋ชจ๋ธ์ ์ฐธ์กฐ๋ฅผ ํด๋์ค ๋ณ์๋ก ๊ฐ์ ธ์ต๋๋ค. `fragment-ktx` ๋ผ์ด๋ธ๋ฌ๋ฆฌ์ `by activityViewModels()` Kotlin ์์ฑ ์์์ ์ฌ์ฉํฉ๋๋ค.

      ```kotlin
      private val sharedViewModel: OrderViewModel by activityViewModels()
      ```

      + `viewModels()`๋ ํ์ฌ ํ๋๊ทธ๋จผํธ๋ก ๋ฒ์๊ฐ ์ง์ ๋ `ViewModel` ์ธ์คํด์ค๋ฅผ ์ ๊ณตํฉ๋๋ค. ๋ฐ๋ผ์ ์ธ์คํด์ค๋ ํ๋๊ทธ๋จผํธ ๋ง๋ค ๋ค๋ฆ๋๋ค.
   
        => โ ๊ทธ๋ฌ๋ฉด, `by viewModels()`๋ก ์์๋ viewModel ๋ณ์๋ฅผ ๊ฐ fragment์์ ์ ์ธํ๋ฉด ๊ฐ fragement์ ์ธ์คํด์ค๋ ๋ค๋ฅด๋๊น ๊ทธ๋ฅ ๊ป์ง, ํ๋ง ๊ณต์ ํ๊ฒ ๋๋๊ฑด๊ฐ ? ํด๋์ค์ ๊ฐ ์ธ์คํด์ค๊ฐ ์๋ก ๋ค๋ฅธ ๊ฒ์ฒ๋ผ 
   
      + `activityViewModels()`๋ ํ์ฌ Activity๋ก ๋ฒ์๊ฐ ์ง์ ๋ `ViewModel` ์ธ์คํด์ค๋ฅผ ์ ๊ณตํฉ๋๋ค. ๋ฐ๋ผ์ ์ธ์คํด์ค๋ ๋์ผํ ํ๋์ ์ฌ๋ฌ ํ๋๊ทธ๋จผํธ ๊ฐ์ ๋์ผํ๊ฒ ์ ์ง๋ฉ๋๋ค.
   
        => โ ํ์ฌ ์ด fragment๊ฐ ์์ฃผํด์๋ Activity์ ๋ผ์ดํ์ฌ์ดํด์ ๊ฐ์ดํ๋ viewModel์ ์์ฑํ๋ ๊ฑด๊ฐ? 
   
   2. ViewModel์ ์ฌ์ฉํ๋ ๊ฐ Fragment์์ 1๋ฒ ๋จ๊ณ๋ฅผ ๋ฐ๋ณตํ๋ค. 
   
   3. ๊ฐ ํ๋๊ทธ๋จผํธ์์ ViewModel์ ๋ฉ์๋๋ฅผ ์ฌ์ฉํ์ฌ live data์ ๊ฐ์ ๋ณ๊ฒฝํ  ์ ์๋ค. 
   
      ```kotlin
      fun orderCupcake(quantity: Int) {
          sharedViewModel.setQuantity(quantity)
          findNavController().navigate(R.id.action_startFragment_to_flavorFragment)
      }
      ```
   
      + StartFragment์์ ์ด๋ค ๋ฒํผ์ ํด๋ฆญํ์ ๋, ์ฐธ์กฐํ๊ณ  ์๋ ๋ทฐ ๋ชจ๋ธ์ ๋ฉ์๋์ธ sharedViewModel.setQuantity๋ฅผ ์ฌ์ฉํด quantity์ ๊ฐ์ ์๋ฐ์ดํธ ํ๋ค. 
   
   4. ๋ฐ์ดํฐ ๋ฐ์ธ๋ฉ๊ณผ ํจ๊ป ๊ณต์  ๋ทฐ ๋ชจ๋ธ ์ฌ์ฉ
   
      1. ๋ฐ์ดํฐ ๋ฐ์ธ๋ฉ์ผ๋ก Fragment์ ๋ ์ด์์์ ๋ฐ๊พธ๊ณ , viewModel์ด๋ผ๋ ๋ ์ด์์ ๋ณ์ ์ถ๊ฐ
   
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
   
      2. Fragment ํด๋์ค์ `onViewCreated()` ๋ด์์ ๋ทฐ ๋ชจ๋ธ ์ธ์คํด์ค๋ฅผ ๋ ์ด์์์ ๊ณต์  ๋ทฐ ๋ชจ๋ธ ์ธ์คํด์ค์ ๊ฒฐํฉํ๊ณ , ๊ฒฐํฉ ๊ฐ์ฒด์ ์๋ช ์ฃผ๊ธฐ ์์ ์๋ฅผ ์ค์ ํ๋ค.
   
         ```kotlin
         binding?.apply {
             viewModel = sharedViewModel
             lifecycleOwner = viewLifecycleOwner
             ...
         }
         ```
   
      3. ๋ ์ด์์ ๋ณ์๋ฅผ ํ์ฉํด ๋ทฐ์ ์์ฑ์ ์ค์ ํ๋ค.
   
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
   
      4. ๋ฆฌ์ค๋ ๊ฒฐํฉ์ ์ฌ์ฉํ  ์๋ ์๋ค. 
   
         ๋ฆฌ์ค๋ ๊ฒฐํฉ์ `onClick` ์ด๋ฒคํธ์ ๊ฐ์ ์ด๋ฒคํธ๊ฐ ๋ฐ์ํ  ๋ ์คํ๋๋ ๋๋ค ํํ์์๋๋ค. ๋ฆฌ์ค๋ ๊ฒฐํฉ์ `textview.setOnClickListener(clickListener)`์ ๊ฐ์ ๋ฉ์๋ ์ฐธ์กฐ์ ๋น์ทํ์ง๋ง, ๋ฆฌ์ค๋ ๊ฒฐํฉ์ ์ฌ์ฉํ๋ฉด ์์์ ๋ฐ์ดํฐ ๊ฒฐํฉ ํํ์์ ์คํํ  ์ ์์ต๋๋ค.
   
         ๐ ์ฌ๊ธฐ์๋ viewModel์ ์ ์๋์ด์๋ ๋ฉ์๋๋ฅผ listener์ ์ค์ 
      
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
   
      5. LiveData๋ฅผ ๊ด์ฐฐํ๋๋ก ์๋ช ์ฃผ๊ธฐ ์์ ์ ์ค์ 
   
         Fragment ํด๋์ค์ `onViewCreated()` ๋ด์์ ๋ทฐ ๋ชจ๋ธ ์ธ์คํด์ค๋ฅผ ๋ ์ด์์์ ๊ณต์  ๋ทฐ ๋ชจ๋ธ ์ธ์คํด์ค์ ๊ฒฐํฉํ๋ค.
      
         ```kotlin
         binding?.apply {
             lifecycleOwner = viewLifecycleOwner
             ...
         }
         ```
   
      6. ๋ฆฌ์ค๋ ๊ฒฐํฉ์ ์ฌ์ฉํ์ฌ ํด๋ฆญ ๋ฆฌ์ค๋ ์ค์  
   
         ๐ ์ฌ๊ธฐ์๋ viewModel์ ์ ์๋์ด์๋ ๋ฉ์๋๊ฐ ์๋๋ผ ํด๋น Fragment์ ์ ์๋์ด์๋ ๋ฉ์๋๋ฅผ listener์ ์ค์ 
      
         1. xmlํ์ผ์ ๊ฐ ํ๋๊ทธ๋จผํธ์ ํด๋นํ๋ ๋ฐ์ดํฐ ๋ณ์๋ฅผ ์ถ๊ฐ. 
         
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
      
         2. ํ๋๊ทธ๋จผํธ์ `onViewCreated()` ๋ฉ์๋์์ ์ ๋ฐ์ดํฐ ๋ณ์๋ฅผ ํ๋๊ทธ๋จผํธ ์ธ์คํด์ค์ ๊ฒฐํฉํฉ๋๋ค. `this` ํค์๋๋ฅผ ์ฌ์ฉํ์ฌ ํ๋๊ทธ๋จผํธ ๋ด์์ ํ๋๊ทธ๋จผํธ ์ธ์คํด์ค์ ์ก์ธ์คํ  ์ ์์ต๋๋ค.
         
            ```kotlin
            override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
                super.onViewCreated(view, savedInstanceState)
                binding?.startFragment = this
            }
            ```
      
         3. ํ๋๊ทธ๋จผํธ์ xml ํ์ผ์์ ๋ฆฌ์ค๋ ๊ฒฐํฉ์ ์ฌ์ฉํ์ฌ ์ด๋ฒคํธ ๋ฆฌ์ค๋๋ฅผ ๋ฒํผ์ `onClick` ์์ฑ์ ์ถ๊ฐํ๊ณ , ํ๋๊ทธ๋จผํธ์ ๋ฉ์๋๋ฅผ ํธ์ถํ์ฌ ์ํ๋ ์์์ ์คํํ๋ค. 
         
            ```kotlin
            <Button
                android:id="@+id/order_one_cupcake"
                android:onClick="@{() -> startFragment.orderCupcake(1)}"
                ... />
            ```

<br><br>

### ๐ mvvm ํด๋๋ง

<img src = "https://user-images.githubusercontent.com/31370590/158093060-260474e8-7e43-4e92-9db2-c3c7c218dbf5.PNG">

+ **data = Model** : ํ๋ก๊ทธ๋จ์ ์ฌ์ฉ๋๋ ์ค์  ๋ฐ์ดํฐ๋ฅผ ๋ด๋นํ๊ธฐ ๋๋ฌธ์, "data"์ ํจํค์ง๋ก ๋ถ๋ฆฌํ์์ต๋๋ค.
  - **model** : ๋ฐ์ดํฐ ํด๋์ค(Entity)๋ค์ ํจํค์ง๋ก์จ, ์ถํ ๋๋ํ์์ ์ ์ธ๋์ด์ผ ํ๋ ๋์์ด๊ธฐ ๋๋ฌธ์, ๋๋ํ์ ํธ์๋ฅผ ์ํด model ํจํค์ง๋ก ๋ฐ๋ก ๋ถ๋ฆฌํ์์ต๋๋ค.
  - **repository** : Local ๋๋ Remote DataSource์ ์ด๋ฌํ ๋ฐ์ดํฐ ์์ค๋ฅผ ์ถ์ํํ๋ Repository ํด๋์ค, ๋คํธ์ํฌ ํต์ (Retrofit ๋ผ์ด๋ธ๋ฌ๋ฆฌ)์ ์ํ Retrofit Service ์ธํฐํ์ด์ค๊ฐ ์์ต๋๋ค.
+ **presentation = View, ViewModel** : ํ๋ฉด์ ํํํ๋ UI๋ฅผ ๋ด๋นํ๋ View์ ViewModel ์ด๊ธฐ ๋๋ฌธ์, "presentation"์ํจํค์ง๋ก ๋ถ๋ฆฌํ์์ต๋๋ค. 
  - **View** : ํ๋ฉด์ ๋ด๋นํ๋, Activity, Fragment, CustomView ๋ฑ๋ฑ... ์ ํด๋นํฉ๋๋ค.
  - **ViewModel** : View์ ์ด๋ฒคํธ๋ฅผ ๋ฐ์, Model์์ ํ์ํ ๋ฐ์ดํฐ๋ฅผ ๊ฐ์ ธ์์ View์์ ์ํ๋ ๋ฐ์ดํฐ๋ก ๊ฐ๊ณตํ๋ ์ญํ ์ ํ๋ ํด๋์ค์๋๋ค.

<br><br>

### ๐ ๋ ํฌ์งํ ๋ฆฌ ํจํด

**๋ ํฌ์งํ ๋ฆฌ ํจํด์ด๋ ?**

+ ๋ฐ์ดํฐ ์ถ์ฒ(๋ก์ปฌDB์ธ์ง, API ์๋ต์ธ์ง ๋ฑ)๊ณผ ๊ด๊ณ ์์ด ๋์ผ ์ธํฐํ์ด์ค๋ก ๋ฐ์ดํฐ์ ์ ์ํ  ์ ์๋๋ก ๋ง๋๋ ๊ฒ

+ ๋ ํฌ์งํ ๋ฆฌ๋ **๋ฐ์ดํฐ ์์ค์ ์ก์ธ์คํ๋ ๋ฐ ํ์ํ ๋ผ๋ฆฌ๋ฅผ ์บก์ํ**ํ๋ ํด๋์ค ๋๋ ๊ตฌ์ฑ ์์์ด๋ค. ์ฆ, ๋ฐ์ดํฐ ๊ทธ ์์ฒด์ธ data source ์ ๋ฐ์ดํฐ๊ด๋ จ ๋ก์ง์ ์์ ํ ๋ถ๋ฆฌํ๋ ๊ธฐ๋ฒ์ด๋ผ๊ณ  ํ  ์ ์๋ค.

  Repository (๋ฐ์ดํฐ ๊ด๋ จ ๋ก์ง)  => Data source(์ค์  data)

  ์ฆ, Repository๋ Datasource๋ฅผ ์บก์ํํ๋ค.

<br>

##### ๋ ํฌ์งํ ๋ฆฌ ํจํด์ ์ฌ์ฉํ๋ ์ด์ 

- ๋ฐ์ดํฐ ๋ก์ง์ ๋ถ๋ฆฌ์ํฌ ์ ์๋ค.
- ์ค์ ์ง์ค์ฒ๋ฆฌ ๋ฐฉ์์ผ๋ก, ์ธ์ ๋ ์ผ๊ด๋ ์ธํฐํ์ด์ค๋ก ๋ฐ์ดํฐ๋ฅผ ์์ฒญํ  ์ ์๋ค.
- ๊ทธ๋ ๊ธฐ ๋๋ฌธ์, ํด๋ผ์ด์ธํธ๊ฐ ์ด๋ค ๋ฐ์ดํฐ๋ฅผ ์ฌ์ฉํ ์ง ์ ํํ  ํ์ ์์ด, **์ด๋ค ๋ฐ์ดํฐ๋ฅผ ๊ฐ์ ธ์ฌ์ง๋ Repository์์ ๊ฒฐ์ **ํ์ฌ ์ ์ ํ ๋ฐ์ดํฐ๋ฅผ ์ ๊ณตํ๋ค.
- ๋จ์ ํ์คํธ๋ฅผ ํตํด ๊ฒ์ฆ์ด ๊ฐ๋ฅํด์ง๋๋ค.
- ์๋ก์ด ๋ฐ์ดํฐ ๋ก์ง ์ฝ๋๋ฅผ ์ฝ๊ฒ ์ถ๊ฐํ  ์ ์์ต๋๋ค.

<br>

##### **Repository ํจํด์ ์ด์ **

+ ํ๋์ ๋๋ฉ์ธ์ ํํํ๋๋ฐ ํ์ํ DataSource๊ฐ ๋ช ๊ฐ ์ด๋์ง client์ชฝ์์๋ ์ด๋ฅผ ์ ํ์๊ฐ ์๋ค. ๋ฐ๋ผ์ DataSource๊ฐ ์๋กญ๊ฒ ์ถ๊ฐ๋๋ ๊ฒ์ ๋ํ ๋ถ๋ด์ด ์๋ค.

+ DataSource์ ๋ณ๊ฒฝ์ด ๋ฐ์ํ๋๋ผ๋ repository ์ธ๋ถ layer๋ก ์ ํ๋์ง ์๋๋ค.

+ client๋ repository ์ธํฐํ์ด์ค์ ์์กดํ๊ธฐ ๋๋ฌธ์ ํ์คํธํ๊ธฐ ์ฉ์ดํ๋ค.

+ ๊ฒฐ๊ตญ respository๋ presentation layer์ data layer ์ Coupling(๊ฒฐํฉ๋)๋ฅผ ๋์จํ๊ฒ ๋ง๋ค์ด์ค๋ค. ์ค๊ฐ์ ์ถ์ํ๋ ๋ ์ด์ด๋ก์ Repository ํด๋์ค๋ฅผ ๋์ด ๋ชจ๋ํ๊ฐ ๋ชํํด์ง๊ณ , ์ ์ง๋ณด์์ฑ์ด ํฅ์๋๋ค.

<br>

##### **์๋๋ก์ด๋์์์ Repository ํจํด**

View -> Presenter / Viewmodel -> Repository -> DataSource(API, LocalDB)

+ Repository๋ ViewModel or Presenter๊ฐ ์์ฒญํ๋ ๋ฐ์ดํฐ๋ฅผ ๋ก์ปฌDB(Room) ๋๋ ์๋ฒ(Retrofit)๋ก๋ถํฐ ๊ฐ์ ธ์ ์ ๋ฌํด์ค๋ค. ์ด๋ฅผ ํตํด ViewModel์ ๋๊ตฌํํ ๊ฐ์ ธ์จ ๋ฐ์ดํฐ์ธ์ง(Local DB์ธ์ง, ์๋ฒ์ธ์ง)์ ๋ํด ์ ๊ฒฝ์ธ ํ์๊ฐ ์์ด์ง๋ค.

  ์ฆ, **ViewModel์ ์์ ์ ๋น์ฆ๋์ค ๋ก์ง์๋ง ์ง์ค**ํ๋ฉด ๋๋ค.

  Relam์ธ์ง, Room์ธ์ง, Retrofit์ ํตํ http์๋น์ค๋ฅผ ํตํด์์ธ์ง, SharedPrference์ธ์ง ๋ฑ ๋ฐ์ดํฐ์ ์ถ์ฒ๋ฅผ ViewModel์ ์ ํ ์ ๊ฒฝ์ฐ์ง ์์๋ ๋๋ค. Repository๊ฐ ์ฒ๋ฆฌํด์ฃผ๊ธฐ ๋๋ฌธ์ด๋ค.

  repository ๋ Presenter ๊ณ์ธต๊ณผ data ๊ณ์ธต์ coupling ์ ๋์จํ๊ฒ ๋ง๋ค์ด์ค๋ค.

<br>
