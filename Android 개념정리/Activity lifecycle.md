## 🎖 Activity lifecycle

+ *activity lifecycle*은 activity의 전체 기간 중 일련의 activity 상태입니다. 수명 주기는 활동이 생성되는 시점에 시작하여 활동이 소멸되어 시스템에서 활동 리소스가 회수될 때까지 이어집니다. 사용자는 앱에서 activity 간에 이동하므로(앱 안팎으로) 이러한 활동은 각각 활동 수명 주기의 다양한 상태로 전환됩니다. 

+ `Activity` 클래스 자체와 `Activity`의 모든 서브클래스(예: `AppCompatActivity`)는 **일련의 수명 주기 콜백 메서드**를 구현합니다. android에서는 **activity가 한 상태에서 다른 상태로 이동할 때 이러한 콜백을 호출**하고 개발자는 이러한 메서드를 **자체 activity에서 재정의**하여 **수명 주기 상태 변경에 응답해 작업을 실행**할 수 있습니다. 다음 다이어그램은 사용할 수 있는 재정의 가능한 완료할 함께 수명 주기 상태를 보여줍니다.

  <img src = "https://user-images.githubusercontent.com/31370590/126263442-98e495ee-9610-4cfd-b41b-4f107b362c8e.PNG" width = "300" height = "400">

  이러한 콜백이 호출되는 시점과 각 콜백 메서드에서 할 작업을 알아야 한다.



### Callback method

#### 1. onCreate()

+ `onCreate()` 메서드에서 Activity의 일회성 초기화를 실행해야 합니다. 예를 들어 `onCreate()`에서 **레이아웃을 확장**하거나 **클릭 리스너를 정의**하거나 **뷰 결합을 설정**합니다.

+ `onCreate()` 메서드는 Activity가 초기화된 직후(새 `Activity` 객체가 메모리에 만들어질 때) 한 번 호출됩니다. `onCreate()`가 실행되면 Activity가 *생성됨*으로 간주됩니다.

  > `onCreate()` 메서드를 재정의할 때 슈퍼클래스 구현을 호출하여 Activity 생성을 완료해야 하므로 Activity 내에서 `super.onCreate()`를 즉시 호출해야 합니다. 다른 수명 주기 콜백 메서드의 경우에도 마찬가지입니다.

+ `onCreate()` 메서드는 중요한 단계입니다. 여기서 첫 초기화가 모두 이루어지고 레이아웃을 확장하여 처음으로 레이아웃을 설정하며 변수를 초기화합니다.

+ log 

  `onCreate()` method에 log 코드 추가

  ```Log.d("MainActivity", "onCreate Called")
  Log.d("MainActivity", "onCreate Called")
  ```

  `Log`클래스는 **Logcat**에 메시지를 씁니다. **Logcat**은 메시지를 기록하는 콘솔입니다. `Log.d()` 메서드나 기타 `Log` 클래스 메서드를 사용하여 로그에 명시적으로 전송하는 메시지를 비롯하여 앱에 관한 Android의 메시지가 여기에 표시됩니다.

<br>

#### 2. onStart()

+ `onStart()` 수명 주기 메서드는 `onCreate()` 직후에 호출됩니다. `onStart()`가 실행되면 **활동이 화면에 표시**됩니다. 활동을 초기화하는 데 한 번만 호출되는 `onCreate()`와 달리 `onStart()`는 **활동의 수명 주기에서 여러 번 호출**될 수 있습니다.

+ `onStart()`는 상응하는 `onStop()` 수명 주기 메서드와 페어링됩니다. 사용자가 앱을 시작한 후 기기 홈 화면으로 돌아오면 활동이 중지되고 더 이상 화면에 표시되지 않습니다.

  ```kotlin
  override fun onStart() {
     super.onStart()
     Log.d(TAG, "onStart Called") // 기본 로깅 설정 => 수명 주기 콜백이 트리거되는 방식 탐색 가능
  }
  ```

<br>

#### 3. onRestart()

+ `onCreate()`나 `onRestart()`는 활동이 표시되기 전에 호출됩니다. `onCreate()` 메서드는 처음에만 호출되고 `onRestart()`는 그 후에 호출됩니다. `onRestart()` 메서드는 **활동이 처음으로 시작되지 않은 경우에만 호출하려는 코드를 배치하는 위치**입니다.

<br><br>

#### acitivity lifecycle 사용 사례 1 : **활동 열기 및 닫기**

1. 앱이 처음 시작되면 `onCreate()`, `onStart()`, `onResume()` 콜백이 호출됩니다
   + `onCreate()` - 앱을 만듭니다.
   + `onStart()` - 활동을 시작하고 화면에 표시되게 합니다.
   + `onResume()` - 활동 포커스를 제공하고 사용자가 상호작용할 수 있도록 활동을 준비합니다.

<br>

2. 컵케이크를 몇 번 탭합니다.

3. 기기에서 **뒤로** 버튼을 탭합니다. Logcat에서 `onPause()`, `onStop()`, `onDestroy()`가 순서대로 호출됩니다.

   이 경우 **뒤로** 버튼을 사용하면 활동 및 앱이 완전히 닫힙니다. **`onDestroy()` 메서드의 실행은 활동이 완전히 종료되었으며 가비지 컬렉션될 수 있음을 의미**합니다. 가비지 컬렉션은 더 이상 사용하지 않을 객체의 자동 정리를 나타냅니다. 

   > 여기서 요점은 `onCreate()`와 `onDestroy()`가 단일 활동 인스턴스의 전체 기간에 한 번만 호출된다는 것입니다. `onCreate()`는 앱을 맨 처음 초기화할 때, `onDestroy()`는 앱에서 사용하는 리소스를 정리할 때 호출됩니다.

   > #### 안드로이드 가비지 콜렉터
   >
   > 모든 어플리케이션은 작업을 하는데 필요한 메모리가 필요한데 가비지 콜렉터가 이에 대한 메모리를 확보를 해줍니다. Android 의 경우 런타임에서 메모리가 부족한 경우에 가비지 콜렉터를 트리거해서 어플리케이션을 원활히 동작할 메모리를 다시 확보를 해줍니다.
   >
   > 가비지 콜렉터의 수집은 3단계로 진행이 됩니다.
   >
   > 1) 메모리에 있는 모든 객체 참조를 나열 해서 참조가 있는 활성객체를 표시 
   >
   > 2) 1)에서 표시가 되지 않는 객체들을 메모리에서 제거 
   >
   > 3) 살아있는 객체를 재 정렬
   >
   > 가비지 콜렉터는 이런식으로 수집해서 메모리를 확보해줍니다.

<br>

#### acitivity lifecycle 사용 사례 2 : 활동에서 이동 및 활동으로 다시 이동

+ 활동은 사용자가 활동에서 벗어날 때마다 완전히 닫히지 않습니다.
  + 활동이 화면에 더 이상 표시되지 않으면 이는 활동이 ***background*에 배치되는 것**입니다. 이와 반대의 경우는 활동이 *foreground*에 있거나 화면에 표시되는 것입니다.
  + 사용자가 앱으로 돌아오면 동일한 활동이 다시 시작되어 화면에 다시 표시됩니다. 수명 주기에서 이 부분을 앱의 *visible* life cycle라고 합니다. 
  + 앱은 백그라운드에 있을 때 시스템 리소스와 배터리 수명을 보존하기 위해 일반적으로 활발히 실행되지 않아야 합니다. `Activity` 수명 주기와 그 콜백을 사용하여 앱이 백그라운드로 이동하는 시점을 알 수 있어 진행 중인 작업을 일시중지할 수 있습니다. 그런 다음 앱이 포그라운드로 전환될 때 작업을 다시 시작합니다.

<br>

1. 앱이 처음 시작되면 `onCreate()`, `onStart()`,`onResume()` 콜백이 호출됩니다

2. 컵케이크를 몇 번 탭합니다.

3. 기기에서 **홈** 버튼을 누르고 Android 스튜디오에서 Logcat을 관찰합니다. **홈 화면으로 돌아오면 앱이 완전히 종료되는 대신 백그라운드로 전환**됩니다. `onPause()` 메서드와 `onStop()` 메서드가 호출되지만 `onDestroy()`는 호출되지 않습니다. 

   + `onPause()`가 호출되면 앱에 더 이상 포커스가 없습니다.
   + `onStop()` 이후에는 앱이 더 이상 화면에 표시되지 않습니다.
   + 활동이 중지되었지만 `Activity` 객체는 여전히 백그라운드에서 메모리에 있습니다. 활동은 소멸되지 않았습니다. 사용자가 앱으로 돌아올 수 있으므로 Android는 활동 리소스를 유지합니다. 

4. 최근 화면을 사용하여 앱으로 돌아갑니다. Logcat에서 활동은 `onRestart()`와 `onStart()`로 다시 시작된 후 `onResume()`으로 재개됩니다.

   + 활동이 포그라운드로 돌아오면 `onCreate()` 메서드가 다시 호출되지 않습니다. 활동 객체는 소멸되지 않았으므로 다시 만들지 않아도 됩니다. `onCreate()` 대신 `onRestart()` 메서드가 호출됩니다. 이번에는 활동이 포그라운드로 돌아올 때 **Desserts Sold** 수가 유지됩니다.

   > 여기서 핵심은 `onStart()`와 `onStop()`이 사용자가 활동에서 나가거나 활동으로 이동할 때 여러 번 호출된다는 점입니다.

<br>

#### acitivity lifecycle 사용 사례 3 : 부분적으로 활동 숨기기

+ `onCreate()` => 앱 시작
+ `onStart()`  => 앱이 화면에 표시
+ `onResume()` => 앱이 사용자 포커스 확보 : 즉 사용자가 앱과 상호작용 할 수 있음

+ 앱이 백그라운드로 이동하면
+ `onPause()` => 포커스 상실
+ `onStop()` => 앱 표시 x

<br>

+ 포커스와 가시성의 차이가 중요한 이유는 활동이 화면에 ***부분적으로*** 표시되지만 사용자 포커스는 없을 수 있기 때문. 

  ex) 오른쪽 상단의 공유 버튼을 누르면, **기존 activity는 계속 화면 위쪽 절반에 표시되므로 포커스는 상실했지만, 앱은 계속 표시되는 것이므로 `onPause()`만 호출**되고, `onStop()`은 호출되지 않는다. 포커스를 상실했으므로 사용자가 상호작용 할 수 없다. 포그라운드에 있는 '공유' activity에 사용자 포커스가 있다.

 <br>

#### configuration changes

+ **화면 가로모드로 전환 시, 시스템은 모든 수명 주기 콜백을 호출하여 활동을 종료합니다. 그런 다음 활동이 다시 만들어질 때 시스템은 모든 수명 주기 콜백을 호출하여 활동을 시작합니다.**
+ 기기가 회전되어 활동이 종료되고 다시 만들어지면 활동은 기본값(판매된 디저트 수와 수익이 0으로 재설정됨)으로 시작됩니다.

 <br>

#### onSaveInstanceState()를 사용하여 번들 데이터 저장

+ `onSaveInstanceState()`

  **Activity가 소멸되면 필요할 수 있는 데이터를 저장**하는 데 사용하는 콜백입니다. 수명 주기 콜백 다이어그램에서 `onSaveInstanceState()`는 **활동이 중지된 후 호출**됩니다. 또한 앱이 **백그라운드로 전환될 때마다** 호출됩니다. 

  `onSaveInstanceState()` 호출을 안전 조치라고 생각하세요. 활동이 포그라운드를 벗어날 때 **소량의 정보를 번들에 저장할 수 있습니다**. 이제 시스템은 이 데이터를 저장합니다. 앱이 종료될 때까지 기다리면 시스템이 리소스 압력을 받을 수 있기 때문입니다.

  `MainActivity`에서 `onSaveInstanceState()` 콜백을 재정의하고 로그 구문을 추가

  ```kotlin
  override fun onSaveInstanceState(outState: Bundle) {
     super.onSaveInstanceState(outState)
  
     Log.d(TAG, "onSaveInstanceState Called")
  }
  ```

  + `Bundle`은 키-값 쌍 모음으로, 키가 항상 문자열입니다. `Int` 및 `Boolean` 값과 같은 간단한 데이터를 번들에 넣을 수 있습니다. 시스템이 이 **번들을 메모리에 유지**하므로 번들의 **데이터를 작게** 유지하는 것이 좋습니다.

<br>

+ `onSaveInstanceState()`에서 `revenue` 값(정수), `dessertsSold`을 `putInt()` 메서드를 사용하여 번들에 넣습니다.

  ```kotlin
  outState.putInt(KEY_REVENUE, revenue)
  outState.putInt(KEY_DESSERT_SOLD, dessertsSold)
  ```


<br>

+ `onCreate()`를 사용하여 번들 데이터 복원

  + 액티비티 상태는 `onCreate(Bundle)`이나 `onRestoreInstanceState(Bundle)`에서 복원할 수 있습니다. `onSaveInstanceState()` 메서드로 채워진 `Bundle`은 두 수명 주기 콜백 메서드에 모두 전달됩니다.

  + ```kotlin
    override fun onCreate(savedInstanceState: Bundle) {
    ```

  + `onCreate()`는 호출될 때마다 `Bundle`을 가져옵니다. 프로세스 종료로 인해 **활동이 다시 시작되면 저장한 번들이 `onCreate()`에 전달**됩니다. 활동이 새로 시작되었다면 `onCreate()`의 이 `Bundle`은 `null`입니다. 따라서 **번들이 `null`이 아니면 이전에 알려진 지점에서 활동을 '다시 생성'**하고 있음을 알 수 있습니다.

  + 활동이 다시 생성되는 경우 `onRestoreInstanceState()` 콜백은 번들과 함께 `onStart()` 후에 호출됩니다. 대부분의 경우 `onCreate()`에서 액티비티 상태를 복원합니다. 그러나 `onRestoreInstanceState()`는 `onStart()` 후에 호출되므로 `onCreate()`가 호출된 후 일부 상태를 복원해야 한다면 `onRestoreInstanceState()`를 사용하면 됩니다.

  + `onCreate()`

    ```kotlin
    if (savedInstanceState != null) {
       revenue = savedInstanceState.getInt(KEY_REVENUE, 0)
       dessertsSold = savedInstanceState.getInt(KEY_DESSERT_SOLD, 0)
    }
    ```

    `getInt()` 메서드는 두 가지 인수를 사용합니다.

    + key 역할을 하는 문자열(예: 수익 값의 `"key_revenue"`)
    + 번들의 키에 값이 없는 경우를 위한 기본값

