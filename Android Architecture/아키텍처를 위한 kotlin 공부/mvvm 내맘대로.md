

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

   